---
title: 启用资源调控器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, enabling
ms.assetid: 4d17af53-cf11-4ce4-aab4-deda94a49836
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5ef8d77de1df31387d33e6577fe84bd5ef9fa680
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52806179"
---
# <a name="enable-resource-governor"></a>启用资源调控器
  默认情况下，资源调控器处于关闭状态。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 启用资源调控器。  
  
-   **开始之前：**[限制和局限](#LimitationsRestrictions)，[权限](#Permissions)  
  
-   **若要启用资源调控器，请使用：**[对象资源管理器](#RGOnObjEx)，[资源调控器属性](#RGOnProp)， [Transact SQL](#RGOnTSQL)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 启用资源调控器会产生下列结果：  
  
-   为新连接运行分类器函数，以便可以将其工作负荷分配到工作负荷组。  
  
-   遵守并强制执行资源调控器配置中指定的资源限制。  
  
-   禁用资源调控器时所做的任何配置更改会影响在启用资源调控器之前就已存在的请求。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 在用户事务中时，您不能使用 `ALTER RESOURCE GOVERNOR` 语句启用资源调控器。  
  
###  <a name="Permissions"></a> Permissions  
 启用资源调控器需要 CONTROL SERVER 权限。  
  
##  <a name="RGOnObjEx"></a> 使用对象资源管理器启用资源调控器  
 **使用对象资源管理器启用资源调控器**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中打开对象资源管理器，并依次逐步展开 **“管理”** 节点直至 **“资源调控器”**。  
  
2.  右键单击“资源调控器” ，再单击“启用” 。  
  
##  <a name="RGOnProp"></a> 使用资源调控器属性启用资源调控器  
 **使用“资源调控器属性”页启用资源调控器**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中打开对象资源管理器，并依次逐步展开 **“管理”** 节点直至 **“资源调控器”**。  
  
2.  右键单击“资源调控器”  ，然后单击“属性” ，这将打开“资源调控器属性”页  。  
  
3.  单击 **“启用资源调控器”** 复选框，再单击 **“确定”**。  
  
##  <a name="RGOnTSQL"></a> 使用 Transact-SQL 启用资源调控器  
 **使用 Transact-SQL 启用资源调控器**  
  
1.  运行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 以下示例启用资源调控器。  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [资源调控器](resource-governor.md)   
 [禁用资源调控器](disable-resource-governor.md)   
 [资源调控器资源池](resource-governor-resource-pool.md)   
 [资源调控器工作负荷组](resource-governor-workload-group.md)   
 [资源调控器分类器函数](resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
