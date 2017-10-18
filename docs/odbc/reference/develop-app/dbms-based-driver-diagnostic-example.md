---
title: "基于 DBMS 的驱动程序诊断示例 |Microsoft 文档"
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
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c0a20af8dc2a35ba451890472ad1af73e01d8688
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="dbms-based-driver-diagnostic-example"></a>基于 DBMS 的驱动程序诊断示例
基于 DBMS 的驱动程序将请求发送到 DBMS，并将信息返回给应用程序通过驱动程序管理器。 由于的驱动程序接口与驱动程序管理器中的组件，其格式，并返回自变量**SQLGetDiagRec**。  
  
 例如，如果对 Oracle Rdb 遇到无效的临时表名称，请使用 SQL/服务，Microsoft 驱动程序，它可能返回中的以下值**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 驱动程序中发生错误，因为它添加前缀到诊断消息 ([Microsoft]) 的供应商和驱动程序 （[ODBC Rdb 驱动程序]）。  
  
 如果 DBMS 找不到表员工，驱动程序可能会设置格式，并返回中的以下值**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 由于数据源中发生错误，该驱动程序将添加到诊断消息的数据源标识符 ([Rdb]) 的前缀。 由于该驱动程序 interfaced 与数据源的组件，但它会将其供应商 ([Microsoft]) 和标识符 （[ODBC Rdb 驱动程序]） 的前缀添加到诊断消息。