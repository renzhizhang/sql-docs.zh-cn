---
title: 字符串填充 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 069fa1deababf347d7c45b62952960f7535115bf
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393800"
---
# <a name="string-padding-ssis"></a>字符串填充 (SSIS)
  表达式计算器不检查字符串是否包含前导空格和尾随空格，并且比较前不填充字符串来使其具有相同长度。 如果表达式需要字符串填充，可使用 + 运算符连接列值和空字符串。 有关详细信息，请参阅 [+（连接）（SSIS 表达式）](concatenate-ssis-expression.md)。  
  
 另一方面，如果要删除空格，表达式计算器提供了 LTRIM、RTRIM 和 TRIM 函数，用于删除前导空格和/或尾随空格。 有关详细信息，请参阅 [LTRIM（SSIS 表达式）](trim-ssis-expression.md)、[RTRIM（SSIS 表达式）](rtrim-ssis-expression.md)和 [TRIM（SSIS 表达式）](trim-ssis-expression.md)。  
  
> [!NOTE]  
>  LEN 函数将前导空格和尾随空格包含在其计数中。  
  
## <a name="related-content"></a>相关内容  
 pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](https://go.microsoft.com/fwlink/?LinkId=217683)。  
  
  
