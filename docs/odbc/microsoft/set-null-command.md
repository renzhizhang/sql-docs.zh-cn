---
title: "SET NULL 命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14cade223de7014dd4a0c27295d3ff742d18af17
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="set-null-command"></a>SET NULL 命令
确定如何支持 null 值的 ALTER TABLE-SQL、 创建表的 SQL 和插入的 SQL 命令。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （默认为驱动程序; Visual FoxPro 的默认值为 OFF。）指定使用 ALTER TABLE 和 CREATE TABLE 创建的表中的所有列都允许 null 值。 您可以通过在列的定义中包含的 NOT NULL 子句覆盖表中的列的 null 值支持。  
  
 此外指定它插入-SQL 将插入 null 值到插入-SQL VALUE 子句中不包含任何列。 插入的 SQL 将插入 null 值仅允许 null 值的列。  
  
 OFF  
 指定使用 ALTER TABLE 和 CREATE TABLE 创建的表中的所有列将不都允许 null 值。 您可以通过在列的定义中包含 NULL 子句指定 ALTER TABLE 和 CREATE TABLE 中的列的 null 值支持。  
  
 此外指定它插入-SQL 将插入空值到插入-SQL VALUE 子句中不包含任何列。  
  
## <a name="remarks"></a>注释  
 ALTER TABLE、 CREATE TABLE 和 INSERT-SQL 支持 SET NULL 影响仅如何 null 值。 其他命令不会受到设置为 NULL。  
  
## <a name="see-also"></a>另请参阅  
 [更改表的 SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [创建表的 SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [插入的 SQL 命令](../../odbc/microsoft/insert-sql-command.md)