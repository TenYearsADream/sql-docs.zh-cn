---
title: MSSQL_ENG002627 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002627 error
ms.assetid: 7f4136ac-3784-4a41-a98c-8a02308e4883
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a102991d08085f093e08a068a3d3127c9d7f7fc6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62666693"
---
# <a name="mssqleng002627"></a>MSSQL_ENG002627
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2627|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称|不可用|  
|消息正文|违反了 %ls 约束 '%.*ls'。 不能在对象 '%.\*ls' 中插入重复键。|  
  
## <a name="explanation"></a>解释  
 这是可能引发的一般错误，不管是否复制数据库，都会引发该错误。 在已复制的数据库中，通常会引发该错误，因为尚未跨拓扑对主键进行适当的管理。 在分布式环境中，确保没有将同一值插入到多个节点上的主键列或任何其他唯一列，这一点很重要。 可能的原因包括：  
  
-   在多个节点上对行进行了插入和更新。 合并复制和事务性复制的可更新订阅都提供了冲突检测和解决，但是最好还是只在一个节点上插入或更新给定行。 对等事务性复制没有提供冲突检测和解决，它要求对插入和更新进行分区。  
  
-   在应该为只读的订阅服务器上插入了行。 应该将快照发布的订阅服务器视为只读，就像事务发布的订阅服务器一样，除非使用了可更新的订阅或对等事务性复制。  
  
-   使用了具有标识列的表，但是没有对该列进行适当的管理。  
  
## <a name="user-action"></a>用户操作  
 所需操作取决于引发错误的原因：  
  
-   在多个节点上对行进行了插入和更新。  
  
     不管使用哪种复制类型，我们都建议您尽可能地对插入和更新进行分区，因为这样可以减少检测和解决冲突所需的处理操作。 对于对等事务性复制，需要对插入和更新进行分区。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)。  
  
-   在应该为只读的订阅服务器上插入了行。  
  
     除非使用合并复制、具有可更新订阅的事务性复制或对等事务性复制，否则不要在订阅服务器上插入或更新行。  
  
-   使用了具有标识列的表，但是没有对该列进行适当的管理。  
  
     对于合并复制和具有可更新订阅的事务性复制，标识列应该由复制自动管理。 对于对等事务性复制，必须手动进行管理。 有关详细信息，请参阅[复制标识列](publish/replicate-identity-columns.md)。  
  
## <a name="see-also"></a>请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [合并复制](merge/merge-replication.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)   
 [事务复制的可更新订阅](transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
