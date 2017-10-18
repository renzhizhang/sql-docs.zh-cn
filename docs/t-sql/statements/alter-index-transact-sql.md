---
title: "ALTER INDEX (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- indexes [SQL Server], reorganizing
- ALTER INDEX statement
- indexes [SQL Server], disabling
- online index operations
- index reorganization [SQL Server]
- ALLOW_ROW_LOCKS option
- ALL keyword
- reorganizing indexes
- constraints [SQL Server], indexes
- row locks [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- locking [SQL Server], indexes
- partitioned indexes [SQL Server], rebuilding
- defragmenting indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- index modifications [SQL Server]
- indexes [SQL Server], modifying
- index options [SQL Server]
- modifying indexes
- index disabling [SQL Server]
- MAXDOP index option, ALTER INDEX statement
- spatial indexes [SQL Server], modifying
- indexes [SQL Server], options
- ALLOW_PAGE_LOCKS option
- page locks [SQL Server]
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
caps.latest.revision: 222
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: f61b6469e40ba303cbff14db9bde15161b225ca7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="alter-index-transact-sql"></a>ALTER INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  通过禁用、重新生成或重新组织索引或者设置索引的选项，修改现有的表或视图索引（关系或 XML）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and SQL Database
  
ALTER INDEX { index_name | ALL } ON <object>  
{  
      REBUILD {  
            [ PARTITION = ALL ] [ WITH ( <rebuild_index_option> [ ,...n ] ) ]   
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> ) [ ,...n ] ]  
      }  
    | DISABLE  
    | REORGANIZE  [ PARTITION = partition_number ] [ WITH ( <reorganize_option>  ) ]  
    | SET ( <set_index_option> [ ,...n ] )   
    | RESUME [WITH (<resumable_index_options>,[…n])]
    | PAUSE
    | ABORT
}  
[ ; ]  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<rebuild_index_option > ::=  
{  
      PAD_INDEX = { ON | OFF }  
    | FILLFACTOR = fillfactor   
    | SORT_IN_TEMPDB = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | STATISTICS_INCREMENTAL = { ON | OFF }  
    | ONLINE = {   
          ON [ ( <low_priority_lock_wait> ) ]   
        | OFF } 
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | COMPRESSION_DELAY = {0 | delay [Minutes]}  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }   
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]  
}  
  
<single_partition_rebuild_index_option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<reorganize_option>::=  
{  
       LOB_COMPACTION = { ON | OFF }  
    |  COMPRESS_ALL_ROW_GROUPS =  { ON | OFF}  
}  
  
<set_index_option>::=  
{  
      ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | COMPRESSION_DELAY= {0 | delay [Minutes]}  
}  

<resumable_index_option> ::=
 { 
    MAXDOP = max_degree_of_parallelism
    | MAX_DURATION =<time> [MINUTES]
    | <low_priority_lock_wait>  
 }
 
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                          ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )  
}  

```  
  
```  
-- Syntax for SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER INDEX { index_name | ALL }  
    ON   [ schema_name. ] table_name  
{  
      REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_index_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> )] ] 
      }  
    | DISABLE  
    | REORGANIZE [ PARTITION = partition_number ]  
}  
[;]  

<rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
  
