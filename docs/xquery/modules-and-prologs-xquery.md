---
title: "模块和起始 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2253aae6b19fcede1465ba6d0cef5b479f5be8af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="modules-and-prologs-xquery"></a>模块和 Prolog (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)是一系列的命名空间声明。 在 Prolog 中使用声明命名空间时，可以为命名空间绑定指定前缀并在查询正文中使用该前缀。  
  
## <a name="implementation-limitations"></a>实现限制  
 在此实现中，不支持下列 XQuery 规范：  
  
-   模块声明 (`version`)  
  
-   模块声明 (`module namespace`)  
  
-   Xmpspacedeclaration (`xmlspace`)  
  
-   默认排序规则声明 (`declare default collation`)  
  
-   基准 URI 声明 (`declare base-uri`)  
  
-   构造声明 (`declare construction`)  
  
-   默认排序声明 (`declare ordering`)  
  
-   架构导入 (`import schema namespace`)  
  
-   模块导入 (`import module`)  
  
-   Prolog 中的变量声明 (`declare variable`)  
  
-   函数声明 (`declare function`)  
  
## <a name="in-this-section"></a>本节内容  
 [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)  
 介绍 XQuery Prolog。  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)  
  
  