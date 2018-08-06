---
title: SQL Server - Broker TO Statistics 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 404c16baf92fb1f10adbbfd5c04ce3cdc05c3247
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203077"
---
# <a name="sql-server-broker-to-statistics-object"></a>SQL Server Broker TO Statistics 对象
  SQLServer:Broker TO Statistics 性能对象报告有关 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话框请求传输对象的次数以及传输对象写入 **tempdb** 中的频率的信息。  
  
 传输对象记录 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话框的消息传输状态。 这些对象存储在内存中。 为了释放内存， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 会定期将各批非活动传输对象写入 **tempdb**的工作表中。  
  
 下表列出了此对象包含的计数器。  
  
|SQL Server Broker TO Statistics 计数器|Description|  
|----------------------------------------------|-----------------|  
|**页的Length of Batched Writes**|保存在一个批次中的传输对象平均数。|  
|**页的Time To Write Batch (ms)**|保存一批传输对象所需的平均毫秒数。|  
|**页的Time Between Batches (ms)**|不同传输对象批次写入之间间隔的平均毫秒数。|  
|**Tran Object Gets/sec**|对话框每秒请求传输对象的次数。|  
|**Tran Objects Marked Dirty/sec**|传输对象每秒标记为“脏”的次数。 当第一次出现导致内存中的副本不同于存储在 **tempdb**中的副本的修改时，传输对象会被其标记为“脏”。 当 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 必须在对话框的消息传输状态下记录更改时，将会修改传输对象。|  
|**Tran Object Writes/sec**|每秒将各批传输对象写入 **tempdb** 工作表的次数。 大量写入可表明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存正在承受很大的压力。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Access Methods 对象](sql-server-access-methods-object.md)   
 [SQL Server Memory Manager 对象](sql-server-memory-manager-object.md)   
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  