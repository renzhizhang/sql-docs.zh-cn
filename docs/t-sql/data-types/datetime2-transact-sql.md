---
title: "datetime2 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetime2
- datetime2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- dates [SQL Server], data types
- date and time [SQL Server], datetime2
- data types [SQL Server], date and time
- datetime2 data type [SQL Server]
ms.assetid: 868017f3-214f-43ef-8536-cc1632a2288f
caps.latest.revision: 58
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13766b3d0cb86780c2eca55c7f36e8fd16e973c5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2-transact-sql"></a>datetime2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定义结合了 24 小时制时间的日期。 **datetime2**可视为现有扩展**datetime**具有更大的日期范围、 更大的默认小数精度和可选的用户指定的精度的类型。
  
## <a name="datetime2-description"></a>datetime2 说明
  
|属性|值|  
|--------------|-----------|  
|语法|**datetime2** [(*秒的小数部分精度*)]|  
|用法|声明@MyDatetime2 **datetime2 （7)**<br /><br /> 创建表 Table1 (Column1 **datetime2 （7)** )|  
|默认字符串文本格式<br /><br /> （用于下级客户端）|YYYY-MM-DD hh:mm:ss[.fractional seconds]<br /><br /> 有关详细信息，请参阅"下层客户端向后的兼容性"下一节。|  
|日期范围|0001-01-01 到 31.12.99<br /><br /> 年 1 月 1，1 公元年 12 月 31 日，9999|  
|时间范围|00:00:00 到 23:59:59.9999999|  
|时区偏移量范围|无|  
|各元素的范围|YYYY 是一个四位数，范围从 0001 到 9999，表示年份。<br /><br /> MM 是一个两位数，范围从 01 到 12，它表示指定年份中的月份。<br /><br /> DD 是一个两位数，范围为 01 到 31（具体取决于月份），它表示指定月份中的某一天。<br /><br /> hh 是一个两位数，范围从 00 到 23，它表示小时。<br /><br /> mm 是一个两位数，范围从 00 到 59，它表示分钟。<br /><br /> ss 是一个两位数，范围从 00 到 59，它表示秒钟。<br /><br /> n* 代表 0 到 7 位数字，范围从 0 到 9999999，它表示秒小数部分。 在 Informatica，秒的小数部分时将被截断 n > 3。|  
|字符长度|最低 19 位 (YYYY-MM-DD hh:mm:ss )，最高 27 位 (YYYY-MM-DD hh:mm:ss.0000000)|  
|精度、小数位数|0 至 7 位，准确度为 100ns。 默认精度为 7 位数。|  
|存储大小|精度小于 3 时为 6 个字节；精度为 3 和 4 时为 7 个字节。 所有其他精度则需要 8 个字节。|  
|精确度|100 纳秒|  
|默认值|1900-01-01 00:00:00|  
|日历|公历|  
|用户定义的秒的小数部分精度|是|  
|时区偏移量感知和保留|是|  
|夏时制感知|是|  
  
