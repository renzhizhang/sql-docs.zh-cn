---
title: MSSQL_ENG020574 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG02574 error
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4788e7696b9bb986ab5a16fb2fea618d0b996cc9
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133587"
---
# <a name="mssqleng020574"></a>MSSQL_ENG020574
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20574|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|订阅服务器“%s”对发布“%s”中项目“%s”的订阅未通过数据验证。|  
  
## <a name="explanation"></a>解释  
 根据发布服务器上的数据对订阅服务器上的数据进行验证，数据不匹配；因此验证失败。 有关验证的详细信息，请参阅 [Validate Replicated Data](validate-data-at-the-subscriber.md)。  
  
## <a name="user-action"></a>用户操作  
 建议您进行以下操作：  
  
-   确定验证失败的原因。  
  
-   更正导致失败的基本问题。  
  
-   通过重新初始化订阅或其他方法收敛数据。  
  
## <a name="see-also"></a>请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
