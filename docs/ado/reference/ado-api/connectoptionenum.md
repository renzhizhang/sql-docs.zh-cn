---
title: ConnectOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9df3fd695e9bf281133dabf436e5e8b5de7e0b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646615"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
指定是否[开放](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)（同步） 建立连接之后或之前，应返回对象 （异步）。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|以异步方式打开的连接。 [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)事件可用于确定连接可用。|  
|**adConnectUnspecified**|-1|默认值。 以同步方式打开的连接。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>适用范围  
 [Open 方法（ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)
