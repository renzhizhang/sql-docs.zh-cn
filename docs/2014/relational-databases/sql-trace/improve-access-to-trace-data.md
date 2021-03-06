---
title: 改进对跟踪数据的访问 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], space
- SQL Server Profiler, space
- space [SQL Server], SQL Server Profiler
ms.assetid: c260c000-fd53-4831-993f-df6894f3228b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 540a0bd9430a182ef3eda43fd816b4a495dc36b5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767872"
---
# <a name="improve-access-to-trace-data"></a>改进对跟踪数据的访问
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 使用 **temp** 目录中的空间来改进对跟踪数据的访问。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 需要至少 10 兆字节 (MB) 的可用空间。 如果在使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]时可用空间低于 10 MB，则所有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 功能都将会停止。  
  
 在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 使用 **temp** 目录的空间时，对该空间的使用可能导致 **temp** 目录所包含的数据量迅速增长。 为了避免出现文件增大的问题，可以通过更改 TEMP 环境变量的值，将 **temp** 目录放在非系统驱动器的驱动器上。  
  
 以下过程说明如何在大多数 Microsoft Windows 操作系统中更改 TEMP 环境变量的值。 有关设置环境变量的详细信息，请参阅 Windows 操作系统文档。  
  
### <a name="to-change-the-temp-environment-variable-in-windows-operating-systems"></a>在 Windows 操作系统中更改 TEMP 环境变量  
  
1.  在 **“开始”** 菜单上，选择 **“控制面板”**，再单击 **“系统”**。  
  
2.  在 **“系统属性”** 对话框中，单击 **“高级”** 选项卡，再单击 **“环境变量”**。  
  
3.  向下滚动 **“系统变量”** 列表，选择对应于 **TEMP** 变量的行，并单击 **“编辑”**。  
  
4.  在 **“编辑系统变量”** 对话框中，输入要作为 **temp** 目录的驱动器及目录的路径和名称。  
  
5.  单击 **“确定”** 保存更改。  
  
## <a name="see-also"></a>请参阅  
 [启动 SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
