---
title: "sp_add_log_shipping_primary_secondary (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_secondary_TSQL
- sp_add_log_shipping_primary_secondary
dev_langs: TSQL
helpviewer_keywords: sp_add_log_shipping_primary_secondary
ms.assetid: 23b3e100-5318-410e-b8f3-51c89b2dd777
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4276f846490a700a7e3c541e0616273b5f5e321f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spaddlogshippingprimarysecondary-transact-sql"></a>sp_add_log_shipping_primary_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程可在主服务器上添加辅助数据库项。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_log_shipping_primary_secondary  
[ @primary_database = ] 'primary_database',  
[ @secondary_server = ] 'secondary_server',   
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>参数  
 [  **@primary_database**  =] '*primary_database*  
 主服务器上的数据库的名称。 *primary_database*是**sysname**，无默认值。  
  
 [  **@secondary_server**  =] '*secondary_server*，  
 辅助服务器的名称。 *secondary_server*是**sysname**，无默认值。  
  
 [  **@secondary_database**  =] '*secondary_database*  
 辅助数据库的名称。 *secondary_database*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 **sp_add_log_shipping_primary_secondary**必须从运行**master**主服务器上的数据库。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_add_log_shipping_primary_secondary**添加辅助数据库的条目**LogShipAdventureWorks**到辅助服务器 FLATIRON。  
  
```  
EXEC master.dbo.sp_add_log_shipping_primary_secondary   
@primary_database = N'AdventureWorks'   
, @secondary_server = N'flatiron'   
, @secondary_database = N'LogShipAdventureWorks' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  