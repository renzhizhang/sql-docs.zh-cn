---
title: LinRegR2 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 42c703e703e8c557b4de8466a0cd1b686217fd4b
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742056"
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)


  计算对一组进行线性回归，并返回确定，R 系数<sup>2</sup>。  
  
## <a name="syntax"></a>语法  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression_y*  
 返回表示 Y 轴值的数字的有效数值表达式，通常是单元坐标的多维表达式 (MDX)。  
  
 *Numeric_Expression_x*  
 通常是单元坐标（返回代表 X 轴的值的数字）的多维表达式 (MDX) 的有效数值表达式。  
  
## <a name="remarks"></a>Remarks  
 线性回归使用最小二乘法，可以计算出回归线（即一系列点的最佳拟合线）的公式。 回归行都有以下公式，其中是斜率，b 是截距：  
  
 y = ax+b  
  
 **LinRegR2**函数的计算结果指定的 setagainst 第一个数值 expressionto 获取 y 轴的值。 然后，该函数对指定集计算第二个数值表达式（如果指定）的值，以获得 X 轴的值。 如果未指定第二个数值 expressionis，该功能将用作值具有 x 轴中指定集的单元格的当前上下文。 不指定 x axisargument 经常用于在时间维度。  
  
 获取组点之后, **LinRegR2**函数将返回统计 R<sup>2</sup>描述最适合的线性方程式与点状态。  
  
> [!NOTE]  
>  **LinRegR2**函数将忽略空单元格包含文本或逻辑值。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下面的示例返回统计 R<sup>2</sup>描述拟合度到单位销售额和销售的应用商店的度量值的点的线性回归公式的好坏。  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
