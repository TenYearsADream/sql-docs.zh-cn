---
title: "主管 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LEAD_TSQL
- LEAD
dev_langs:
- TSQL
helpviewer_keywords:
- LEAD function
- analytic functions, LEAD
ms.assetid: 21f66bbf-d1ea-4f75-a3c4-20dc7fc1c69e
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5ec17dc2c38f040d6877cb69ac484ad56225a37
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lead-transact-sql"></a>LEAD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  访问相同结果集的后续行中的数据，而不使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的自联接。 LEAD 以当前行之后的给定物理偏移量来提供对行的访问。 在 SELECT 语句中使用此分析函数可将当前行中的值与后续行中的值进行比较。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LEAD ( scalar_expression [ ,offset ] , [ default ] )   
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>参数  
 *scalar_expression*  
 要根据指定偏移量返回的值。 这是一个返回单个（标量）值的任何类型的表达式。 *scalar_expression*不能为分析的函数。  
  
 *偏移量*  
 从在其中获取值的当前行前移的行数。 如果未指定，则默认值为 1。 *偏移量*可以是列、 子查询或计算结果为正整数其他表达式或可以隐式转换为**bigint**。 *偏移量*不能为负值或分析函数。  
  
 *默认值*  
 要返回时的值*scalar_expression*在*偏移量*为 NULL。 如果未指定默认值，则返回 NULL。 *默认*可以是列、 子查询或其他表达式，但不是能为分析的函数。 *默认*必须是类型兼容与*scalar_expression*。  
  
 通过**(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*将划分为分区函数应用到的 FROM 子句生成的结果集。 如果未指定，则此函数将查询结果集的所有行视为单个组。 *order_by_clause*应用函数之前确定数据的顺序。 当*partition_by_clause*指定，它确定每个分区中的数据的顺序。 *Order_by_clause*是必需的。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>返回类型  
 指定的数据类型*scalar_expression*。 如果返回 NULL *scalar_expression*可以为 null 或*默认*设置为 NULL。  
  
 LEAD 具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-compare-values-between-years"></a>A. 比较年度之间的值  
 此查询使用 LEAD 函数返回特定员工在后续年度的销售配额差异。 请注意，因为最后一行没有提供提前值，所以将返回默认值零 (0)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, YEAR(QuotaDate) AS SalesYear, SalesQuota AS CurrentQuota,   
    LEAD(SalesQuota, 1,0) OVER (ORDER BY YEAR(QuotaDate)) AS NextQuota  
FROM Sales.SalesPersonQuotaHistory  
WHERE BusinessEntityID = 275 and YEAR(QuotaDate) IN ('2005','2006');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
BusinessEntityID SalesYear   CurrentQuota          NextQuota  
---------------- ----------- --------------------- ---------------------  
275              2005        367000.00             556000.00  
275              2005        556000.00             502000.00  
275              2006        502000.00             550000.00  
275              2006        550000.00             1429000.00  
275              2006        1429000.00            1324000.00  
275              2006        1324000.00            0.00  
```  
  
### <a name="b-compare-values-within-partitions"></a>B. 比较分区中的值  
 下面的示例使用 LEAD 函数比较员工之间年初至今的销售额。 指定 PARTITION BY 子句来按销售地区对结果集中的行进行分区。 LEAD 函数分别应用于每个分区，并为每个分区重新启动计算。 在应用函数之前，在 OVER 子句中指定的 ORDER BY 子句将对每个分区中的行进行排序。 SELECT 语句中的 ORDER BY 子句对整个结果集中的行进行排序。 请注意，因为每个分区的最后一行没有提供提前值，所以将返回默认值零 (0)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TerritoryName, BusinessEntityID, SalesYTD,   
       LEAD (SalesYTD, 1, 0) OVER (PARTITION BY TerritoryName ORDER BY SalesYTD DESC) AS NextRepSales  
FROM Sales.vSalesPerson  
WHERE TerritoryName IN (N'Northwest', N'Canada')   
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
TerritoryName            BusinessEntityID SalesYTD              NextRepSales  
-----------------------  ---------------- --------------------- ---------------------  
Canada                   282              2604540.7172          1453719.4653  
Canada                   278              1453719.4653          0.00  
Northwest                284              1576562.1966          1573012.9383  
Northwest                283              1573012.9383          1352577.1325  
Northwest                280              1352577.1325          0.00  
  
```  
  
### <a name="c-specifying-arbitrary-expressions"></a>C. 指定任意表达式  
 下面的示例演示如何在 LEAD 函数语法中指定各种任意表达式。  
  
```  
CREATE TABLE T (a int, b int, c int);   
GO  
INSERT INTO T VALUES (1, 1, -3), (2, 2, 4), (3, 1, NULL), (4, 3, 1), (5, 2, NULL), (6, 1, 5);   
  
SELECT b, c,   
    LEAD(2*c, b*(SELECT MIN(b) FROM T), -c/2.0) OVER (ORDER BY a) AS i  
FROM T;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
b           c           i  
----------- ----------- -----------  
1           -3          8  
2           4           2  
1           NULL        2  
3           1           0  
2           NULL        NULL  
1           5           -2  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-compare-values-between-quarters"></a>D： 比较季度之间的值  
 下面的示例演示主管函数。 该查询通过后续日历季度获得指定员工销售配额值之间的差异。 请注意，因为没有前导值可用的最后一行之后，将使用默认的为零 (0)。  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       LEAD(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS NextQuota,  
   SalesAmountQuota - LEAD(Sale sAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Diff  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear IN (2001,2002)  
ORDER BY CalendarYear, CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Year Quarter  SalesQuota  NextQuota  Diff`  
  
 `---- -------  ----------  ---------  -------------`  
  
 `2001 3        28000.0000   7000.0000   21000.0000`  
  
 `2001 4         7000.0000  91000.0000  -84000.0000`  
  
 `2001 1        91000.0000 140000.0000  -49000.0000`  
  
 `2002 2       140000.0000   7000.0000    7000.0000`  
  
 `2002 3         7000.0000 154000.0000   84000.0000`  
  
 `2002 4       154000.0000      0.0000  154000.0000`  
  
## <a name="see-also"></a>另请参阅  
 [LAG &#40;Transact SQL &#41;](../../t-sql/functions/lag-transact-sql.md)  
  
  