```    
## <a name="arguments"></a>参数  
 *index_name*  
 索引的名称。 索引名称在表或视图中必须唯一，但在数据库中不必唯一。 索引名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 ALL  
 指定与表或视图相关联的所有索引，而不考虑是什么索引类型。 如果有一个或多个索引脱机或不允许对一个或多个索引类型执行只读文件组操作或指定操作，则指定 ALL 将导致语句失败。 下表列出了索引操作和不允许使用的索引类型。  
  
|所有与此操作使用关键字|如果表有一个或多个，语句会失败|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|XML 索引<br /><br /> 空间索引<br /><br /> 列存储索引：**适用于：** （从 SQL Server 2012 开始） 的 SQL Server 和 Azure SQL 数据库。|  
|重新生成分区 = *partition_number*|未分区的索引、XML 索引、空间索引或已禁用的索引|  
|REORGANIZE|ALLOW_PAGE_LOCKS 设置为 OFF 的索引。|  
|重新组织分区 = *partition_number*|未分区的索引、XML 索引、空间索引或已禁用的索引|  
|IGNORE_DUP_KEY = ON|XML 索引<br /><br /> 空间索引<br /><br /> 列存储索引：**适用于：** （从 SQL Server 2012 开始） 的 SQL Server 和 Azure SQL 数据库。|  
|ONLINE = ON|XML 索引<br /><br /> 空间索引<br /><br /> 列存储索引：**适用于：** （从 SQL Server 2012 开始） 的 SQL Server 和 Azure SQL 数据库。|
| 可恢复 = ON  | 不支持的可恢复索引**所有**关键字。 <br /><br /> **适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能） |   
  
> [!WARNING]
>  有关详细信息可以联机执行索引操作，请参阅[联机索引操作准则](../../relational-databases/indexes/guidelines-for-online-index-operations.md)。

 如果使用分区指定了 ALL = *partition_number*，所有索引必须都对齐。 这意味着，它们是基于等同的分区函数进行分区的。 使用分区具有相同导致所有索引分区*partition_number*要重新生成或重新组织。 有关已分区索引的详细信息，请参阅 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 *database_name*  
 数据库的名称。  
  
 *schema_name*  
 表或视图所属架构的名称。  
  
 *table_or_view_name*  
 与该索引关联的表或视图的名称。 若要显示有关对象的索引的报表，使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目录视图。  
  
 SQL Database 支持三个部分组成的名称格式 database_name。[schema_name].table_or_view_name database_name 是当前数据库或 database_name 是 tempdb 和 table_or_view_name 时以 # 开头。  
  
 重新生成 [WITH **(**\<rebuild_index_option > [ **，**...*n*]**)** ]  
 指定将使用相同的列、索引类型、唯一性属性和排序顺序重新生成索引。 此子句相当于[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)。 REBUILD 启用已禁用的索引。 重新生成聚集索引并不重新生成关联的非聚集索引，除非指定了关键字 ALL。 如果未指定索引选项，现有的索引选项值存储在[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)应用。 其值不会存储在任何索引选项**sys.indexes**，则应用默认的选项的参数定义中所示。  
  
 如果指定 ALL 且基础表为堆，则重新生成操作对表没有任何影响。 重新生成与表相关联的所有非聚集索引。  
  
 如果数据库恢复模式设置为大容量日志记录或简单日志记录，则可以对重新生成操作进行最小日志记录。  
  
> [!NOTE]
>  重新生成主 XML 索引时，基础用户表在索引操作持续期间不可用。  
  
**适用于**: SQL Server （从 SQL Server 2012 开始） 和 Azure SQL 数据库。
  
 对于列存储索引，重新生成操作：  
  
1.  不使用排序顺序。  
  
2.  在重新生成进行时获取表或分区上的排他锁。  数据是“离线”的，在重新生成期间不可用，即使使用 NOLOCK、RCSI 或 SI 也是如此。  
  
3.  将所有数据重新压缩到列存储中。 在进行重新生成时存在列存储索引的两个副本。 在重新生成完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将删除原始列存储索引。  
  
 有关重新生成列存储索引的详细信息，请参阅[列存储索引的碎片整理](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
PARTITION  

**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
 指定只重新生成或重新组织索引的一个分区。 如果不指定分区*index_name*不是已分区的索引。  
  
 PARTITION = ALL 重新生成所有分区。  
  
> [!WARNING]
>  对超过 1,000 个分区的表创建和重新生成非对齐索引是可能的，但不支持。 这样做可能会导致性能下降，或在执行这些操作的过程中占用过多内存。 我们建议当分区数超过 1000 时，仅使用对齐索引。  
  
 *partition_number*  
   
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。
  
 要重新生成或重新组织已分区索引的分区数。 *partition_number*是可引用变量的常量表达式。 其中包括用户定义类型变量或函数以及用户定义函数，但不能引用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 *partition_number*必须存在或该语句将失败。  
  
 与**(**\<single_partition_rebuild_index_option >**)**  
   
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
 SORT_IN_TEMPDB、 MAXDOP 和 DATA_COMPRESSION 是可在重新生成单个分区时指定的选项 (分区 =  *n* )。 不能在单个分区重新生成操作中指定 XML 索引。  
  
 DISABLE  
 将索引标记为已禁用，从而不能由 [!INCLUDE[ssDE](../../includes/ssde-md.md)]使用。 可禁用任何索引。 已禁用的索引的索引定义保留在没有基础索引数据的系统目录中。 禁用聚集索引将阻止用户访问基础表数据。 若要启用索引，请使用 ALTER INDEX REBUILD 或 CREATE INDEX WITH DROP_EXISTING。 有关详细信息，请参阅[禁用索引和约束](../../relational-databases/indexes/disable-indexes-and-constraints.md)和[Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)。  
  
 重新组织行存储索引  
 对于行存储索引，重新组织指定来重新组织索引叶级别。  重新组织操作是：  
  
-   始终联机执行。 这意味着不保留长期阻塞的表锁，且对基础表的查询或更新可以在 ALTER INDEX REORGANIZE 事务处理期间继续。  
  
-   不允许已禁用的索引  
  
-   ALLOW_PAGE_LOCKS 设置为 OFF 时，不允许  
  
-   在事务中执行，并回滚事务时，不回滚。  
  
重新组织与**(** LOB_COMPACTION = { **ON** |OFF} **)**  
 适用于行存储索引。  
  
LOB_COMPACTION = ON  
  
-   指定要压缩所有包含的这些大型对象 (LOB) 数据类型的数据的页： 图像、 文本、 ntext、 varchar （max）、 nvarchar (max)、 varbinary （max） 和 xml。 压缩此数据可以减少磁盘上的数据大小。  
  
-   为聚集索引，这会压缩表中包含的所有 LOB 列。  
  
-   对于非聚集索引，这会压缩索引中的键 （包含） 列的所有 LOB 列。  
  
-   重新组织所有对所有索引执行 LOB_COMPACTION。 对于每个索引，这会压缩聚集的索引、 基础表或在非聚集索引的包含的列中的所有 LOB 列。  
  
LOB_COMPACTION = 关闭  
  
-   不压缩包含大型对象数据的页。  
  
-   OFF 对堆没有影响。  
  
重新组织列存储索引  
REORGANIZE 是在线执行的。  
  
对于列存储索引，重新组织将每个已关闭的增量行组作为压缩行组压缩到列存储。  
  
-   REORGANIZE 不需要将已关闭的增量行组移到压缩行组。 后台元组发动机 (TM) 进程唤醒定期压缩已关闭的增量行组。 我们建议使用 REORGANIZE 元组发动机落后时。 重新组织可以更加主动地压缩行组。  
  
-   若要压缩所有打开和已关闭行组，请参阅本部分中的重新组织与 (COMPRESS_ALL_ROW_GROUPS) 选项。  
  
对于 SQL Server （从 2016年开始） 和 SQL 数据库中的列存储索引，重新组织执行下列其他碎片整理优化联机：  
  
-   以物理方式从行组删除行时已逻辑删除 10%或更多的行。 已删除的字节进行回收物理介质上。 例如，如果有 100 万行压缩的行组具有 100k 行删除的行，SQL Server 将删除已删除的行，并重新压缩 900 k 行与行组。 它将保存在存储上通过删除已删除的行。  
  
-   将合并一个或多个压缩行组来增加每个最大值的 1,024,576 行的行的行。 例如，如果你将批量导入的 102,400 行 5 批你将获得 5 压缩行组。 如果你运行重新组织，这些行组将获取合并到的大小 512,000 行 1 压缩行组。 这假定没有任何字典大小或内存限制。  
  
-   在其中 10%或更多的行已被逻辑删除的行组，SQL Server 将尝试与一个或多个行组组合此行组。    例如，具有 500,000 行压缩行组 1 和与 1,048,576 行的最大压缩行组 21。  行组 21 具有的删除的行数的 60%，这会为 409,830 行。 SQL Server 优先组合这些行来压缩已 909,830 行新行组的两个组。  
  
与重新组织 (COMPRESS_ALL_ROW_GROUPS = {ON |**OFF** })  
 在 SQL Server （从 2016年开始） 和 SQL 数据库中，COMPRESS_ALL_ROW_GROUPS 使您能够打开或已关闭增量行组强制转到列存储。 使用此选项时，不需要重新生成列存储索引，若要在清空增量行组。  此操作，请结合其他删除和合并碎片整理功能使它不再需要重新生成在大多数情况下的索引。    
-   ON 到列存储，而不考虑大小和状态 （关闭或打开） 强制所有行组。  
  
-   关闭到列存储强制所有已关闭行组。  
  
设置**(** \<set_index 选项 > [ **，**...*n*] **)**  
 指定不重新生成或重新组织索引的索引选项。 不能为已禁用的索引指定 SET。  
  
PAD_INDEX = { ON | OFF }  
   
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
 指定索引填充。 默认为 OFF。  
  
 ON  
 FILLFACTOR 指定的可用空间百分比应用于索引的中间级页。 如果在同一时间 PAD_INDEX 设置为 ON 不指定 FILLFACTOR，填充考虑因素中存储值[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)使用。  
  
 关闭或*fillfactor*未指定  
 中间级页已填充到接近容量限制。 这样将至少为索引可以基于中间页中的键集拥有的最大大小的一行留出足够的空间。  
  
 有关详细信息，请参阅 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)。  
  
填充因子 =*填充因子*  
 
 **适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。
  
 指定一个百分比，指示在[!INCLUDE[ssDE](../../includes/ssde-md.md)]创建或修改索引的过程中，应将每个索引页面的叶级填充到什么程度。 *填充因子*必须是介于 1 到 100 的整数值。 默认值为 0。 填充因子的值 0 和 100 在所有方面都是相同的。  
  
 显式的 FILLFACTOR 设置只是在索引首次创建或重新生成时应用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]并不会在页中动态保持指定的可用空间百分比。 有关详细信息，请参阅 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)。  
  
 若要查看的填充因子设置，请使用**sys.indexes**。  
  
> [!IMPORTANT]
>  使用 FILLFACTOR 值创建或更改聚集索引会影响数据占用的存储空间量，因为[!INCLUDE[ssDE](../../includes/ssde-md.md)]在创建聚集索引时会再分发数据。  
  
 SORT_IN_TEMPDB = {ON |**OFF** }  
 

**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
 指定是否存储中的排序结果**tempdb**。 默认为 OFF。  
  
 ON  
 用于生成索引的中间排序结果存储在**tempdb**。 如果**tempdb**是一组不同的与用户数据库的磁盘，这可以减少创建索引所需的时间。 但是，这会增加索引生成期间所使用的磁盘空间量。  
  
 OFF  
 中间排序结果与索引存储在同一数据库中。  
  
 如果不需要执行排序操作，或者可以在内存中进行排序，则忽略 SORT_IN_TEMPDB 选项。  
  
 有关详细信息，请参阅[SORT_IN_TEMPDB 选项为索引](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)。  
  
 IGNORE_DUP_KEY  **=**  {ON |关闭}  
 指定在插入操作尝试向唯一索引插入重复键值时的错误响应。 IGNORE_DUP_KEY 选项仅适用于创建或重新生成索引后发生的插入操作。 默认为 OFF。  
  
 ON  
 向唯一索引插入重复键值时将出现警告消息。 只有违反唯一性约束的行才会失败。  
  
 OFF  
 向唯一索引插入重复键值时将出现错误消息。 整个 INSERT 操作将被回滚。  
  
 对视图创建索引、 非唯一索引、 XML 索引、 空间索引和筛选的索引，IGNORE_DUP_KEY 不能设置为 ON。  
  
 若要查看 IGNORE_DUP_KEY，使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 在向后兼容的语法中，WITH IGNORE_DUP_KEY 等效于 WITH IGNORE_DUP_KEY = ON。  
  
 STATISTICS_NORECOMPUTE  **=**  {ON |关闭}  
 指定是否重新计算分布统计信息。 默认为 OFF。  
  
 ON  
 不会自动重新计算过时的统计信息。  
  
 OFF  
 启用统计信息自动更新功能。  
  
 若要恢复统计信息自动更新，请将 STATISTICS_NORECOMPUTE 设置为 OFF，或执行 UPDATE STATISTICS 但不包含 NORECOMPUTE 子句。  
  
> [!IMPORTANT]
>  如果禁用分发统计信息的自动重新计算，可能会阻止查询优化器为涉及该表的查询挑选最佳执行计划。  
  
 STATISTICS_INCREMENTAL = {ON |**OFF** }  
 当**ON**，创建的统计信息是每个分区统计信息。 当**OFF**，删除统计信息树和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新计算统计信息。 默认值是**OFF**。  
  
 如果不支持每个分区统计信息，将忽略该选项并生成警告。 对于以下统计信息类型，不支持增量统计信息：  
  
-   使用未与基表的分区对齐的索引创建的统计信息。  
  
-   对 Always On 可读辅助数据库创建的统计信息。  
  
-   对只读数据库创建的统计信息。  
  
-   对筛选的索引创建的统计信息。  
  
-   对视图创建的统计信息。  
  
-   对内部表创建的统计信息。  
  
-   使用空间索引或 XML 索引创建的统计信息。  
  
 
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。  
  
 联机 **=**  {ON |**OFF** }\<因为应用于 rebuild_index_option >  
 指定在索引操作期间基础表和关联的索引是否可用于查询和数据修改操作。 默认为 OFF。  
  
 对于 XML 索引或空间索引，仅支持 ONLINE = OFF。如果 ONLINE 设置为 ON，则会引发错误。  
  
> [!NOTE]
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的各版本中均不提供联机索引操作。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ON  
 在索引操作期间不持有长期表锁。 在索引操作的主要阶段，源表上只使用意向共享 (IS) 锁。 这样，即可继续对基础表和索引进行查询或更新。 操作开始时，将对源对象保持极短时间的共享 (S) 锁。 操作结束时，如果创建非聚集索引，将对源持有极短时间的 S 锁；当联机创建或删除聚集索引时，或者重新生成聚集或非聚集索引时，将获取 SCH-M（架构修改）锁。 对本地临时表创建索引时，ONLINE 不能设置为 ON。  
  
 OFF  
 在索引操作期间应用表锁。 创建、重新生成或删除聚集索引、空间索引或 XML 索引或者重新生成或删除非聚集索引的脱机索引操作将获得对表的架构修改 (Sch-M) 锁。 这样可以防止所有用户在操作期间访问基础表。 创建非聚集索引的脱机索引操作将对表获取共享 (S) 锁。 这样可以防止更新基础表，但允许读操作（如 SELECT 语句）。  
  
 有关详细信息，请参阅[联机索引操作的工作原理](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
 索引（包括全局临时表中的索引）可以联机重新生成，但以下索引除外：  
  
-   XML 索引  
  
-   本地临时表中的索引  
  
-   分区索引的子集（可以联机重新构建整个分区索引。）  

-  V12 之前, 的 SQL 数据库和 SQL Server 2012 之前的 SQL Server 不允许`ONLINE`选项的聚集的索引生成或重新生成操作，当基本表包含**varchar （max)**或**varbinary （max)**列。

可恢复 **=**  {ON |**OFF**}

**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）  

 指定是否可恢复联机索引操作。

 在索引操作是可恢复。

 关闭索引操作不是可恢复的。

MAX_DURATION  **=**  *时间*[**分钟**] 用于**RESUMABLE = ON** (需要**ONLINE = ON**).
 
**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）  

指示时间 （以分钟为单位指定的整数值） 可恢复联机索引操作正在暂停之前执行。 

ALLOW_ROW_LOCKS  **=**  { **ON** |关闭}  
 
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
 指定是否允许行锁。 默认值为 ON。  
  
 ON  
 在访问索引时允许使用行锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用行锁。  
  
 OFF  
 不使用行锁。  
  
ALLOW_PAGE_LOCKS  **=**  { **ON** |关闭}  
  
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。
  
 指定是否允许使用页锁。 默认值为 ON。  
  
 ON  
 访问索引时允许使用页锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用页锁。  
  
 OFF  
 不使用页锁。  
  
> [!NOTE]
>  ALLOW_PAGE_LOCKS 设置为 OFF 时，无法重新组织索引。  
  
 MAXDOP  **=**  max_degree_of_parallelism  
 
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
 重写**最大并行度**索引操作的持续时间的配置选项。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 使用 MAXDOP 可以限制在执行并行计划的过程中使用的处理器数量。 最大数量为 64 个处理器。  
  
> [!IMPORTANT]
>  虽然所有 XML 索引在语法上都支持 MAXDOP 选项，但对于空间索引或主 XML 索引，ALTER INDEX 当前只使用一个处理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 1  
 取消生成并行计划。  
  
 \>1  
 将并行索引操作中使用的最大处理器数量限制为指定数量。  
  
 0（默认值）  
 根据当前系统工作负荷使用实际的处理器数量或更少数量的处理器。  
  
 有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]
>  并非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个版本中均支持并行索引操作。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 COMPRESSION_DELAY  **=**  { **0** |*持续时间 [分钟]* }  
 此功能可从 SQL Server 2016 开始  
  
 对于基于磁盘的表，延迟指定的最小必须保持为增量行组处于关闭状态的分钟数增量行组之前中 SQL Server 可以将其压缩到压缩行组。 由于基于磁盘的表不跟踪插入和更新时间在上单个行，SQL Server 应用延迟到处于关闭状态的增量行组。  
默认值为 0 分钟。  
  
 默认值为 0 分钟。  
  
 有关何时使用 COMPRESSION_DELAY，实时运行分析，请参阅列存储索引的建议。  
  
 DATA_COMPRESSION  
 为指定的索引、分区号或分区范围指定数据压缩选项。 这些选项如下：  
  
 无  
 不压缩索引或指定的分区。 这不适用于列存储索引。  
  
 ROW  
 使用行压缩来压缩索引或指定的分区。 这不适用于列存储索引。  
  
 PAGE  
 使用页压缩来压缩索引或指定的分区。 这不适用于列存储索引。  
  
 COLUMNSTORE  
   
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。
  
 仅适用于列存储索引，包括非聚集列存储索引和聚集列存储索引。 COLUMNSTORE 指定对使用 COLUMNSTORE_ARCHIVE 选项压缩的索引或指定分区进行解压缩。 在还原数据时，将继续通过用于所有列存储索引的列存储压缩对数据进行压缩。  
  
 COLUMNSTORE_ARCHIVE  
  
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。
  
 仅适用于列存储索引，包括非聚集列存储索引和聚集列存储索引。 COLUMNSTORE_ARCHIVE 会进一步将指定分区压缩为更小的大小。 这可用于存档，或者用于要求更小存储大小并且可以付出更多时间来进行存储和检索的其他情形。  
  
 有关压缩的详细信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
 在分区上**(** { \<partition_number_expression > |\<范围 >}[**，**...n] **)**  
    
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。 
  
 指定对其应用 DATA_COMPRESSION 设置的分区。 如果索引未分区，则 ON PARTITIONS 参数将产生错误。 如果不提供 ON PARTITIONS 子句，则 DATA_COMPRESSION 选项将应用于分区索引的所有分区。  
  
 \<partition_number_expression > 可以通过以下方式指定：  
  
-   提供一个分区号，例如：ON PARTITIONS (2)。  
  
-   提供若干单独分区的分区号并用逗号将它们隔开，例如：ON PARTITIONS (1, 5)。  
  
-   同时提供范围和单独的分区：ON PARTITIONS (2, 4, 6 TO 8)。  
  
 \<范围 > 可以指定为分区号分隔逐字，例如： ON PARTITIONS (6 TO 8)。  
  
 若要为不同分区设置不同的数据压缩类型，请多次指定 DATA_COMPRESSION 选项，例如：  
  
```tsql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 联机 **=**  {ON |**OFF** }\<因为应用于 single_partition_rebuild_index_option >  
 指定是否了索引或索引分区的基础表可以重新生成联机或脱机。 如果**重新生成**在线执行 (**ON**) 此表中的数据是可用于在索引操作期间的查询和数据修改。  默认值是**OFF**。  
  
 ON  
 在索引操作期间不持有长期表锁。 在索引操作的主要阶段，源表上只使用意向共享 (IS) 锁。 上表的 S 锁需要在开始索引重新生成和末尾的联机索引重新生成表上的 SCH-M 锁。 不过两个锁都是短的元数据锁，特别是 Sch-M 锁必须等待所有阻塞事务完成。 在等待期间，Sch-M 锁在访问同一表时阻止在此锁后等待的所有其他事务。  
  
