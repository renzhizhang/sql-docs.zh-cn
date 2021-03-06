---
title: sp_delete_maintenance_plan_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan_job
- sp_delete_maintenance_plan_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan_job
ms.assetid: 1c2148c3-2928-4d9b-b1c8-3512cfbd6a63
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c4daab0b36ff21fea956c1c5b0db27588cc5acee
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168697"
---
# <a name="spdeletemaintenanceplanjob-transact-sql"></a>sp_delete_maintenance_plan_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  取消指定作业与指定维护计划的关联。  
  
> [!NOTE]  
>  数据库维护计划使用这些存储过程。 但此功能已由不使用此存储过程的维护计划取代。 可使用此过程对从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级的安装维护数据库维护计划。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_maintenance_plan_job [ @plan_id = ] 'plan_id' ,   
   [ @job_id = ] 'job_id'   
```  
  
## <a name="arguments"></a>参数  
 [  **@plan_id =**] **'**_计划\_id_  
 指定维护计划的 ID。 *plan_id*是**uniqueidentifier**，并且必须是有效的 id。  
  
 [  **@job_id =**] **'**_作业\_id_  
 指定与维护计划相关联的作业的 ID。 *job_id*是**uniqueidentifier**，并且必须是有效的 id。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_delete_maintenance_plan_job**必须从运行**msdb**数据库。  
  
 如果已从维护计划中删除所有作业，我们建议用户执行**sp_delete_maintenance_plan_db**若要从计划中删除剩余的数据库。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_delete_maintenance_plan_job**。  
  
## <a name="examples"></a>示例  
 以下示例从维护计划中删除作业“B8FCECB1-E22C-11D2-AA64-00C04F688EAE”。  
  
```  
EXECUTE   sp_delete_maintenance_plan_job N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'B8FCECB1-E22C-11D2-AA64-00C04F688EAE';  
```  
  
## <a name="see-also"></a>请参阅  
 [维护计划](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [数据库维护计划存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