数据类型元数据，请参阅[sys.systypes &#40;Transact SQL &#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)或[TYPEPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md). 某些日期和时间数据类型的精度和小数位数是可变的。 若要获取的精度和小数位数的列，请参阅[COLUMNPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)， [COL_LENGTH &#40;Transact SQL &#41;](../../t-sql/functions/col-length-transact-sql.md)，或[sys.columns &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).
  
## <a name="supported-string-literal-formats-for-datetime2"></a>支持 datetime2 字符串格式
下表列出了支持的 ISO 8601 和 ODBC 字符串文本的格式为**datetime2**。 字母、 数字、 未分隔，和时间格式的日期和时间部分的有关信息**datetime2**，请参阅[日期 &#40;Transact SQL &#41;](../../t-sql/data-types/date-transact-sql.md)和[时间 &#40;Transact SQL &#41;](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|“说明”|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> YYYY-MM-DDThh:mm:ss[.nnnnnnn]|此格式不受 SET LANGUAGE 和 SET DATEFORMAT 会话区域设置的影响。 **T**，冒号 （:） 和句点 （.） 中包含字符串文本，例如"2007年-05-02T19:58:47.1234567。|  
  
|ODBC|Description|  
|---|---|
|{ ts 'yyyy-mm-dd hh:mm:ss[.fractional seconds]' }|特定于 ODBC API：<br /><br /> 小数点右侧的数字表示秒小数部分，可指定 0 到 7 位（100 纳秒）。|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 法规遵从性  
ANSI 和 ISO 8601 的法规遵从性[日期](../../t-sql/data-types/date-transact-sql.md)和[时间](../../t-sql/data-types/time-transact-sql.md)适用于**datetime2**。
  
##  <a name="backward-compatibility-for-down-level-clients"></a>下级客户端的向后兼容性  
不支持某些下层客户端**时间**，**日期**， **datetime2**和**datetimeoffset**数据类型。 下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上级实例与下级客户端之间的类型映射。
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型|传递给下级客户端的默认字符串文字格式|下级 ODBC|下级 OLEDB|下级 JDBC|下级 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
|**datetimeoffset**|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|String 或 SqString|  
  
## <a name="converting-date-and-time-data"></a>将日期和时间数据转换
当转换为日期和时间数据类型时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会拒绝它无法识别为日期或时间的所有值。 CAST 和 CONVERT 函数中使用的日期和时间数据的信息，请参阅[CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>将其他日期和时间类型转换为 datetime2 数据类型
本部分介绍其他日期和时间数据类型转换为时会发生什么情况**datetime2**数据类型。  
  
当转换是来自**日期**，复制年、 月和日。  时间组成部分设置为 00:00:00.0000000。  下面的代码显示将 `date` 值转换为 `datetime2` 值的结果。  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
当转换是来自**time(n)**，复制时间组件，并且日期部分设置为 1900年-01-01。 下面的示例显示了将 `time(7)` 值转换为 `datetime2` 值的结果。  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
当转换是来自**smalldatetime**，复制的小时和分钟数。 秒和秒的小数部分设置为 0。 下面的代码显示将 `smalldatetime` 值转换为 `datetime2` 值的结果。  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
当转换是来自**datetimeoffset(n)**，复制的日期和时间的组件。 时区被截断。 下面的示例显示了将 `datetimeoffset(7)` 值转换为 `datetime2` 值的结果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

当转换是来自**datetime**，复制的日期和时间。  小数精度扩展到 7 的数字。  下面的示例显示了将 `datetime` 值转换为 `datetime2` 值的结果。

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  
  
### <a name="converting-string-literals-to-datetime2"></a>将字符串文字转换为 datetime2  
如果字符串所有部分的格式均有效，则允许从字符串文字转换为日期和时间类型。 否则，将引发运行时错误。 从日期和时间类型向字符串文字进行的未指定样式的隐式转换或显式转换将采用当前会话的默认格式。 下表显示了规则将字符串转换为文本**datetime2**数据类型。
  
|输入字符串文字|**datetime2(n)**|  
|---|---|
|ODBC DATE|ODBC 字符串映射到**datetime**数据类型。 从 ODBC 日期时间文本中插入任何赋值运算**datetime2**类型将导致之间的隐式转换**datetime**和此类型定义的转换规则。|  
|ODBC TIME|请参阅前面的 ODBC DATE 规则。|  
|ODBC DATETIME|请参阅前面的 ODBC DATE 规则。|  
|仅 DATE|TIME 部分默认为 00:00:00。|  
|仅 TIME|DATE 部分默认为 1900-1-1。|  
|仅 TIMEZONE|提供默认值。|  
|DATE + TIME|无庸赘述|  
|DATE + TIMEZONE|不允许。|  
|TIME + TIMEZONE|DATE 部分默认为 1900-1-1。 忽略 TIMEZONE 输入。|  
|DATE + TIME + TIMEZONE|将使用本地 DATETIME。|  
  
## <a name="examples"></a>示例  
下面的示例强制转换到每个字符串的结果进行比较**日期**和**时间**数据类型。
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|数据类型|“输出”|  
|---|---|
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
