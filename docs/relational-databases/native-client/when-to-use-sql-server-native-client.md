---
title: "何时使用 SQL Server Native Client |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8acbbdc6247628aee18efd8e10ed783b455270fe
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="when-to-use-sql-server-native-client"></a>何时使用 SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 是可用于访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据的一种技术。  有关不同的数据访问技术的讨论，请参阅[数据访问技术路线图](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 在决定是否使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 作为应用程序的数据访问技术时，应当考虑多种因素。  
  
 对于新的应用程序，如果使用的是托管编程语言，如 Microsoft Visual C# 或 Visual Basic，且需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的新功能，那么应当使用用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 .NET Framework 数据访问接口，该接口是用于 .NET Framework 的一部分。  
  
 如果要开发基于 COM 的应用程序，且需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的新功能，则应当使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。 如果不需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能，则可以继续使用 Windows 数据访问组件 (WDAC)。  
  
 对于现有的 OLE DB 和 ODBC 应用程序，主要问题在于是否需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能。 如果已有不需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能的成熟应用程序，那么可以继续使用 WDAC。 但是，如果你需要访问这些新功能，例如[xml 数据类型](../../t-sql/xml/xml-transact-sql.md)，应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 和 MDAC 都支持使用行版本控制的已提交读事务隔离，但只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 支持快照事务隔离。 （在编程术语中，使用行版本控制的读取已提交的事务隔离是 Read Committed 事务相同。）  
  
 有关之间的差异信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端和 MDAC，请参阅[更新到 SQL Server Native Client 应用程序从 MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 编程](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC 操作指南主题](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 操作指南主题](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  