> [!NOTE]
>  联机索引重新生成可以设置*low_priority_lock_wait*此部分后面所述的选项。  
  
 OFF  
 在索引操作期间应用表锁。 这样可以防止所有用户在操作期间访问基础表。  
  
 与使用 WAIT_AT_LOW_PRIORITY **ONLINE = ON**仅。  
 
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。
  
 联机索引重新生成必须等待对此表执行的阻塞操作。 **WAIT_AT_LOW_PRIORITY**指示联机索引重新生成操作将等待低优先级锁，从而允许同时联机索引生成操作正在等待继续其他操作。 省略**等待在低优先级**选项等同于`WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。 有关详细信息，请参阅[WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md)。 
  
 MAX_DURATION =*时间*[**分钟**]  
  
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。
  
 联机索引重新生成锁将在执行 DDL 命令时以低优先级等待的等待时间（以分钟为单位指定的整数值）。 如果该操作被阻止的**MAX_DURATION**时间、 之一**ABORT_AFTER_WAIT**将执行操作。 **MAX_DURATION**时间始终是以分钟和 word**分钟**可以省略。  
 
 ABORT_AFTER_WAIT = [**NONE** | **自助** | **BLOCKERS** }]  
   
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。
  
 无  
 继续以普通（常规）优先级等待锁。  
  
 SELF  
 不采取任何操作，直接退出当前执行的联机索引重新生成 DDL 操作。  
  
 BLOCKERS  
 终止阻塞联机索引重新生成 DDL 操作的所有用户事务以使操作可以继续。 **BLOCKERS**选项要求登录拥有**ALTER ANY CONNECTION**权限。  
 
 RESUME 
 
**适用于**： 开头 （功能处于公共预览版中） 的 SQL Server 2017

恢复已暂停，手动或由于失败的索引操作。

MAX_DURATION 用于**RESUMABLE = ON**

 
**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）

时间 （以分钟为单位指定一个整数值） 可恢复的联机索引操作之后执行正在恢复。 时间到期后，可恢复的操作已暂停，如果它仍在运行。

与使用 WAIT_AT_LOW_PRIORITY **RESUMABLE = ON**和**ONLINE = ON**。  
  
**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）
  
 要等待的时间对此表的阻止操作暂停后恢复联机索引重新生成。 **WAIT_AT_LOW_PRIORITY**指示联机索引重新生成操作将等待低优先级锁，从而允许同时联机索引生成操作正在等待继续其他操作。 省略**等待在低优先级**选项等同于`WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。 有关详细信息，请参阅[WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md)。 


