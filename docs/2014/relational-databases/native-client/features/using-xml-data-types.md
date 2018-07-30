---
title: 使用 XML 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [SQL Server Native Client], xml data type
- SQL Server Native Client OLE DB schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- SQL Server Native Client OLE DB interfaces
- XML [SQL Server], SQL Server Native Client
- COLUMNS rowset
ms.assetid: a7af5b72-c5c2-418d-a636-ae4ac6270ee5
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5db3626a0e2eba0154e565907d9ca9a888453925
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417037"
---
# <a name="using-xml-data-types"></a>使用 XML 数据类型
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入**xml**使用户可以存储 XML 文档和片段中的数据类型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。 **Xml**数据类型是中的内置数据类型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，并且在某些方面类似于其他内置类型，如**int**并**varchar**。 您可以使用其他内置类型**xml**数据类型作为列类型创建表时，在作为变量类型、 参数类型或函数返回类型; 或在 CAST 和 CONVERT 函数。  
  
## <a name="programming-considerations"></a>编程时的注意事项  
 XML 可以是自描述的，即可以根据需要包含一个 XML 标头来指定文档的编码，例如：  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 XML 标准描述 XML 处理器如何通过检查文档的前若干个字节来检测用于文档的编码。 有时，应用程序指定的编码可能与文档指定的编码相冲突。 对于作为绑定参数传递的文档，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将 XML 视为二进制数据，因此不执行转换，并且 XML 分析器可以使用在文档内指定的编码而不会出现问题。 然而，对于绑定为 WSTR 的 XML 数据，应用程序必须确保将文档编码为 Unicode。 这可能需要将文件加载到 DOM 中，同时将编码更改为 Unicode 并对文档进行序列化。 否则，可能发生数据转换，而导致 XML 无效或损坏。  
  
 当在文字中指定 XML 时，也可能发生冲突。 例如，下面的内容无效：  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 访问接口  
 DBTYPE_XML 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口中特定于 XML 的新数据类型。 此外，可以通过现有的 OLE DB 类型（DBTYPE_BYTES、DBTYPE_WSTR、DBTYPE_BSTR、DBTYPE_XML、DBTYPE_STR、DBTYPE_VARIANT 和 DBTYPE_IUNKNOWN）访问 XML 数据。 可以从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口行集的列中按以下格式检索存储在类型为 XML 的列中的数据：  
  
-   文本字符串  
  
-   **ISequentialStream**  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不包括 SAX 读取器，但**ISequentialStream**可以轻松地传递到 SAX 和 DOM MSXML 中的对象。  
  
 **ISequentialStream**应该是用于检索大型 XML 文档。 用于其他大值类型的相同技术也适用于 XML。 有关详细信息，请参阅[使用大值类型](using-large-value-types.md)。  
  
 也可以检索行集中的 XML，类型的列中存储的数据插入或更新应用程序通过常见接口如**irow:: Getcolumns**， **irowchange:: Setcolumns**，并且**Icommand:: Execute**。 同样与检索情况中，应用程序可以传递文本字符串或**ISequentialStream**到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。  
  
> [!NOTE]  
>  以字符串格式通过发送 XML 数据**ISequentialStream**接口，你必须获取**ISequentialStream**通过指定 DBTYPE_IUNKNOWN 并设置其*pObject*为 null 的绑定中的参数。  
  
 当由于使用者缓冲区过小而导致已检索的 XML 数据被截断时，长度可能作为 0xffffffff 返回，这意味着长度为未知的。 这与将它实现为针对客户端进行流处理的数据类型而未在发送实际数据之前发送长度信息是一致的。 在某些情况下的实际长度时，可能会返回访问接口已缓冲了整个值，如**irowset:: Getdata**并执行数据转换。  
  
 服务器会将发送到 SQL Server 的 XML 数据视为二进制数据。 这可防止发生任何转换并允许 XML 分析器自动检测 XML 编码。 这样，就可以接受更广泛的 XML 文档（例如，以 UTF-8 编码的文档）作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的输入。  
  
 如果将输入 XML 绑定为 DBTYPE_WSTR，则应用程序必须确保已对其进行 Unicode 编码，以避免由于不必要的数据转换而可能导致损坏。  
  
