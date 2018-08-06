---
title: 使用行集绑定 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71a00f38d1424a05d5549e3b3a4c4fa816f26844
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412326"
---
# <a name="use-rowset-binding-odbc"></a>使用行集绑定 (ODBC)
    
### <a name="to-use-column-wise-binding"></a>使用按列绑定  
  
1.  对于每个绑定列，执行以下操作：  
  
    -   分配一个包含 R（或更多）个列缓冲区的数组以存储数据值，其中，R 是行集中的行数。  
  
    -   此外，可以选择分配一个包含 R（或更多）个列缓冲区的数组以存储数据长度。  
  
    -   调用[SQLBindCol](../../native-client-odbc-api/sqlbindcol.md)若要将列的数据值和数据长度数组绑定到行集的列。  
  
2.  调用[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)以设置以下属性：  
  
    -   将 SQL_ATTR_ROW_ARRAY_SIZE 设置为行集中的行数 (R)。  
  
    -   将 SQL_ATTR_ROW_BIND_TYPE 设置为 SQL_BIND_BY_COLUMN。  
  
    -   将 SQL_ATTR_ROWS FETCHED_PTR 属性设置为指向 SQLUINTEGER 变量，以包含所提取的行数。  
  
    -   将 SQL_ATTR_ROW_STATUS_PTR 设置为指向 SQLUSSMALLINT 变量的数组 [R]，以包含行状态指示器。  
  
3.  执行语句。  
  
4.  每次调用[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)检索 R 行并将数据传输到绑定列。  
  
### <a name="to-use-row-wise-binding"></a>使用按行绑定  
  
1.  分配结构数组 [R]，其中，R 是行集中的行数。 该结构对于每列都有一个元素，并且每个元素有两部分：  
  
    -   第一部分是适当的数据类型的变量，用于包含列数据。  
  
    -   第二部分是 SQLINTEGER 变量，用于包含列状态指示器。  
  
2.  调用[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)以设置以下属性：  
  
    -   将 SQL_ATTR_ROW_ARRAY_SIZE 设置为行集中的行数 (R)。  
  
    -   将 SQL_ATTR_ROW_BIND_TYPE 设置为在步骤 1 中分配的结构的大小。  
  
    -   将 SQL_ATTR_ROWS_FETCHED_PTR 属性设置为指向 SQLUINTEGER 变量，以包含所提取的行数。  
  
    -   将 SQL_ATTR_PARAMS_STATUS_PTR 设置为指向 SQLUSSMALLINT 变量的数组 [R]，以包含行状态指示器。  
  
3.  对于结果集中的每个列，调用[SQLBindCol](../../native-client-odbc-api/sqlbindcol.md)数据值和列的数据长度指针指向其在步骤 1 中分配的结构数组的第一个元素中的变量。  
  
4.  执行语句。  
  
5.  每次调用[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)检索 R 行并将数据传输到绑定列。  
  
## <a name="see-also"></a>请参阅  
 [使用游标操作指南主题&#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)   
 [如何实现游标](../../native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [使用游标&#40;ODBC&#41;](use-cursors-odbc.md)  
  
  