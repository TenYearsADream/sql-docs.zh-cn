---
title: "使用行集绑定 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1afbe98e2825be95a6c009e5cf8123f4a91af2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="use-rowset-binding-odbc"></a>使用行集绑定 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-column-wise-binding"></a>使用按列绑定  
  
1.  对于每个绑定列，执行以下操作：  
  
    -   分配一个包含 R（或更多）个列缓冲区的数组以存储数据值，其中，R 是行集中的行数。  
  
    -   此外，可以选择分配一个包含 R（或更多）个列缓冲区的数组以存储数据长度。  
  
    -   调用[SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)将列的数据值和数据长度数组绑定到的行集列。  
  
2.  调用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)设置以下属性：  
  
    -   将 SQL_ATTR_ROW_ARRAY_SIZE 设置为行集中的行数 (R)。  
  
    -   将 SQL_ATTR_ROW_BIND_TYPE 设置为 SQL_BIND_BY_COLUMN。  
  
    -   将 SQL_ATTR_ROWS FETCHED_PTR 属性设置为指向 SQLUINTEGER 变量，以包含所提取的行数。  
  
    -   将 SQL_ATTR_ROW_STATUS_PTR 设置为指向 SQLUSSMALLINT 变量的数组 [R]，以包含行状态指示器。  
  
3.  执行语句。  
  
4.  每次调用[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)检索 R 行，并将数据传输到绑定的列。  
  
### <a name="to-use-row-wise-binding"></a>使用按行绑定  
  
1.  分配结构数组 [R]，其中，R 是行集中的行数。 该结构对于每列都有一个元素，并且每个元素有两部分：  
  
    -   第一部分是适当的数据类型的变量，用于包含列数据。  
  
    -   第二部分是 SQLINTEGER 变量，用于包含列状态指示器。  
  
2.  调用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)设置以下属性：  
  
    -   将 SQL_ATTR_ROW_ARRAY_SIZE 设置为行集中的行数 (R)。  
  
    -   将 SQL_ATTR_ROW_BIND_TYPE 设置为在步骤 1 中分配的结构的大小。  
  
    -   将 SQL_ATTR_ROWS_FETCHED_PTR 属性设置为指向 SQLUINTEGER 变量，以包含所提取的行数。  
  
    -   将 SQL_ATTR_PARAMS_STATUS_PTR 设置为指向 SQLUSSMALLINT 变量的数组 [R]，以包含行状态指示器。  
  
3.  对于结果集中每个列，调用[SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)到在步骤 1 中分配的结构数组的第一个元素及其变量指向的数据值和列的数据长度指针。  
  
4.  执行语句。  
  
5.  每次调用[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)检索 R 行，并将数据传输到绑定的列。  
  
## <a name="see-also"></a>另请参阅  
 [使用游标操作指南主题 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [如何实现游标](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [使用游标 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
  