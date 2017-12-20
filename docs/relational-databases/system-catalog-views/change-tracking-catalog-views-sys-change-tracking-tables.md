---
title: "sys.change_tracking_tables (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- change_tracking_tables_TSQL
- sys.change_tracking_tables
- change_tracking_tables
- sys.change_tracking_tables_TSQL
dev_langs: TSQL
helpviewer_keywords:
- change tracking [SQL Server], sys.change_tracking_tables
- sys.change_tracking_tables
ms.assetid: 97ec69b6-0d49-4d98-82f0-d3e77ba1ad2b
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a921017fae8b8ec70c04787a8327c9389df23f3f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="change-tracking-catalog-views---syschangetrackingtables"></a>更改跟踪目录视图-sys.change_tracking_tables
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  为当前数据库中已启用更改跟踪的每个表返回一行。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|具有更改日志的表的 ID。 即使更改跟踪当前已关闭，表仍然可以具有更改日志。<br /><br /> 此表 ID 在数据库中是唯一的。|  
|is_track_columns_updated_on|**bit**|该表的更改跟踪的当前状态：<br /><br /> 0 = OFF<br /><br /> 1 = ON|  
|begin_version|**bigint**|开始对该表进行更改跟踪时数据库的版本。 此版本通常指示何时启用更改跟踪，但如果已截断该表，则会重置该值。|  
|cleanup_version|**bigint**|一个版本，在该版本以前的版本中，清除操作可能会删除更改跟踪信息。|  
|min_valid_version|**bigint**|该表可用的更改跟踪信息的最低有效版本。<br /><br /> 从该表中获取与该行关联的更改时，last_sync_version 的值必须大于或等于此列报告的版本。 有关详细信息，请参阅[CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact SQL &#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md).|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CHANGE_TRACKING_MIN_VALID_VERSION (Transact-SQL)](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [更改跟踪目录视图 &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [跟踪数据更改 (SQL Server)](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  