---
title: GPU 支持和 TensorFlow
titleSuffix: SQL Server 2019 big data clusters
description: 部署具有 GPU 支持的大数据群集和在 Azure 数据 Studio 笔记本中使用 TensorFlow。
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: craigg
ms.date: 03/14/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f766c343152fa601cc22e59e3385c454ec23879
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161908"
---
# <a name="deploy-a-big-data-cluster-with-gpu-support-and-run-tensorflow"></a>部署具有 GPU 支持的大数据群集和运行 TensorFlow

本文演示如何将大数据群集在 Azure Kubernetes 服务 (AKS) 支持启用了 GPU 的节点池的计算密集型工作负荷的部署。 然后，在执行使用 TensorFlow 图像分类的 GPU 的 Azure Data Studio 中运行 notebook 示例。

## <a name="prerequisites"></a>先决条件

- [大数据工具](deploy-big-data-tools.md):
  - **mssqlctl**
  - **kubectl**
  - **Azure Data Studio**
  - **SQL Server 2019 扩展**
  - **Azure CLI**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="create-an-aks-cluster"></a>创建 AKS 群集

以下步骤使用 Azure CLI 创建支持 Gpu 的 AKS 群集。

1. 在命令提示符处，运行以下命令并按照提示登录到你的 Azure 订阅：

    ```azurecli
    az login
    ```

1. 创建一个包含资源组**az 组创建**命令。 下面的示例创建名为的资源组`sqlbigdatagroupgpu`在`eastus`位置。

   ```azurecli
   az group create --name sqlbigdatagroupgpu --location eastus
   ```

