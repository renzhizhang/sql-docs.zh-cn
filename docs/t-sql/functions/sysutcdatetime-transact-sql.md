---
title: "SYSUTCDATETIME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/01/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYSUTCDATETIME
- SYSUTCDATETIME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- date and time [SQL Server], SYSUTCDATETIME
- SYSUTCDATETIME function [SQL Server]
- time [SQL Server], system
ms.assetid: f14fc2cd-9ea8-4daf-88f4-418cf523ab55
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9dfaf40ac3d7722c39592fc3e7b4d4e790ec25f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sysutcdatetime-transact-sql"></a>SYSUTCDATETIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回**datetime2**值，该值包含的日期和时间的计算机上的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 日期和时间作为 UTC 时间（通用协调时间）返回。 秒部分精度规范的范围为 1 至 7 位。 默认精度为 7 位数。  
  
> [!NOTE]  
>  SYSDATETIME 和 SYSUTCDATE 在秒的小数部分精度上要比 GETDATE 和 GETUTCDATE 高。 SYSDATETIMEOFFSET 包含系统时区偏移量。 SYSDATETIME、SYSUTCDATE 和 SYSDATETIMEOFFSET 可分配给任何一种日期和时间类型的变量。  
  
 有关的所有概述[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和时间数据类型和函数，请参阅[日期和时间数据类型和函数](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SYSUTCDATETIME ( )  
```  
  
## <a name="return-type"></a>返回类型  
 **datetime2**  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]语句可以指 SYSUTCDATETIME 随处它们可引用**datetime2**表达式。  
  
 SYSUTCDATETIME 是不确定性函数。 不能对在列中引用该函数的视图和表达式建立索引。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用 GetSystemTimeAsFileTime() Windows API 中获取日期和时间值。 精确程度取决于运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机硬件和 Windows 版本。 此 API 的精度固定为 100 纳秒。 可以使用 GetSystemTimeAdjustment() Windows API 确定准确性。  
  
## <a name="examples"></a>示例  
 以下示例使用六个返回当前日期和时间的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统函数来返回日期和/或时间。 序列; 中返回的值因此，其秒的小数部分可能会有所不同。  
  
### <a name="a-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>A. 显示由日期和时间函数返回的格式  
 下面的示例显示由日期和时间函数返回的其他格式。  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `SYSDATETIME()      2007-04-30 13:10:02.0474381`  
  
 `SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00`  
  
 `SYSUTCDATETIME()   2007-04-30 20:10:02.0474381`  
  
 `CURRENT_TIMESTAMP  2007-04-30 13:10:02.047`  
  
 `GETDATE()          2007-04-30 13:10:02.047`  
  
 `GETUTCDATE()       2007-04-30 20:10:02.047`  
  
### <a name="b-converting-date-and-time-to-date"></a>B. 将日期和时间转换为日期  
 下面的示例说明如何将日期和时间值转换为 `date`。  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
### <a name="c-converting-date-and-time-values-to-time"></a>C. 将日期和时间值转换为时间  
 下面的示例说明如何将日期和时间值转换为 `time`。  
  
 `DECLARE @DATETIME DATETIME = GetDate();`  
  
 `DECLARE @TIME TIME`  
  
 `SELECT @TIME = CONVERT(time, @DATETIME)`  
  
 `SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Time             Date Time`  
  
 `13:49:33.6330000 2009-04-22 13:49:33.633`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例使用六个返回当前日期和时间的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统函数来返回日期和/或时间。 序列; 中返回的值因此，其秒的小数部分可能会有所不同。  
  
### <a name="d-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>D. 显示由日期和时间函数返回的格式  
 下面的示例显示由日期和时间函数返回的其他格式。  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `SYSDATETIME()      2007-04-30 13:10:02.0474381`  
  
 `SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00`  
  
 `SYSUTCDATETIME()   2007-04-30 20:10:02.0474381`  
  
 `CURRENT_TIMESTAMP  2007-04-30 13:10:02.047`  
  
 `GETDATE()          2007-04-30 13:10:02.047`  
  
 `GETUTCDATE()       2007-04-30 20:10:02.047`  
  
### <a name="e-converting-date-and-time-to-date"></a>E. 将日期和时间转换为日期  
 下面的示例说明如何将日期和时间值转换为 `date`。  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
### <a name="f-converting-date-and-time-values-to-time"></a>F. 将日期和时间值转换为时间  
 下面的示例说明如何将日期和时间值转换为 `time`。  
  
 `DECLARE @DATETIME DATETIME = GetDate();`  
  
 `DECLARE @TIME TIME`  
  
 `SELECT @TIME = CONVERT(time, @DATETIME)`  
  
 `SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Time             Date Time`  
  
 `13:49:33.6330000 2009-04-22 13:49:33.633`  
  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [时区 &AMP; #40;Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


