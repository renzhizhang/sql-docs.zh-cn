---
title: 从查询中删除表 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bda582c7b9171e89a43b6870b3b6c2df139b7b11
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52763609"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>从查询中删除表 (Visual Database Tools)
  可从查询中移除表或任何表值对象。  
  
> [!NOTE]  
>  移除表或表值对象不会从数据库中删除任何内容，该操作只会将表或表值对象从当前查询中移除。 有关从数据库中删除一个表的详细信息，请参阅[删除的表&#40;数据库引擎&#41;](../../relational-databases/tables/delete-tables-database-engine.md)。  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>移除表或表结构对象  
  
-   在“关系图”窗格中，选择表、视图、用户定义函数、同义词或查询，再按 Delete；或者右键单击该对象，然后在显示的对话框中选择“删除”。 您可一次选择和移除多个对象。  
  
     -或-  
  
-   在 **SQL 窗格**中删除对该对象的所有引用。  
  
 当移除表或表值对象时，查询和视图设计器将自动删除涉及该表或表值对象的联接，并在“SQL 窗格”和“条件窗格”中删除对该对象的列的引用。 但是，如果查询包含涉及该对象的复杂表达式，则只有在移除对该对象的所有引用后才会自动移除该对象。  
  
## <a name="see-also"></a>请参阅  
 [向查询添加表&#40;可视化数据库工具&#41;](visual-database-tools.md)   
 [创建表别名&#40;可视化数据库工具&#41;](create-table-aliases-visual-database-tools.md)   
 [指定搜索条件&#40;可视化数据库工具&#41;](specify-search-criteria-visual-database-tools.md)   
 [汇总查询结果&#40;可视化数据库工具&#41;](summarize-query-results-visual-database-tools.md)   
 [执行基本的查询操作 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
