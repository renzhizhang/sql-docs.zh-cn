---
title: 在跟踪中筛选服务器进程 ID (SPID) (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fb45338f5fde510ea8a838e763ba46c03ff84c96
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202157"
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>在跟踪中筛选服务器进程 ID (SPID) (SQL Server Profiler)
  本主题说明了如何通过 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]在跟踪中筛选服务器进程标识符 (SPID)。  
  
### <a name="to-filter-system-ids-in-a-trace"></a>在跟踪中筛选系统 ID  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”**，再连接到 SQL Server 实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”，则不会显示“跟踪属性”对话框，而是开始跟踪。 若要关闭此设置，请在“工具”菜单上，单击“选项”，然后清除“建立连接后立即开始跟踪”复选框。  
  
2.  在 **“跟踪名称”** 框中，键入跟踪的名称。  
  
3.  在“使用模板”名称列表中，选择跟踪模板。  
  
4.  根据需要，指定保存跟踪结果的目标文件或表。  
  
5.  在“事件选择”选项卡上，单击“SPID”列标题以启动“编辑筛选器”对话框。 还可以右键单击列标题，然后选择“编辑列筛选器”。 如果 **SPID** 列不出现，请选中 **“显示所有列”** 框。  
  
6.  在 **“编辑筛选器”** 对话框中，展开相应的比较运算符，输入 SPID 作为比较的值。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 事件探查器](sql-server-profiler.md)  
  
  