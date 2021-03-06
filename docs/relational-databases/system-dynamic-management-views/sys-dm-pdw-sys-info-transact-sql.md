---
title: sys.dm_pdw_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 19f26a2f65a3b9c8484a62f79dc2995b47aca593
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039248"
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  提供了一组设备级别反映在设备的总体活动的计数器。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|在系统中当前的会话数。|0 到 max_active_sessions （见下文）。|  
|idle_sessions|**int**|当前处于空闲状态的会话数。||  
|active_requests|**int**|当前正在运行的活动请求数。||  
|queued_requests|**int**|当前排队请求数。||  
|active_loads|**int**|在系统中当前正在运行的负载的数目。||  
|queued_loads|**int**|排队等待执行的加载的数。||  
|active_backups|**int**|当前正在运行的备份数。||  
|active_restores|**int**|当前正在运行的备份还原的数量。||  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
