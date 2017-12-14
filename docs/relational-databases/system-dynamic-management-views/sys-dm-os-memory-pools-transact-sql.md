---
title: "sys.dm_os_memory_pools (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e0e649688167c772defa308172f3b8a633ab6b7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosmemorypools-transact-sql"></a>sys.dm_os_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中存储的每个对象分别返回一行。 可以使用此视图来监视缓存内存使用情况，并识别错误的缓存行为。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_memory_pools**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary （8)**|代表内存池的项的内存地址。 不可为 null。|  
|**pool_id**|**int**|在一组池中的特定池的 ID。 不可为 null。|  
|**type**|**nvarchar(60)**|对象池的类型。 不可为 null。 有关详细信息，请参阅[sys.dm_os_memory_clerks &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**名称**|**nvarchar(256)**|系统为此内存对象分配的名称。 不可为 null。|  
|**max_free_entries_count**|**bigint**|池可以拥有的最大可用项的个数。 不可为 null。|  
|**free_entries_count**|**bigint**|池中当前可用项的个数。 不可为 null。|  
|**removed_in_all_rounds_count**|**bigint**|自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启动以来从池中删除的项数。 不可为 null。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件有时使用公用池框架来缓存同种、无状态类型的数据。 池框架比缓存框架更简单。 池中的所有项都被视为是等同的。 在内部，池是内存分配器，并且可以用在使用内存分配器的地方。  
  
## <a name="see-also"></a>另请参阅  
 
  [SQL Server 操作系统相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  

