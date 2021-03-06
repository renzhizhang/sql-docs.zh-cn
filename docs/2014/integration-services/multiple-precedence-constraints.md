---
title: 多个优先约束 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5f06a05ff275151e2488b1f3ec89c8d9cb7afb12
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375585"
---
# <a name="multiple-precedence-constraints"></a>多个优先约束
  一个优先约束连接两个可执行文件：两个任务、两个容器或一个任务和一个容器。 它们被称为优先可执行文件和受约束的可执行文件。 受约束的可执行文件可具有多个优先约束。 有关详细信息，请参阅 [Precedence Constraints](control-flow/precedence-constraints.md)。  
  
 对约束进行分组以组合成复杂的约束方案，可使您在包中实现复杂的控制流。 例如，在下图中，一个 `Success` 约束将任务 D 链接到任务 A，一个 `Failure` 约束将任务 D 链接到任务 B，而一个 `Success` 约束将任务 D 链接到任务 C。 任务 D 和任务 A 之间、任务 D 和任务 B 之间，以及任务 D 和任务 C 之间的优先约束参与逻辑与  关系。 因此，任务 A 必须运行成功，任务 B 必须失败，并且任务 C 必须运行成功才能运行任务 D。  
  
 ![按优先约束链接的任务](media/precedenceconstraints.gif "Tasks linked by precedence constraints")  
  
## <a name="logicaland-property"></a>LogicalAnd 属性  
 如果任务或容器具有多个约束，则 `LogicalAnd` 属性指定一个优先约束是单独计算还是与其他约束一起计算。  
  
 可以设置`LogicalAnd`属性使用**优先约束编辑器**中[!INCLUDE[ssIS](../includes/ssis-md.md)]设计器中，或在属性窗口中的[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]提供。  
  
## <a name="related-tasks"></a>Related Tasks  
 [设置优先约束的属性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
