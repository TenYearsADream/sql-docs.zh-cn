---
title: “SMO 和 DMO XP”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d55bd667909721a68d51bcd1db7128b809118843
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62755282"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO 和 DMO XP 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 SMO 和 DMO XP 选项可以在此服务器上启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) 扩展存储过程。  
  
 请注意，从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，DMO 已从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中删除。  
  
 下表中列出了该选项的可能值：  
  
|ReplTest1|含义|  
|-----------|-------------|  
|0|SMO XP 不可用。|  
|1|SMO XP 可用。 这是默认设置。|  
  
 此设置将立即生效。  
  
## <a name="examples"></a>示例  
 以下示例启用了 SMO 扩展存储过程。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 管理对象 (SMO) 编程指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
