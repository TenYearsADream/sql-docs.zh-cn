---
title: 升级主服务器前升级所有目标服务器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97272209c1ceba780711ecf4a07178ddf8943d49
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156722"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>升级主服务器前先升级所有目标服务器
  在升级主服务器前，升级正在运行配置为目标服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有计算机。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>Description  
 若要在多服务器环境下进行自动管理，您必须至少有一台主服务器和至少一台目标服务器。 主服务器将作业分发到目标服务器并从它那里接收事件。 主服务器还存储在目标服务器上运行的作业的作业定义的中央副本。  
  
 如果当前服务器已配置为主服务器，则在升级此主服务器前，请先升级所有目标服务器。  
  
## <a name="corrective-action"></a>纠正措施  
 如果无法在升级主服务器前升级所有目标服务器，则必须先脱离所有目标服务器，再在升级后重新登记这些服务器。  
  
 有关详细信息，请参阅"自动执行跨企业管理，"的主题"如何：脱离目标服务器从主服务器，"和"如何：登记到主目标服务器"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