PAUSE
 
**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）
  
暂停可恢复的联机索引重新生成操作。

中止

**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）   

中止已声明为可恢复的正在运行或暂停索引操作。 您必须显式执行**中止**命令终止可恢复索引重新生成操作。 故障或暂停可恢复的索引操作不会终止其执行;相反，它留在无限期暂停状态的操作。
  
## <a name="remarks"></a>注释  
 ALTER INDEX 不能用于对索引重新分区或将索引移到其他文件组。 此语句不能用于修改索引定义，如添加或删除列，或更改列的顺序。 使用带有 DROP_EXISTING 子句的 CREATE INDEX 执行这些操作。  
  
 未显式指定选项时，则应用当前设置。 例如，如果未在 REBUILD 子句中指定 FILLFACTOR 设置，将在重新生成过程中使用系统目录中存储的填充因子值。 若要查看当前的索引选项设置，请使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
> [!NOTE]
>  系统目录中不存储 ONLINE、MAXDOP 和 SORT_IN_TEMPDB 的值。 除非在索引语句中指定，否则，将使用选项的默认值。
  
 在多处理器计算机中，就像其他查询那样，ALTER INDEX REBUILD 自动使用更多处理器来执行与修改索引相关联的扫描和排序操作。 当你运行 ALTER INDEX REORGANIZE，无论 LOB_COMPACTION，**最大并行度**值是单个线程的操作。 有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
 如果索引所在的文件组脱机或设置为只读，则无法重新组织或重新生成索引。 如果指定了关键字 ALL，但有一个或多个索引位于脱机文件组或只读文件组中，该语句将失败。  
  
