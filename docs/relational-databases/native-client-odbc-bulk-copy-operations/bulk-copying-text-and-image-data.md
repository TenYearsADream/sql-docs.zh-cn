---
title: "大容量复制文本和图像数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e9e9a39634c28ea9948d2f34b08cd7401048b04
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="bulk-copying-text-and-image-data"></a>大容量复制文本和图像数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  大型**文本**， **ntext**，和**映像**的值为大容量复制使用[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)函数。 你的代码[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)为**文本**， **ntext**，或**映像**列*pData*指针设置为NULL，数据将向你提供该值**bcp_moretext**。 务必要指定的数据为每个提供的确切长度**文本**， **ntext**，或**映像**中大容量复制的每一行的列。 如果列的数据的长度不同于中指定的列长度[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)，使用[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)将长度设置为适当的值。 A [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)发送所有非**文本**、 非-**ntext**，和非-**映像**数据; 你然后调用**bcp_moretext**发送**文本**， **ntext**，或**映像**单独单位中的数据。 大容量复制函数确定所有数据均已都发送当前**文本**， **ntext**，或**映像**列时通过都发送数据的长度的总和**bcp_moretext**等于中最新指定的长度**bcp_collen**或**bcp_bind**。  
  
 **bcp_moretext**没有参数来标识列。 如果有多个**文本**， **ntext**，或**映像**列在行中， **bcp_moretext**对**文本**， **ntext**，或**映像**开头具有最低序号和继续到具有最高的第几号列的列的列。 **bcp_moretext**将转从一列到下一步时发送的数据长度之和等于中最新指定的长度**bcp_collen**或**bcp_bind**当前列。  
  
## <a name="see-also"></a>另请参阅  
 [执行大容量复制操作 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  