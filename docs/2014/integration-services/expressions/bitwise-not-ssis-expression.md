---
title: ~（位非）（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73a67105a8b70b1b55b15d894ebc13c90417d8e5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387155"
---
# <a name="-bitwise-not-ssis-expression"></a>~ （位非）（SSIS 表达式）
  对整数执行位求反运算。 此运算符可应用于有符号和无符号整数数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>参数  
 *integer_expression*  
 整数数据类型的任何有效表达式。 integer_expression 是一个整数，该整数转换为二进制数以进行位运算。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>结果类型  
 返回 integer_expression 数据类型。  
  
## <a name="remarks"></a>备注  
 None  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例对数值 170 (0000 0000 1010 1010) 执行位 ~（非）运算。 该数值是一个有符号整数。  
  
```  
  
~ 170  
```  
  
 表达式的计算结果为 -170 (1111111101010101)。  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>请参阅  
 [运算符优先级和结合性](operator-precedence-and-associativity.md)   
 [运算符（SSIS 表达式）](operators-ssis-expression.md)  
  
  
