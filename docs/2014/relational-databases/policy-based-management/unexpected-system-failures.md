---
title: 意外的系统故障 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 951b49c0356ae27cb58041af5186becfd12853bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62677066"
---
# <a name="unexpected-system-failures"></a>意外的系统故障
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查计算机事件日志中是否存在 SYSTEM Event 6008。 该事件表示意外的系统关闭。 系统可能不稳定，并且可能不能提供承载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例所需的稳定性和完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 立即找出服务器意外重新启动的原因，或者将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例移到另一台计算机。  
  
  
