---
title: 从饼图顶部开始绘制饼图值（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 74eb4008ad9de17c8da8ced5f70d9eba4b0a85a9
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291545"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>从饼图顶部开始绘制饼图值（报表生成器和 SSRS）
  默认情况下，在饼图中，数据集中的第一个值从与饼顶部成 90 度的位置开始绘制。 您可能希望从顶部开始绘制第一个值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>从饼顶部开始绘制饼图  
  
1.  单击饼图本身。  
  
2.  如果 **“属性”** 窗格未打开，请单击 **“视图”** 选项卡上的 **“属性”**。  
  
3.  在 **“属性”** 窗格中，在 **“自定义属性”** 下，将 **PieStartAngle** 从 **0** 更改为 **270**。  
  
4.  单击 **“运行”** 以预览报表。  
  
 第一个值现在将从饼图顶部开始绘制。  
  
## <a name="see-also"></a>请参阅  
 [设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)   
 [饼图&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
