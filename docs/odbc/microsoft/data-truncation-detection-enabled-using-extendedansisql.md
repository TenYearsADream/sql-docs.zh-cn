---
title: 使用 ExtendedAnsiSQL 启用的数据截断检测 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95b7d538c2ace45b42c947b56ca5a5bd5f981ec5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744275"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 启用的数据截断检测
当启用 ExtendedAnsiSQL 标志和应用程序将数据插入到字符或二进制列和数据将被截断时，将检测截断。 时 ExtendedAnsiSQL 标志处于关闭状态，因为它在以前版本的 ODBC 桌面数据库驱动程序而不发出警告，截断的数据。
