---
title: "STIntersection (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection (geometry Data Type)
ms.assetid: 354843f5-cc14-478c-974a-04f363f9530f
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: accdd0fe059521ec45beeb386db6bfa34e66ccc0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stintersection-geometry-data-type"></a>STIntersection（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回一个对象，表示点其中**几何图形**实例与另一个相交**几何图形**实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.STIntersection ( other_geometry )  
```  
  
## <a name="arguments"></a>参数  
 *other_geometry*  
 是另一种**几何图形**实例进行比较的实例上的`STIntersection()`从中调用，以确定它们的相交处。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="remarks"></a>注释  
 `STIntersection()`始终返回 null 如果的空间引用 Id 为 (Srid)**几何图形**实例不匹配。 只有在输入实例包含它们时，结果才可能包含圆弧段。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-stintersection-on-polygon-instances"></a>A. 对 Polygon 实例使用 STIntersection()  
 下面的示例使用 `STIntersection()` 计算两个多边形的交点。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-using-stintersection-with-curvepolygon-instance"></a>B. 对 CurvePolygon 实例使用 STIntersection()  
 以下示例返回一个包含圆弧线段的实例。  
  
 `DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';`  
  
 `DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';`  
  
 `SELECT @h.STIntersection(@g).ToString();`  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

