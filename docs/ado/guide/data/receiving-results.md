---
title: 接收结果 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 648fd220988a0b32837ddcdf2b4c1c23de5e9f69
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911184"
---
# <a name="receiving-results"></a>接收结果
在 ADO 中的大多数命令导致返回给调用方的一些信息。 返回行集的命令，请在收到的结果**记录集**对象，它是可能最常用的 ADO 对象。  
  
 有几种方法来接收中的数据**记录集**从数据源，包括调用以下对象：  
  
-   [Connection.Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 接收中的数据**记录集**对象以获取数据，参与的进程结束**连接**对象和一个**命令**对象时，隐式或显式。 在典型的客户端/服务器应用程序系统中，获取数据的整个过程需要一次往返过程在网络上为每个填充**记录集**。  
  
 若要接收多个结果集意味着，将需要进行多次往返通过网络，另一个用于封装在每个数据集**记录集**对象。 对于速度缓慢或堵塞网络，减少往返次数可帮助提高应用程序的性能。 因此，某些提供商提供支持，以便接收多个**记录集**的往返一次。 以下主题中对此进行了讨论：  
  
-   [接收多个记录集](../../../ado/guide/data/receiving-multiple-recordsets.md)
