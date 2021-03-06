---
title: 兼容性级别 (SSAS 表格 SP1) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4587dda82f8e6e3d02581ebcd5a13bf0005b14ed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054059"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>兼容级别（SSAS 表格 SP1）
  您可以指定*兼容性级别*或导入 PowerPivot 工作簿时创建新表格模型项目时、 升级现有表格模型项目时、 升级已部署表格模型数据库。  
  
## <a name="compatibility-level"></a>兼容级别  
 通常，应该先在开发和测试计算机上安装新版本和 Service Pack，然后再在生产计算机上安装。 在此类情况下，了解如何为新的表格模型项目以及已部署到生产环境中的表格模型项目设置兼容级别十分重要。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Analysis Services 实例支持以下兼容级别（数据库版本）：  
  
-   SQL Server 2012 (1100);  
  
-   SQL Server 2012 SP1 (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>在创建新的表格模型项目时设置兼容级别  
 在创建新的表格模型项目中 SQL Server Data Tools (SSDT)，当**新的表格项目选项**对话框，可以指定兼容性级别。 您可以在创建要部署到 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本的 Analysis Services 实例还是 SQL Server 2012 Analysis Services 实例（不含 Service Pack 1）的新项目之间进行选择。  
  
 您还可以通过选择 **“不再显示此消息”** 选项指定默认的兼容级别。 所有后续项目都将使用您指定的兼容级别。 您可以通过 SSDT 在“选项”中更改默认兼容级别。  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>将现有的表格模型项目升级到 1103 兼容级别  
 可以升级在 SSDT 中在安装之前创建的表格模型项目[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]或更高版本才能使用与数据库版本 1103年兼容**兼容性级别**模型中的属性**属性**窗口。 为了升级表格模型项目，安装 SSDT 的计算机必须安装了 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本，并且工作区数据库所在的 Analysis Services 实例必须也安装了[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本。 不能降级到更早的版本。  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>将已部署的表格模型数据库升级到 1103 兼容级别  
 你可以通过使用升级现有部署的表格模型数据库版本 1103 兼容 SQL Server Management Studio (SSMS) 中**兼容性级别**属性中的**数据库属性**. 为了进行升级，安装 SQL Server Analysis Services 实例的计算机必须安装 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本。 不能将已部署的表格模型数据库降级到更早的版本。  
  
### <a name="import-from-powerpivot"></a>从 PowerPivot 导入  
 在通过从 PowerPivot 导入来创建新的表格模型项目时，您可以指定是要将兼容级别升级到默认兼容级别（如果以前已在 SSDT 中配置），还是将该兼容级别保留为已在 PowerPivot 工作簿中指定的兼容级别。  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>检查 SSMS 中表格模型数据库的兼容级别  
 可以通过查看检查 SSMS 中表格模型数据库的兼容性级别**兼容性级别**属性 (中的新增功能[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) 中**数据库属性**。  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>检查 SSMS 中 Analysis Services 实例支持的兼容级别  
 可以通过查看检查 SSMS 中支持的兼容级别**支持的兼容级别**上的属性**信息**页面 (中的新增功能[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) 中**分析服务属性**。 支持的兼容级别 1103 指示安装了 SQL Server SP1 或更高版本。 不能更改支持的兼容级别。  
  
  
