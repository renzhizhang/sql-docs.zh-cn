---
title: setApplicationName 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3853262dd5e1a62542387e9b61f8c30f5967f09b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210586"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>setApplicationName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置应用程序名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *applicationName*  
  
 包含应用程序名称的一个字符串。  
  
## <a name="remarks"></a>Remarks  
 此应用程序名称用于在各种 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析和日志记录工具中标识特定的应用程序。 如果未设置应用程序名称，getApplicationName 方法则将返回未本地化的字符串“[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
