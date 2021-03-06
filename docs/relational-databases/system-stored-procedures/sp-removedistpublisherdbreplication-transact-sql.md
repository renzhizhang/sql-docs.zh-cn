---
title: sp_removedistpublisherdbreplication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d57034b65559e696a9692a1c71e612c7d921661b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754639"
---
# <a name="spremovedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除属于分发服务器上的特定发布的发布元数据。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher=** ] **'***发布服务器***’**  
 是发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@publisher_db=** ] **'***publisher_db***’**  
 发布数据库的名称。 *publisher_db*是**sysname** ，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_removedistpublisherdbreplication**由事务复制和快照复制。  
  
 **sp_removedistpublisherdbreplication**但不删除分发数据库，必须重新创建已发布的数据库时使用。 将删除下列元数据：  
  
-   所有的发布元数据。  
  
-   属于该发布的所有项目的元数据。  
  
-   发布的全部订阅的元数据。  
  
-   属于发布的所有复制代理作业的元数据。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色的成员的分发服务器**db_owner**分发数据库中的固定的数据库角色可以执行**sp_removedistpublisherdbreplication**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