## <a name="rebuilding-indexes"></a>重新生成索引  
 重新生成索引将会删除并重新创建索引。 这将根据指定的或现有的填充因子设置压缩页来删除碎片、回收磁盘空间，然后对连续页中的索引行重新排序。 如果指定 ALL，将删除表中的所有索引，然后在单个事务中重新生成。 不必预先删除 FOREIGN KEY 约束。 重新生成具有 128 个区或更多区的索引时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]延迟实际的页释放及其关联的锁，直到事务提交。  
  
 重新生成或重新组织小索引不会减少碎片。 小索引的页面有关存储在混合盘区中。 混合区最多可由八个对象共享，因此在重新组织或重新生成小索引之后可能不会减少小索引中的碎片。  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，当创建或重新生成已分区索引时，不会通过扫描表中的所有行来创建统计信息。 相反，查询优化器使用默认采样算法来生成统计信息。 若要通过扫描表中所有行的方法获得有关已分区索引的统计信息，请使用 CREATE STATISTICS 或 UPDATE STATISTICS 以及 FULLSCAN 子句。  
  
 在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您有时可以重新生成非聚集索引以纠正硬件故障导致的不一致问题。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，您仍然可以通过脱机重新生成非聚集索引来纠正索引和聚集索引之间的这种不一致问题。 但是，您不能通过联机重新生成索引来纠正非聚集索引的不一致，因为联机重新生成机制将会使用现有的非聚集索引作为重新生成的基础，因此仍存在不一致。 脱机重新生成索引有时会强制扫描聚集索引（或堆）并因此删除不一致。 要确保从聚集索引重新生成，请删除并重新创建非聚集索引。 与早期版本一样，建议通过从备份还原受影响的数据来从不一致状态进行恢复；但是，您可以通过脱机重新生成非聚集索引来纠正索引的不一致。 有关详细信息，请参阅 [DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)。  
  
 若要重新生成聚集列存储索引，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将：  
  
1.  在重新生成进行时获取表或分区上的排他锁。 在重新生成期间数据“处于脱机状态”并且不可用。  
  
2.  通过物理删除已从表中逻辑上删除的行对列存储进行碎片整理；已删除的字节在物理介质上回收。  
  
3.  从原始列存储索引（包括增量存储）中读取所有数据。 它将数据合并到新的行组中，并且将行组压缩到列存储中。  
  
4.  要求物理介质上的空间，以便在进行重新生成时存储列存储索引的两个副本。 在重新生成完成后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将删除原始聚集列存储索引。  
  
## <a name="reorganizing-indexes"></a>重新组织索引  
 使用最少系统资源重新组织索引。 通过对叶级页以物理方式重新排序，使之与叶节点的从左到右的逻辑顺序相匹配，进而对表和视图中的聚集索引和非聚集索引的叶级进行碎片整理。 重新组织还会压缩索引页。 压缩基于现有的填充因子值。 若要查看的填充因子设置，请使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 如果指定 ALL，将重新组织表中的关系索引（包括聚集索引和非聚集索引）和 XML 索引。 指定 ALL 时应用某些限制，请参阅“参数”部分的 ALL 定义。  
  
 有关详细信息，请参阅 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
## <a name="disabling-indexes"></a>禁用索引  
 禁用索引可防止用户访问该索引，对于聚集索引，还可防止用户访问基础表数据。 索引定义保留在系统目录中。 对视图禁用非聚集索引或聚集索引会以物理方式删除索引数据。 禁用聚集索引将阻止对数据的访问，但在删除或重新生成索引之前，数据在 B 树中一直保持未维护的状态。 若要查看启用或禁用索引的状态，查询**is_disabled**中的列**sys.indexes**目录视图。  
  
 如果表位于事务复制发布中，则无法禁用任何与主键列关联的索引。 复制需要使用这些索引。 若要禁用索引，必须先从发布中删除该表。 有关详细信息，请参阅[发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
 使用 ALTER INDEX REBUILD 语句或 CREATE INDEX WITH DROP_EXISTING 语句启用索引。 重新生成已禁用聚集索引不能在 ONLINE 选项设置为 ON 时执行。 有关详细信息，请参阅 [禁用索引和约束](../../relational-databases/indexes/disable-indexes-and-constraints.md)。  
  
## <a name="setting-options"></a>“设置选项”  
 您可以为指定的索引设置选项 ALLOW_ROW_LOCKS、ALLOW_PAGE_LOCKS、IGNORE_DUP_KEY 和 STATISTICS_NORECOMPUTE，而不重新生成或重新组织该索引。 修改的值立即应用于索引。 若要查看这些设置，请使用**sys.indexes**。 有关详细信息，请参阅 [设置索引选项](../../relational-databases/indexes/set-index-options.md)。  
  
### <a name="row-and-page-locks-options"></a>行锁和页锁选项  
 如果 ALLOW_ROW_LOCKS = ON 并且 ALLOW_PAGE_LOCK = ON，则当访问索引时将允许行级别、页级别和表级别的锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]将选择相应的锁，并且可以将锁从行锁或页锁升级到表锁。  
  
 如果 ALLOW_ROW_LOCKS = OFF 并且 ALLOW_PAGE_LOCK = OFF，则当访问索引时只允许表级锁。  
  
 设置行锁或页锁选项时，如果指定 ALL，这些设置将应用于所有索引。 基础表为堆时，通过以下方式应用这些设置：  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON 或 OFF|应用于堆和任何关联的非聚集索引。|  
