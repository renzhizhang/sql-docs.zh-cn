---
title: 常规连接与上下文连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f4810a7a7d117c498ce74dbe978716900b25d19f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516783"
---
# <a name="context-connections-vs-regular-connections"></a>上下文连接与常规连接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果要连接到远程服务器，请始终使用常规连接，而不使用上下文连接。 如果您需要连接到存储过程或函数正在其上运行的同一台服务器，则在大多数情况下请使用上下文连接。 这具有一些优势，例如，在同一个事务空间中运行以及不必重新验证。  
  
 此外，使用上下文连接通常会导致性能更佳和占用更少的资源。 上下文连接是过程仅在建立连接后，因此它可以与服务器联系"直接"通过跳过网络协议和传输层发送 TRANSACT-SQL 语句和接收结果。 同时跳过验证过程。 下图显示的主要组成部分**SqlClient**托管提供程序，以及不同组件时使用常规连接和使用上下文连接时相互的交互。  
  
 ![上下文和常规连接代码路径。](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "代码的上下文和常规连接的路径。")  
  
 上下文连接所采用的代码路径较短，且所涉及的组件较少，因此，您可以预计请求到达服务器和从服务器获得结果的速度将高于采用常规连接时。 服务器上的查询执行时间对于上下文连接和常规连接是相同的。  
  
 在某些情况下，您可能需要与同一台服务器之间建立单独的常规连接。 例如，有一定限制在使用中所述的上下文连接[限制对常规连接和上下文连接](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)。  
  
## <a name="see-also"></a>请参阅  
 [上下文连接](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
