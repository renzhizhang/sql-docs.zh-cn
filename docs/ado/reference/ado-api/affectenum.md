---
title: AffectEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf8f067cd223bb9064e5e44734b9765cc8b41c79
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129467"
---
# <a name="affectenum"></a>AffectEnum
指定的操作会影响哪些记录。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|如果不存在[筛选器](../../../ado/reference/ado-api/filter-property.md)应用于**记录集**，影响所有记录。<br /><br /> 如果**筛选器**属性设置为字符串条件 (如"作者 = Smith")，则该操作会影响当前的一章中可见的记录。<br /><br /> 如果**筛选器**属性设置为的成员[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)或数组的书签，则该操作将影响的所有行**记录集**。 **注意： adAffectAll**隐藏在 Visual Basic 对象浏览器中。|  
|**adAffectAllChapters**|4|影响所有记录中的所有同级章节**记录集**，包括那些通过任何不可见**筛选器**当前应用。|  
|**adAffectCurrent**|1|会影响仅当前记录。|  
|**adAffectGroup**|2|影响满足当前的记录[筛选器](../../../ado/reference/ado-api/filter-property.md)属性设置。 必须设置**筛选器**属性设置为**FilterGroupEnum**值或数组**书签**要使用此选项。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Affect.ALL|  
|AdoEnums.Affect.ALLCHAPTERS|  
|AdoEnums.Affect.CURRENT|  
|AdoEnums.Affect.GROUP|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|[Delete 方法（ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|  
|[重新同步方法](../../../ado/reference/ado-api/resync-method.md)|[UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)|