|ALLOW_PAGE_LOCKS = ON|应用于堆和任何关联的非聚集索引。|  
|ALLOW_PAGE_LOCKS = OFF|完全针对非聚集索引。 这意味着不允许对非聚集索引使用所有页锁。 在堆中，仅不允许使用有页的共享 (S) 锁、更新 (U) 锁和排他 (X) 锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]仍然可以获取意向页锁（IS、IU 或 IX），供内部使用。|  
  
## <a name="online-index-operations"></a>联机索引操作  
 重新生成索引且 ONLINE 选项设置为 ON 时，基础对象、表和关联的索引均可用于查询和数据修改。 您也可以联机重新生成单个分区上某索引的一部分。 更改过程中，排他表锁只保留非常短的时间。  
  
 重新组织索引始终联机执行。 该进程不长期保留锁，因此，不阻塞正在运行的查询或更新。  
  
 只有在执行以下操作时，才能对同一个表或表部分执行并发联机索引操作：  
  
-   创建多个非聚集索引。  
  
-   在同一个表中重新组织不同索引。  
  
-   在同一个表中重新生成不重叠的索引时，重新组织不同的索引。  
  
 同一时间执行的所有其他联机索引操作都将失败。 例如，您不能在同一个表中同时重新生成两个索引或更多索引，也不能在同一个表中重新生成现有索引时创建新的索引。  

### <a name="resumable-index-operations"></a>可恢复的索引操作

**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）

联机索引重新生成被指定为可恢复使用 RESUMABLE = ON 选项。 
-  可恢复的选项不会保存在给定索引的元数据并且仅适用于当前的 DDL 语句的持续时间。 因此，RESUMABLE = ON 子句必须显式指定，若要启用 resumability。

-  请注意两个不同的 MAX_DURATION 选项。 一个与 low_priority_lock_wait 相关，它的其他相关 RESUMABLE = ON 选项。
   -  支持为 RESUMABLE MAX_DURATION 选项 = ON 选项或**low_priority_lock_wait**参数选项。 
   MAX_DURATION 可恢复的选项指定正在重新生成索引的时间间隔。 使用此时间后重新生成索引或者暂停或完成其执行。 用户决定时可以恢复已暂停索引重新生成。 **时间**以分钟为 MAX_DURATION 必须是大于 0 分钟和小于或等于一周 （7 x 24 x 60 = 10080 分钟的时间）。 具有长暂停索引操作可能会影响特定的表上的 DML 性能，以及数据库磁盘容量，因为两个索引原始和新创建的一个需要磁盘空间并需要在 DML 操作期间更新。 如果省略 MAX_DURATION 选项，则索引操作将继续，直到其完成或失败为止。 
-   \<Low_priority_lock_wait > 参数选项允许你决定如何在索引操作可以继续执行时在 SCH-M 锁相上被阻止。
 
