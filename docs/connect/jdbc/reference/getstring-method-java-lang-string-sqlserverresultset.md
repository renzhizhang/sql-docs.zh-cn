---
title: getString 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a98c8a8-61d0-40c9-9335-25a87b732dc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a153811c723875da51e747a4d9cff24a57ace75
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642885"
---
# <a name="getstring-method-javalangstring-sqlserverresultset"></a>getString 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称作为 Java 编程语言中的字符串的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getString(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串。  
  
## <a name="return-value"></a>返回值  
 一个字符串值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getString方法是由 java.sql.ResultSet 接口中的 getString 方法指定的。  
  
 SQL Server 中的所有列都可作为字符串返回。 这意味着可以返回基于数字和基于字符的所有类型的字符串表示形式，以及二进制列的十六进制字符串表示形式，例如 binary、varbinary、varbinary(max)、image、timestamp 和 uniqueidentifier。  
  
 位置敏感类型（如 money、smallmoney, datetime、smalldatetime、float、real、decimal 和 numeric）将返回基本类型值的规范 toString() 格式。  
  
 用户定义类型将作为十六进制字符串值返回。  
  
## <a name="see-also"></a>另请参阅  
 [getString 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
