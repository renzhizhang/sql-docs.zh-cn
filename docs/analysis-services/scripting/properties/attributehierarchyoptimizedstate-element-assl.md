---
title: "AttributeHierarchyOptimizedState 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AttributeHierarchyOptimizedState Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributeHierarchyOptimizedState
helpviewer_keywords:
- AttributeHierarchyOptimizedState element
ms.assetid: d87148c8-2011-45ae-94c3-851f48babc5f
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79b7f84f96c9921a0d1fafce4bc0c8604b5fd582
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="attributehierarchyoptimizedstate-element-assl"></a>AttributeHierarchyOptimizedState 元素 (ASSL)
  确定应用于属性层次结构的优化级别。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute -->  
   ...  
   <AttributeHierarchyOptimizedState>...  
   </AttributeHierarchyOptimizedState>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*FullyOptimized*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*FullyOptimized*|实例为属性层次结构生成索引以提高查询性能。|  
|*NotOptimized*|实例未生成其他索引。|  
  
 对应的允许值为枚举**AttributeHierarchyOptimizedState**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.OptimizationType>。 对应的父级的元素**AttributeHierarchyOptimizedState** AMO 对象模型中是<xref:Microsoft.AnalysisServices.CubeAttribute>和<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  