---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0fae1116025949657739878f754782d775bf8717
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653299"
---
# <a name="mssqlserver9524"></a>MSSQLSERVER_9524
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9254|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|XMLERR_INVALID_COLUMNSET_XML|  
|消息正文|提供的 XML 内容不符合稀疏列集所需的 XML 格式。|  
  
## <a name="explanation"></a>解释  
已尝试修改列集。 列集的 XML 内容必须满足列集的格式限制要求。 列集的常用格式如下所示：  
  
`<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
有关列集的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“使用列集”主题。  
  
## <a name="user-action"></a>用户操作  
在语句中更正此列集的 XML 格式。  
  
