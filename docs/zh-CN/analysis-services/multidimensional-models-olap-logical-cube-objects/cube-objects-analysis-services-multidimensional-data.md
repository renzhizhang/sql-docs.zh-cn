---
title: 多维数据集对象 (Analysis Services-多维数据) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5e670318a298cd49c8c03538093f8739c5f601c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>多维数据集对象（Analysis Services - 多维数据）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
    
## <a name="introducing-cube-objects"></a>多维数据集对象介绍  
 简单 <xref:Microsoft.AnalysisServices.Cube> 对象由基本信息、维度和度量值组组成。 基本信息包括多维数据集的名称、多维数据集的默认度量值、数据源和存储模式等。  
  
 维度集合包含在数据库维度集合的多维数据集中使用的实际维度集。 所有维度都必须先在数据库的维度集合中定义，然后才能在多维数据集中引用。 专用维度中均不提供[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 度量值组是多维数据集中的度量值集。 度量值组是具有常见数据源视图和维度集的度量值的集合。 度量值组是度量值的处理单元；可先对度量值组进行单独处理，然后再浏览。  
  
## <a name="in-this-section"></a>在本节中  
  
|||  
|-|-|  
|主题||  
|[操作 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[聚合和聚合设计](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)||  
|[计算](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)||  
|[多维数据集单元 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-cells-analysis-services-multidimensional-data.md)||  
|[多维数据集属性 - 多维模型编程](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-properties-multidimensional-model-programming.md)||  
|[多维数据集存储 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)||  
|[多维数据集翻译](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)||  
|[维度关系](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)||  
|[关键绩效指标 & #40;Kpi & #41;多维模型中](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[度量值和度量值组](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)||  
|[分区 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)||  
|[透视](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md)||  
  
  