-  重新执行具有相同参数的原始 ALTER INDEX REBUILD 语句将恢复暂停的索引重新生成操作。 你可以通过执行 ALTER 索引恢复的语句来恢复已暂停的索引重新生成操作。
-  SORT_IN_TEMPDB = ON 可恢复的索引不支持选项 
-  将 DDL 命令与 RESUMABLE = ON 无法执行显式事务中 (不能属于开始 tran... 提交块）。
-  仅都已暂停的索引操作都是可恢复的。
-   当恢复已暂停某一索引操作，你可以更改为新值的 MAXDOP 值。  如果未指定 MAXDOP 当恢复已暂停某一索引操作，将使用最后一个的 MAXDOP 值。 如果索引重新生成操作未在所有指定 MAXDOP 选项，则采用默认值。
- 若要暂停立即索引操作，你可以停止正在进行的命令 (CTRL-C)，也可以执行 ALTER INDEX 暂停命令或 KILL *session_id*命令。 一旦命令被暂停它可以恢复使用恢复选项。
-  中止命令可终止的会话中承载原始索引重新生成，并且将中止此索引操作  
-  没有额外的资源所需的可恢复索引重新生成除外
   -    其他空间保持正在生成索引所需包括索引正在暂停时的时间
   -    阻止任何 DDL 修改 DDL 状态
-  虚影清除将运行在索引暂停阶段，但它将暂停期间运行的索引   
为可恢复索引重新生成操作禁用以下功能
   -    重新生成已禁用的索引不支持 RESUMABLE = ON
   -    ALTER 索引重新生成所有的命令
   -    使用重新生成索引的 ALTER TABLE  
   -    使用的 DDL 命令"RESUMEABLE = ON"不能显式事务中执行 (不能属于开始 tran... 提交块）
   -    重新生成已计算的索引或时间戳列作为键列。
-   索引重新生成在基础表包含 LOB 列可恢复群集的情况下需要此操作的开始 SCH-M 锁
   -    SORT_IN_TEMPDB = ON 可恢复的索引不支持选项 

> [!NOTE]
> DDL 命令可运行直到完成、 暂停或失败。 以防该命令会暂停，则将发出错误，该值指示该操作已暂停和索引创建未完成。 可以从获取有关当前索引状态的详细信息[sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md)。 为之前发生故障时，将发出错误以及。 

  
 有关详细信息，请参阅 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>联机索引操作使用 WAIT_AT_LOW_PRIORITY  
  
 要执行联机索引重新生成的 DDL 语句，必须完成对某一特定表运行的所有活动阻塞事务。 在联机索引重新生成执行时，它会阻塞准备对此表执行的所有新事务。 尽管联机索引重新生成锁的持续时间非常短，但等待某一给定表的所有打开的事务完成并阻塞新事务启动可能对吞吐量造成很大影响，导致工作负荷变慢或超时，并严重限制对基础表的访问。 **WAIT_AT_LOW_PRIORITY**选项允许数据库管理员的管理所需的联机索引重新生成，并允许他们选择 3 个选项之一的 S 锁和 SCH-M 锁。 在所有 3 的情况下，如果过程的等待时间 ( `(MAX_DURATION = n [minutes])` )、 有没有阻止活动，而不等待立即执行联机索引重新生成和完成的 DDL 语句。  
  
## <a name="spatial-index-restrictions"></a>空间索引限制  
 重新生成空间索引时，基础用户表在索引操作持续期间不可用，因为空间索引持有架构锁。  
  
 对用户表的某一列定义了空间索引时，无法修改该表中的 PRIMARY KEY 约束。 若要更改 PRIMARY KEY 约束，首先要删除该表的每个空间索引。 修改 PRIMARY KEY 约束后，您可以重新创建每个空间索引。  
  
 在单个分区重新生成操作中，无法指定任何空间索引。 但是，您可以在完整的分区重新生成过程中指定空间索引。  
  
 若要更改特定于某个空间索引的选项（例如 BOUNDING_BOX 或 GRID），您可以使用 CREATE SPATIAL INDEX 语句指定 DROP_EXISTING = ON，或删除该空间索引并创建一个新的空间索引。 有关示例，请参阅 [CREATE SPATIAL INDEX (Transact-SQL)](../../t-sql/statements/create-spatial-index-transact-sql.md)中的“备注”部分。  
  
## <a name="data-compression"></a>Data Compression  
 有关数据压缩的详细信息，请参阅 [数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
 若要评估更改页和行压缩将如何影响表、 索引或分区，使用[sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)存储过程。  
  
 以下限制适用于已分区索引：  
  
-   当你使用`ALTER INDEX ALL ...`，你无法更改的压缩设置的单个分区如果表具有非对齐的索引。  
  
-   ALTER INDEX\<索引 >...REBUILD PARTITION ... 语法可重新生成索引的指定分区。  
  
-   ALTER INDEX\<索引 >...REBUILD WITH ... 语法可重新生成索引的所有分区。  
  
## <a name="statistics"></a>统计信息  
 执行时**ALTER INDEX ALL...** 上表中，更新仅与索引的统计信息关联。 针对表（而不是索引）自动或手动创建的统计信息不会更新。  
  
## <a name="permissions"></a>Permissions  
 若要执行 ALTER INDEX，至少需要对表或视图具有 ALTER 权限。  
  
## <a name="version-notes"></a>版本说明  
  
-   SQL 数据库不使用文件组和 filestream 选项。  
  
-   列存储索引不可用 SQL Server 2012 之前。 

-  可恢复的索引操作是可从开始的 SQL Server 2017 和 Azure SQL 数据库 （功能是以公共预览版） |   
  
## <a name="basic-syntax-example"></a>基本语法示例：   
  
```tsql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>示例： 列存储索引  
 这些示例适用于列存储索引。  
  
### <a name="a-reorganize-demo"></a>A. 重新组织演示  
 此示例演示 ALTER INDEX REORGANIZE 命令的工作原理。  它创建一个表具有多个行组，并且然后演示如何重新合并行组。  
  
```  
-- Create a database   
CREATE DATABASE [ columnstore ];  
GO  
  
-- Create a rowstore staging table  
CREATE TABLE [ staging ] (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey     int  
     )  
  
-- Insert 10 million rows into the staging table.   
DECLARE @loop int  
DECLARE @AccountDescription varchar(50)  
DECLARE @AccountKey int  
DECLARE @AccountType varchar(50)  
DECLARE @AccountCode int  
  
SELECT @loop = 0  
BEGIN TRAN  
    WHILE (@loop < 300000)   
      BEGIN  
        SELECT @AccountKey = CAST (RAND()*10000000 as int);  
        SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountCode =  CAST (RAND()*10000000 as int);  
  
        INSERT INTO  staging VALUES (@AccountKey, @AccountDescription, @AccountType, @AccountCode);  
  
        SELECT @loop = @loop + 1;  
    END  
COMMIT  
  
-- Create a table for the clustered columnstore index  
  
CREATE TABLE cci_target (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey int  
     )  
  
-- Convert the table to a clustered columnstore index named inxcci_cci_target;  
```tsql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 使用 TABLOCK 选项在并行中插入行。 从 SQL Server 2016 开始，INSERT INTO 操作可以并行运行时使用 TABLOCK。  
  
```tsql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 运行此命令可查看打开的增量行组。 行组数取决于并行度。  
  
```tsql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 运行此命令以强制到列存储的所有已关闭和打开行组。  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 再次运行此命令，你将看到较小的行组被合并到一个压缩行组。  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>B. 已关闭的增量行组压缩到列存储  
 此示例使用 REORGANIZE 选项设为压缩每个已关闭的增量行组到列存储为压缩行组。   这不是有必要，但当元组发动机不能压缩已关闭行组的速度不够快时非常有用。  
  
```tsql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>C. 所有打开和关闭增量行组压缩到列存储  
 不适用于： SQL Server 2012 和 2014年  
  
 从 SQL Server 2016 开始，你可以重新组织使用运行 (COMPRESS_ALL_ROW_GROUPS = ON) 每个打开和已关闭的增量行组压缩到列存储为压缩行组。    这将清空增量存储，并强制所有行被压缩到列存储。 这是执行许多插入操作，因为这些操作在一个或多个增量存储中存储的行后尤其有用。  
  
 REORGANIZE 将合并行组来填充最多的最大行数的行组\<= 1,024,576。 因此，压缩所有打开和已关闭行组时你不会得到与大量在它们中只有少量的行的压缩行组。 你想要为已满尽可能减少的压缩的大小并提高查询性能的行组。  
  
```tsql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>D. 对列存储索引联机碎片整理  
 不适用于： SQL Server 2012 和 2014年。  
  
 重新组织从 SQL Server 2016 开始，未超过压缩多增量行组到列存储。 它还执行联机碎片整理。 首先，它通过以物理方式删除已删除的行，10%或更多行组中的行已被删除时减少列存储的大小。  然后，它将组合在一起以形成更大包含最多为每行组 1,024,576 行的最大值的行组的行组。  将所键入的所有行组被重新压缩。  
  
> [!NOTE]
>  从 SQL Server 2016 开始，则重新生成列存储索引不能再在大多数情况下需要因为 REORGANIZE 以物理方式移除已删除的行，并合并行组。 COMPRESS_ALL_ROW_GROUPS 选项强制到其以前仅可以使用重新生成列存储的所有打开或已关闭的增量行组。   REORGANIZE 处于联机状态，并且出现在后台，因此该操作那样可以继续进行查询。  
  
```tsql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>E. 重新生成聚集列存储索引脱机  
 适用于： SQL Server 2012、 SQL Server 2014  
  
 使用 SQL Server 2016 和在启动[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，我们建议您使用 ALTER INDEX REORGANIZE 而不是 ALTER INDEX REBUILD。  
  
> [!NOTE]
>  在 SQL Server 2012 和 2014年中，重新组织仅用于已关闭行组压缩到列存储。 若要执行碎片整理操作，并为所有增量行组都强制转到列存储的唯一方法是重新生成索引。  
  
 此示例演示如何重新生成聚集列存储索引和所有增量行组都强制转到列存储。 这个第一步将准备具有一个聚集列存储索引的表 FactInternetSales2 并且插入来自前四列的数据。  
  
```tsql  
-- Uses AdventureWorksDW  
  
CREATE TABLE dbo.FactInternetSales2 (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_FactInternetSales2  
ON dbo.FactInternetSales2;  
  
INSERT INTO dbo.FactInternetSales2  
SELECT ProductKey, OrderDateKey, DueDateKey, ShipDateKey  
FROM dbo.FactInternetSales;  
  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 结果显示没有一个打开行组，这意味着[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将等待关闭行组和将数据移到列存储前添加更多的行。 此下一个语句重新生成聚集列存储索引，这会强制到列存储的所有行。  
  
```tsql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 SELECT 语句的结果表明行组被压缩 (COMPRESSED)，这意味着行组的列段现在被压缩并且存储于列存储中。  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>F. 重新生成聚集列存储索引脱机的分区  
 使用此窗体： SQL Server 2012、 SQL Server 2014  
  
 若要重新生成大型聚集列存储索引的分区，使用使用分区选项的 ALTER INDEX REBUILD。 此示例重新生成分区 12。 从 SQL Server 2016 开始，建议重新生成替换重新组织。  
  
```tsql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>G. 更改群集的而索引以使用存档压缩  
 不适用于： SQL Server 2012  
  
 你可以选择通过使用 COLUMNSTORE_ARCHIVE 数据压缩选项减少甚至可更进一步聚集列存储索引的大小。 这是适用于你想要保留更便宜的存储上的旧数据。 我们建议仅使用这通常由于不能访问的数据上解压缩低于使用正常的列存储压缩。  
  
 下面的示例重新生成一个聚集列存储索引以便使用存档压缩，然后显示如何删除该存档压缩。 最后的结果将仅使用列存储压缩。  
  
```tsql  
--Prepare the example by creating a table with a clustered columnstore index.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL  
);  
  
CREATE CLUSTERED INDEX cci_SimpleTable ON SimpleTable (ProductKey);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_SimpleTable  
ON SimpleTable  
WITH (DROP_EXISTING = ON);  
  
--Compress the table further by using archival compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE);  
  
--Remove the archive compression and only use columnstore compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE);  
GO  
```  
  
## <a name="examples-rowstore-indexes"></a>示例： 行存储索引  
  
### <a name="a-rebuilding-an-index"></a>A. 重新生成索引  
 下面的示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `Employee` 表中重新生成单个索引。  
  
```tsql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>B. 重新生成表的所有索引并指定选项  
 下面的示例指定了 `ALL` 关键字。 这将重新生成与 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的表 Production.Product 相关联的所有索引。 其中指定了三个选项。  
  
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
 下面的示例添加包含低优先级锁选项的 ONLINE 选项，并添加行压缩选项。  
  
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH   
(  
    FILLFACTOR = 80,   
    SORT_IN_TEMPDB = ON,  
    STATISTICS_NORECOMPUTE = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, ABORT_AFTER_WAIT = BLOCKERS ) ),   
    DATA_COMPRESSION = ROW  
);  
```  
  
### <a name="c-reorganizing-an-index-with-lob-compaction"></a>C. 通过 LOB 压缩重新组织索引  
 下面的示例重新整理 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的单个聚集索引。 因为该索引在叶级别包含 LOB 数据类型，所以该语句还会压缩所有包含该大型对象数据的页。 注意，不需要指定 WITH (LOB_COMPACTION) 选项，因为默认值为 ON。  
  
```tsql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>D. 设置索引的选项。  
 下面的示例为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的索引 `AK_SalesOrderHeader_SalesOrderNumber` 设置了几个选项。  
  
