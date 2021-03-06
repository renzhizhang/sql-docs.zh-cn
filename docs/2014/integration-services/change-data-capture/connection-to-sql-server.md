---
title: 连接到 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09d597cb7776362c44ca53e8d544f66608d8d37c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377195"
---
# <a name="connection-to-sql-server"></a>连接到 SQL Server
  在不含对 MSXDBCDC 数据库具有写入权限的数据库角色（例如 **db_owner** 角色）的登录名尝试创建某一 Oracle CDC 实例时，“连接到 SQL Server”对话框将显示。  
  
 在此对话框中，必须为对 MSXDBCDC 数据库具有写入权限的登录名（例如 **db_owner** 数据库角色）输入凭据，以便创建新的 Oracle CDC 实例。  
  
 在“连接到 SQL Server”对话框中输入以下信息。  
  
### <a name="server-name"></a>服务器名称  
 键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的服务器的名称。  
  
### <a name="authentication"></a>身份验证  
 选择下列选项之一：  
  
-   Windows 身份验证  
  
-   **SQL Server 身份验证**:如果选择此选项，则必须键入**登录名**并**密码**中的用户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要连接到。  
  
### <a name="options"></a>选项  
 单击箭头可以查看要配置的可用选项。 您可以选择保留这些选项不变，使用其默认值。 可用选项是：  
  
-   **连接超时**:键入程序等待的时间 （以秒为单位）[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成超时错误之前建立连接。 默认值为 **15**。  
  
-   **执行超时值**:类型的程序将等待 SQL 命令执行完成后将生成超时错误的时间 （以秒为单位）。 默认值为 **30**。  
  
-   **对连接进行加密**:选择**加密连接**，确保[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在建立连接进行加密以保护隐私。  
  
-   **高级**：单击“高级”并根据需要在“高级连接属性”对话框中键入任何附加的连接属性。  
  
## <a name="see-also"></a>请参阅  
 [针对 CDC 服务的 SQL Server 连接所需权限](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