1. 在与 AKS 创建 Kubernetes 群集[az aks 创建](https://docs.microsoft.com/cli/azure/aks)命令。 下面的示例创建名为的 Kubernetes 群集`gpucluster`在`sqlbigdatagroupgpu`资源组。

   ```azurecli
   az aks create --name gpucluster --resource-group sqlbigdatagroupgpu --generate-ssh-keys --node-vm-size Standard_NC6 --node-count 3 --node-osdisk-size 50 --kubernetes-version 1.11.7 --location eastus
   ```

   > [!NOTE]
   > 此群集使用**Standard_NC6** [GPU 优化虚拟机大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-gpu)，这是一个专门适用于单个或多个 NVIDIA Gpu 的虚拟机。 有关详细信息，请参阅[计算密集型工作负荷在 Azure Kubernetes 服务 (AKS) 的使用 Gpu](https://docs.microsoft.com/azure/aks/gpu-cluster)。

1. 若要配置 kubectl 以连接到 Kubernetes 群集，运行[az aks get-credentials 来获取凭据](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials)命令。

   ```azurecli
   az aks get-credentials --overwrite-existing --resource-group=sqlbigdatagroupgpu --name gpucluster
   ```

## <a name="apply-yaml-manifest"></a>应用 YAML 清单

1. 使用**kubectl**创建名为 Kubernetes 命名空间`gpu-resources`。

   ```
   kubectl create namespace gpu-resources
   ```

1. 将以下 YAML 文件的内容保存到名为的文件**nvidia 设备插件 ds.yaml**。 将其保存到工作目录运行在计算机上**kubectl**从。

   更新`image: nvidia/k8s-device-plugin:1.11`一半下要与 Kubernetes 版本匹配的清单。 例如，如果你的 AKS 群集运行 Kubernetes 1.12 版起，更新到标记`image: nvidia/k8s-device-plugin:1.12`。

   ```yaml
   apiVersion: extensions/v1beta1
   kind: DaemonSet
   metadata:
     labels:
       kubernetes.io/cluster-service: "true"
     name: nvidia-device-plugin
     namespace: gpu-resources
   spec:
     template:
       metadata:
         # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler
         # reserves resources for critical add-on pods so that they can be rescheduled after
         # a failure.  This annotation works in tandem with the toleration below.
         annotations:
           scheduler.alpha.kubernetes.io/critical-pod: ""
         labels:
           name: nvidia-device-plugin-ds
       spec:
         tolerations:
         # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode.
         # This, along with the annotation above marks this pod as a critical add-on.
         - key: CriticalAddonsOnly
           operator: Exists
         containers:
         - image: nvidia/k8s-device-plugin:1.11 # Update this tag to match your Kubernetes version
           name: nvidia-device-plugin-ctr
           securityContext:
             allowPrivilegeEscalation: false
             capabilities:
               drop: ["ALL"]
           volumeMounts:
             - name: device-plugin
               mountPath: /var/lib/kubelet/device-plugins
         volumes:
           - name: device-plugin
             hostPath:
               path: /var/lib/kubelet/device-plugins
         nodeSelector:
           beta.kubernetes.io/os: linux
           accelerator: nvidia
   ```

1. 现在使用 kubectl apply 命令创建 DaemonSet。 **nvidia 设备插件 ds.yaml**运行以下命令必须为工作目录中：

   ```
   kubectl apply -f nvidia-device-plugin-ds.yaml
   ```

## <a name="deploy-the-big-data-cluster"></a>部署大数据群集

若要部署支持 Gpu 的 SQL Server 2019 大数据群集 （预览版），您必须从特定的 docker 注册表和存储库部署。 具体而言，使用不同的值**DOCKER_REGISTRY**， **DOCKER_REPOSITORY**， **DOCKER_USERNAME**， **DOCKER_PASSWORD**，并**DOCKER_EMAIL**。 以下部分提供有关如何设置环境变量的示例。 使用的 Windows 或 Linux 部分取决于平台的客户端用来部署大数据群集。

### <a name="windows"></a>Windows

   1. 使用 CMD 窗口 (而不是 PowerShell)，配置以下环境变量。 不要使用引号将值。

      ```cmd
      SET ACCEPT_EULA=yes
      SET CLUSTER_PLATFORM=aks

      SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
      SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
      SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
      SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

      SET DOCKER_REGISTRY=marinchcreus3.azurecr.io
      SET DOCKER_REPOSITORY=ctp23-8-0-61-gpu
      SET DOCKER_USERNAME=<your username, gpu-specific credentials provided by Microsoft>
      SET DOCKER_PASSWORD=<your password, gpu-specific credentials provided by Microsoft>
      SET DOCKER_EMAIL=<your email address>
      SET DOCKER_PRIVATE_REGISTRY=1
      SET STORAGE_SIZE=10Gi
      ```

   1. 部署大数据群集：

      ```cmd
      mssqlctl cluster create --name gpubigdatacluster
      ```

### <a name="linux"></a>Linux

   1. 初始化以下环境变量。 在 bash 中，可以使用引号将每个值。

      ```bash
      export ACCEPT_EULA=yes
      export CLUSTER_PLATFORM="aks"

      export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
      export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
      export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
      export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

      export DOCKER_REGISTRY="marinchcreus3.azurecr.io"
      export DOCKER_REPOSITORY="ctp23-8-0-61-gpu"
      export DOCKER_USERNAME="<your username, gpu-specific credentials provided by Microsoft>"
      export DOCKER_PASSWORD="<your password, gpu-specific credentials provided by Microsoft>"
      export DOCKER_EMAIL="<your email address>"
      export DOCKER_PRIVATE_REGISTRY="1"
      export STORAGE_SIZE="10Gi"
      ```

   1. 部署大数据群集：

      ```bash
      mssqlctl cluster create --name gpubigdatacluster
      ```

## <a name="run-the-tensorflow-example"></a>运行 TensorFlow 示例

以下两个示例 notebook 演示培训两个图像分类模型，对于 GPU 使用 TensorFlow 的 Spark 群集在单个节点上。

| Notebook 下载 | Description |
|---|---|
| [**tf-cuda8.ipynb**](https://aka.ms/AA4jdgd) | 使用 8 CUDA、 CUDNN 6 和 TensorFlow 1.4.0。  |
| [**tf-cuda9.ipynb**](https://aka.ms/AA4ixzr) | 使用 CUDA 9 和 CUDNN 7，TensorFlow 1.12.0。 |

将相应笔记本文件到本地计算机，然后打开并在 Azure Data Studio 使用的 PySpark3 内核中运行它。 除非有特定需要 CUDA 或 TensorFlow 的较旧版本，否则选择 CUDA 9/CUDNN 7/TensorFlow 1.12.0。 有关如何使用大数据群集上笔记本的详细信息，请参阅[如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)。

> [!NOTE]
> 请注意笔记本系统位置中安装软件。 这可能是因为笔记本目前以 CTP 2.3 中的 root 权限运行。

在对于 GPU 安装 NVIDIA GPU 库和 TensorFlow，笔记本列出可用的 GPU 设备。 然后，它们适合，并评估 TensorFlow 模型来识别手写的数字使用 MNIST 数据集。 在检查可用磁盘空间后, 它们下载并运行从 CIFAR 10 图像分类示例[ https://github.com/tensorflow/models.git ](https://github.com/tensorflow/models.git)。 通过在群集具有不同的 Gpu 上运行 CIFAR 10 示例，可以观察到的速度增长提供 GPU 可用在 Azure 中的每个生成。

## <a name="clean-up-resources"></a>清理资源

若要删除的大数据群集，请使用以下命令：

```
mssqlctl cluster delete --name gpubigdatacluster
```

前一命令不会删除 AKS 群集。 若要删除 AKS 群集并与之关联的资源，请使用以下命令：

```azurecli
az group delete -n sqlbigdatagroupgpu
```

## <a name="next-steps"></a>后续步骤

有关 SQL Server 2019 大数据群集 （预览版） 的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。