**适用于**: SQL Server （从 SQL Server 2008 开始） 和 Azure SQL 数据库。  
  
```tsql  
ALTER INDEX AK_SalesOrderHeader_SalesOrderNumber ON  
    Sales.SalesOrderHeader  
SET (  
    STATISTICS_NORECOMPUTE = ON,  
    IGNORE_DUP_KEY = ON,  
    ALLOW_PAGE_LOCKS = ON  
    ) ;  
GO
```  
  
### <a name="e-disabling-an-index"></a>E. 禁用索引。  
 下面的示例禁用了对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的 `Employee` 表的非聚集索引。  
  
```tsql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>F. 禁用约束  
 下面的示例通过禁用中的主键索引禁用 PRIMARY KEY 约束[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库。 自动禁用对基础表的 FOREIGN KEY 约束，并显示警告消息。  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
 结果集返回此警告消息。  
  
 ```tsql  
 Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
 on table 'EmployeeDepartmentHistory' referencing table 'Department'  
 was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
 ```  
  
### <a name="g-enabling-constraints"></a>G. 启用约束  
 下面的示例启用在示例 F 中禁用的 PRIMARY KEY 和 FOREIGN KEY 约束。  
  
 通过重新生成 PRIMARY KEY 索引启用 PRIMARY KEY 约束。  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
 此时，将启用 FOREIGN KEY 约束。  
  
```tsql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>H. 重新生成分区索引  
 下面的示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中重新生成一个分区索引为 `5` 的分区，分区号为 `IX_TransactionHistory_TransactionDate`。 分区 5 是联机重新生成的，并且对索引重新生成操作获取的每个锁分别应用低优先级锁的 10 分钟等待时间。 如果在此时间无法获取锁来完成索引重新生成，重新生成操作语句就会中止。  
  
**适用于**: SQL Server （从 SQL Server 2014 开始） 和 Azure SQL 数据库。  
  
```tsql  
-- Verify the partitioned indexes.  
SELECT *  
FROM sys.dm_db_index_physical_stats (DB_ID(),OBJECT_ID(N'Production.TransactionHistory'), NULL , NULL, NULL);  
GO  
--Rebuild only partition 5.  
ALTER INDEX IX_TransactionHistory_TransactionDate  
ON Production.TransactionHistory  
REBUILD Partition = 5   
   WITH (ONLINE = ON (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10 minutes, ABORT_AFTER_WAIT = SELF)));  
GO  
```  
  
### <a name="i-changing-the-compression-setting-of-an-index"></a>I. 更改索引的压缩设置  
 下面的示例重新生成未分区行存储表的索引。  
  
```tsql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
 有关其他数据压缩示例，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
 
### <a name="j-online-resumable-index-rebuild"></a>J. 可恢复的联机索引重新生成

**适用于**： 开头 SQL Server 2017 和 Azure SQL 数据库 （位于公共预览版中的功能）    

 下面的示例演示如何使用可恢复的联机索引重新生成。 

1. 执行联机索引重新生成作为恢复的挂起操作随 MAXDOP = 1。

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. 执行同一个试命令 （参阅上文） 的索引操作已暂停后，将自动索引重新生成操作。

3. 作为可恢复操作随 MAX_DURATION 设置为 240 分钟执行联机索引重新生成。

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. 暂停正在运行的可恢复的联机索引重新生成。

   ```tsql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. 恢复已执行，因为 maxdop 指定新值的可恢复操作将设置为 4 索引重新生成联机索引重新生成。

   ```tsql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. 恢复为可恢复执行索引联机重新生成联机索引重新生成操作。 设置为 2 的 MAXDOP 设置为 240 分钟，如果被阻止锁等待 10 分钟索引作为 resmumable 正在运行的索引的执行时间之后, 终止所有阻止程序问题。 

   ```tsql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. 中止可恢复索引重新生成操作正在运行或已暂停。

   ```tsql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>另请参阅  
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [创建空间索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [创建 XML 索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP INDEX &#40;Transact SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [禁用索引和约束](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [XML 索引 (SQL Server)](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [联机执行索引操作](../../relational-databases/indexes/perform-index-operations-online.md)   
 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