### <a name="data-bindings-and-coercions"></a>数据绑定和强制  
 下表介绍的绑定和强制使用列出的数据类型与时发生[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **xml**数据类型。  
  
|数据类型|到服务器<br /><br /> **XML**|到服务器<br /><br /> **非 XML**|从服务器<br /><br /> **XML**|从服务器<br /><br /> **非 XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|通过传递<sup>6，7</sup>|错误<sup>1</sup>|确定<sup>11，6</sup>|错误<sup>8</sup>|  
|DBTYPE_BYTES|通过传递<sup>6，7</sup>|N/A<sup>2</sup>|确定<sup>11，6</sup>|N/A <sup>2</sup>|  
|DBTYPE_WSTR|通过传递<sup>6，10</sup>|N/A <sup>2</sup>|确定<sup>4、 6、 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_BSTR|通过传递<sup>6，10</sup>|N/A <sup>2</sup>|确定<sup>3</sup>|N/A <sup>2</sup>|  
|DBTYPE_STR|确定<sup>6，9，10</sup>|N/A <sup>2</sup>|确定<sup>5、 6、 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_IUNKNOWN|字节流，通过**ISequentialStream**<sup>7</sup>|N/A <sup>2</sup>|字节流，通过**ISequentialStream**<sup>11</sup>|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &AMP;#124; VT_ARRAY)|通过传递<sup>6，7</sup>|N/A <sup>2</sup>|N/A|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|通过传递<sup>6，10</sup>|N/A <sup>2</sup>|确定<sup>3</sup>|N/A <sup>2</sup>|  
  
 <sup>1</sup>如果的服务器类型不是使用指定 DBTYPE_XML **icommandwithparameters:: Setparameterinfo**取值函数类型为 DBTYPE_XML，执行该语句时出错 (DB_E_ERRORSOCCURRED，参数状态为 DBSTATUS_E_BADACCESSOR）;否则将数据发送到服务器，但服务器返回一个错误，指出没有从 XML 到参数的数据类型的隐式转换。  
  
 <sup>2</sup>超出了本主题的范围。  
  
 <sup>3</sup>格式为 utf-16，无字节顺序标记 (BOM)，无编码规格，无空终止。  
  
 <sup>4</sup>格式为 utf-16，没有 BOM，无编码规格，空终止。  
  
 <sup>5</sup>格式为编码的带有空终止符的客户端代码页中的多字节字符。 从服务器提供的 Unicode 进行转换可能导致数据损坏，因此，强烈建议不要使用此绑定。  
  
 <sup>6</sup>可能会使用 BY_REF。  
  
 <sup>7</sup>utf-16 数据必须以 BOM 开头。 否则，服务器可能无法正确地识别编码。  
  
 <sup>8</sup>创建取值函数时或在提取时，会在发生验证。 此错误为 DB_E_ERRORSOCCURRED，绑定状态设置为 DBBINDSTATUS_UNSUPPORTEDCONVERSION。  
  
 <sup>9</sup>数据转换为 Unicode 在发送到服务器之前，使用客户端代码页。 如果文档编码与客户端代码页不匹配，则这可能导致数据损坏，因此强烈建议不要使用此绑定。  
  
 <sup>10</sup>物料清单始终添加到数据发送到服务器。 如果数据已经以一个 BOM 开始，则这可能导致在缓冲区的开头具有两个 BOM。 服务器使用第一个 BOM 将编码识别为 utf-16，然后将其丢弃。 第二个 BOM 将被解释为零宽度不间断空格字符。  
  
 <sup>11</sup>格式为 utf-16，无编码规格，从服务器收到的数据添加一个 BOM。 如果服务器返回一个空字符串，则 BOM 仍会返回到应用程序。 如果缓冲区长度的字节数为奇数，会正确地截断数据。 如果在块中返回整个值，则它们可以连接来重建正确的值。  
  
 <sup>12</sup>如果缓冲区长度小于两个字符-是的没有足够的空间用于空终止-报告溢出错误。  
  
> [!NOTE]  
>  对于 NULL XML 值，不返回值。  
  
 XML 标准要求 UTF-16 编码的 XML，以便以字节顺序标记 (BOM) UTF-16 字符代码 0xFEFF 开头。 当使用 WSTR 和 BSTR 绑定时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 不要求或添加 BOM，因为编码为隐式绑定。 当使用 BYTES、XML 或 IUNKNOWN 绑定时，目的是为了在处理其他 XML 处理器和存储系统时提供简便性。 在此情况下，应向 UTF-16 编码的 XML 提供 BOM，并且应用程序无需关心实际编码，因为绝大多数的 XML 处理器（包括 SQL Server）会通过检查该值的前几个字节推导出编码。 从收到的 XML 数据[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端使用 BYTES、 XML 或 IUNKNOWN 绑定始终编码以 utf-16 具有 BOM 但没有嵌入式编码声明。  
  
 OLE DB 核心服务提供的数据转换 (**IDataConvert**) 不适用于 DBTYPE_XML。  
  
 当向服务器发送数据时将执行验证。 应由应用程序处理客户端验证和编码更改，强烈建议您不要直接处理 XML 数据，而应使用 DOM 或 SAX 读取器来处理此数据。  
  
 可以绑定 DBTYPE_NULL 和 DBTYPE_EMPTY，用于输入参数而不是输出参数或结果。 当将它们绑定用于输入参数时，状态必须设置为 DBSTATUS_S_ISNULL 或 DBSTATUS_S_DEFAULT。  
  
 可以将 DBTYPE_XML 转换为 DBTYPE_EMPTY 和 DBTYPE_NULL，并可以将 DBTYPE_EMPTY 转换为 DBTYPE_XML，但无法将 DBTYPE_NULL 转换为 DBTYPE_XML。 这与 DBTYPE_WSTR 相一致。  
  
 DBTYPE_IUNKNOWN 是支持的绑定（如上表中所示），但在 DBTYPE_XML 与 DBTYPE_IUNKNOWN 之间不存在转换。 DBTYPE_IUNKNOWN 不能与 DBTYPE_BYREF 一起使用。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 行集的添加和更改内容  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端添加了新值，或将更改为许多核心 OLE DB 架构行集。  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>COLUMNS 和 PROCEDURE_PARAMETERS 架构行集  
 COLUMNS 和 PROCEDURE_PARAMETERS 架构行集添加了以下列。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|在其中定义 XML 架构集合的目录的名称。 对于非 XML 列或非类型化 XML 列，为 NULL。|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|在其中定义 XML 架构集合的架构的名称。 对于非 XML 列或非类型化 XML 列，为 NULL。|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 架构集合的名称。 对于非 XML 列或非类型化 XML 列，为 NULL。|  
  
#### <a name="the-providertypes-schema-rowset"></a>PROVIDER_TYPES 架构行集  
 在 PROVIDER_TYPES 架构行集，COLUMN_SIZE 值为 0 **xml**数据类型，并且 DATA_TYPE 为 DBTYPE_XML。  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>SS_XMLSCHEMA 架构行集  
 所引入的新的架构行集 SS_XMLSCHEMA 可供客户端检索 XML 架构信息。 SS_XMLSCHEMA 行集包含以下列。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 集合所属的目录。|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 集合所属的架构。|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 架构集合的类型化 XML 列，否则为 NULL 的名称。|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|XML 架构的目标命名空间。|  
|SCHEMACONTENT|DBTYPE_WSTR|XML 架构内容。|  
  
 每个 XML 架构都按目录名称、架构名称、架构集合名称和目标命名空间统一资源标识符 (URI) 限定范围。 此外，还定义了新的 GUID，其名称为 DBSCHEMA_XML_COLLECTIONS。 SS_XMLSCHEMA 架构行集的限制数和受限列定义如下。  
  
|GUID|限制数|受限列|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB 属性集的添加和更改内容  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端添加了新值或更改为许多核心 OLE DB 属性集。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 属性集  
 为了支持**xml**通过 OLE DB 数据类型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 实现新的 DBPROPSET_SQLSERVERPARAMETER 属性集，其中包含以下值。  
  
|“属性”|类型|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|在其中定义 XML 架构集合的目录（数据库）的名称。 SQL 三部分组成的名称标识符的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|架构集合内 XML 架构的名称。 由三部分组成的 SQL 名称标识符的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|目录内 XML 架构集合的名称。由三部分组成的 SQL 名称标识符的一部分。|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 属性集  
 若要支持中的表创建**ITableDefinition**接口， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 向 DBPROPSET_SQLSERVERCOLUMN 属性集添加三个新列。  
  
|“属性”|类型|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|对于类型化 XML 列，此属性是一个字符串，它指定在其中存储 XML 架构的目录的名称。 对于其他列类型，此属性返回空字符串。|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|对于类型化 XML 列，此属性是一个字符串，它指定定义此列的 XML 架构的名称。|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|对于类型化 XML 列，此属性是一个字符串，它指定定义此值的 XML 架构集合的名称。|  
  
 与 SSPROP_PARAM 值类似，所有这些属性都是可选的且默认值为空。 仅当指定 SSPROP_COL_XML_SCHEMACOLLECTIONNAME 时，才能指定 SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME 和 SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME。 在将 XML 传递到服务器时，如果包含这些值，则将针对当前数据库检查它们是否存在（有效性），并且针对架构检查实例数据。 在所有情况下，要使这些值有效，它们必须全部为空或全部添入这些值。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 接口的添加和更改内容  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端添加了新值，或将更改为许多核心 OLE DB 接口。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 接口  
 为了支持**xml**通过 OLE DB 数据类型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 实现了许多的更改包括添加[ISSCommandWithParameters](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)接口。 此新接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了三个方法继承自**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，并**SetParameterInfo**;**ISSCommandWithParameters**提供[GetParameterProperties](../../native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)并[SetParameterProperties](../../native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)用于处理特定于服务器的方法数据类型。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**接口，还可使用新的 SSPARAMPROPS 结构。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 接口  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端中添加以下[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-返回的行集的特定列**icolumnrowset:: Getcolumnsrowset**方法。 这些列包含 XML 架构集合的由三个部分组成的名称。 对于非 XML 列或非类型化 XML 列，所有这三列均取默认值 NULL。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 架构集合所属的目录，<br /><br /> 否则为 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 架构集合所属的架构。 否则为 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|类型化 XML 列的 XML 架构集合的名称，否则为 NULL。|  
  
#### <a name="the-irowset-interface"></a>IRowset 接口  
 通过检索 XML 列中的 XML 实例**irowset:: Getdata**方法。 根据由客户端指定的绑定，可以将 XML 实例作为 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML、DBTYPE_STR、DBTYPE_BYTES 进行检索，或者通过 DBTYPE_IUNKNOWN 将其作为接口检索。 如果使用者指定 DBTYPE_BSTR、DBTYPE_WSTR 或 DBTYPE_VARIANT，则访问接口将 XML 实例转换为用户请求的类型，并将其放入在相应绑定中指定的位置。  
  
 如果使用者指定 DBTYPE_IUNKNOWN 并设置*pObject*参数为 NULL，或者集*pObject*自变量为 IID_ISequentialStream，提供程序返回**ISequentialStream**接口向使用者，以便使用者可以流式传输列之外的 XML 数据。 **ISequentialStream**然后返回将 XML 数据作为 Unicode 字符流。  
  
 当返回与 DBTYPE_IUNKNOWN 绑定的 XML 值时，访问接口将报告 `sizeof (IUnknown *)` 的大小值。 请注意，这与在将某列绑定为 DBTYPE_IUnknown 或 DBTYPE_IDISPATCH 时所采取的方法相一致；当无法确定实际列大小时，将返回 DBTYPE_IUNKNOWN/ISequentialStream。  
  
#### <a name="the-irowsetchange-interface"></a>IRowsetChange 接口  
 使用者可以通过两种方法更新列中的 XML 实例。 第一种方法是通过存储对象**ISequentialStream**提供程序创建。 使用者可以调用**isequentialstream:: Write**方法来直接更新提供程序返回的 XML 实例。  
  
 第二种方法是通过**irowsetchange:: Setdata**或**irowsetchange:: Insertrow**方法。 通过这一方法，可以在类型为 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML 或 DBTYPE_IUNKNOWN 的绑定中指定使用者缓冲区内的 XML 实例。  
  
 对于 DBTYPE_BSTR、DBTYPE_WSTR 或 DBTYPE_VARIANT，访问接口将位于使用者缓冲区中的 XML 实例存储到适当的列中。  
  
 对于 DBTYPE_IUNKNOWN/ISequentialStream，如果使用者未指定任何存储对象，使用者必须创建**ISequentialStream**提前对象、 将 XML 文档对象时，绑定，然后传递的对象通过提供程序**irowsetchange:: Setdata**方法。 使用者还可以创建一个存储对象，将 pObject 参数设置为 IID_ISequentialStream，创建**ISequentialStream**对象，然后将传递**ISequentialStream**对象**Irowsetchange:: Setdata**方法。 在这两种情况下，该提供程序可以检索通过 XML 对象**ISequentialStream**对象，并将其插入到适当的列。  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate 接口  
 **IRowsetUpdate**接口提供了用于延迟更新的功能。 行集提供的数据不会提供对其他事务直到使用者可调用**IRowsetUpdate:Update**方法。  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind 接口  
 **Irowsetfind:: Findnextrow**方法并不适用于**xml**数据类型。 当**irowsetfind:: Findnextrow**称为和*hAccessor* DBTYPE_XML 的列指定的参数，则返回 DB_E_BADBINDINFO。 此时不考虑正在搜索的列的类型。 对于任何其他绑定类型， **FindNextRow**如果要在其中搜索的列的失败并返回 DB_E_BADCOMPAREOP **xml**数据类型。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驱动程序  
 在中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序的大量更改已对各种功能来支持**xml**数据类型。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)函数具有三个新的字段标识符，包括 SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME、 SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME 和 SQL_CA_SS _XML_SCHEMACOLLECTION_NAME。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序为 SQL_DESC_DISPLAY_SIZE 和 SQL_DESC_LENGTH 列报告 SQL_SS_LENGTH_UNLIMITED。  
  
### <a name="sqlcolumns"></a>SQLColumns  
 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)函数具有三个新列，包括 SS_XML_SCHEMACOLLECTION_CATALOG_NAME、 SS_XML_SCHEMACOLLECTION_SCHEMA_NAME 和 SS_XML_SCHEMACOLLECTION_NAME。 现有的 TYPE_NAME 列用于指示 XML 类型的名称，而 XML 类型列或参数的 DATA_TYPE 为 SQL_SS_XML。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序对于 COLUMN_SIZE 和 CHAR_OCTET_LENGTH 值报告 SQL_SS_LENGTH_UNLIMITED。  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序报告 SQL_SS_LENGTH_UNLIMITED，当不能在确定列大[SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md)函数。  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序有关的最大 column_size 报告 SQL_SS_LENGTH_UNLIMITED **xml**中的数据类型[SQLGetTypeInfo](../../native-client-odbc-api/sqlgettypeinfo.md)函数。  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 [SQLProcedureColumns](../../native-client-odbc-api/sqlprocedurecolumns.md)函数具有相同的列添加为**SQLColumns**函数。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序有关的最大 column_size 报告 SQL_SS_LENGTH_UNLIMITED **xml**数据类型。  
  
### <a name="supported-conversions"></a>支持的转换  
 当从 SQL 转换为 C 数据类型时，SQL_C_WCHAR、SQL_C_BINARY 和 SQL_C_CHAR 可全部转换为 SQL_SS_XML，但必须符合以下规定：  
  
-   SQL_C_WCHAR：格式为 UTF-16，无字节顺序标记 (BOM)，无空终止。  
  
-   SQL_C_BINARY：格式为 UTF-16，无空终止。 向从服务器接收的数据添加一个 BOM。 如果服务器返回了空字符串，则仍然将 BOM 返回给应用程序。 如果缓冲区长度的字节数为奇数，则会正确地截断数据。 如果分块区返回了整个值，则可以将它们连接起来以重新构建正确的值。  
  
-   SQL_C_CHAR：格式为在客户端代码页中编码的带有空终止的多字节字符。 从服务器提供的 UTF-16 进行转换可能导致数据损坏，因此，强烈建议不要使用此绑定。  
  
 当从 C 转换为 SQL 数据类型时，SQL_C_WCHAR、SQL_C_BINARY 和 SQL_C_CHAR 可全部转换为 SQL_SS_XML，但必须符合以下规定：  
  
-   SQL_C_WCHAR：始终向发送到服务器的数据添加一个 BOM。 如果数据已经以一个 BOM 开始，则这可能导致在缓冲区的开头具有两个 BOM。 服务器使用第一个 BOM 将编码识别为 UTF-16，然后放弃它。 第二个 BOM 将被解释为零宽度不间断空格字符。  
  
-   SQL_C_BINARY：不执行转换，数据“按原样”传递到服务器。 UTF-16 数据必须以 BOM 为开头；否则，服务器可能无法正确地识别编码。  
  
-   SQL_C_CHAR：数据在客户端上转换为 UTF-16 并发送到服务器，就像 SQL_C_WCHAR 一样（包括添加 BOM）。 如果未在客户端代码页中对 XML 进行编码，则这可能导致数据损坏。  
  
 XML 标准要求 UTF-16 编码的 XML，以便以字节顺序标记 (BOM) UTF-16 字符代码 0xFEFF 开头。 当使用 SQL_C_BINARY 绑定时， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不要求或添加 BOM，因为编码隐含绑定。 其目的是为了在处理其他 XML 处理器和存储系统时提供简便性。 在此情况下，应向 UTF-16 编码的 XML 提供 BOM，并且应用程序无需关心实际编码，因为绝大多数的 XML 处理器（包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）会通过检查该值的前几个字节推导出编码。 从收到的 XML 数据[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端使用 SQL_C_BINARY 绑定始终以进行编码，utf-16 具有 BOM 但没有嵌入式编码声明。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  