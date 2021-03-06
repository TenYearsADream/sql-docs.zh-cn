---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5bc7caa063d14967e576fd009a23110b9647836b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689030"
---
# <a name="bcpgettypename"></a>bcp_gettypename
  返回指定 BCP 类型标记的 SQL 类型名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *token*  
 指示 BCP 类型标记的值。  
  
 field  
 指示请求的标记是否为 max 类型。  
  
## <a name="returns"></a>返回  
 一个字符串，其中包含与 BCP 类型对应的 SQL 类型名称。 如果指定了无效的 BCP 类型，则返回空字符串。  
  
## <a name="remarks"></a>备注  
 BCP 类型标记在 sqlncli.h 头文件和 sqlncli11.lib 库中定义。  
  
 下表指定了可能的 BCP 类型、这些类型是否是 max 类型以及预期的输出。  
  
|BCP 类型名称|MaxType|“输出”|  
|-------------------|-------------|------------|  
|`SQLDECIMAL`|之前或之后|**decimal**|  
|`SQLNUMERIC`|之前或之后|**numeric**|  
|`SQLINT1`|之前或之后|**tinyint**|  
|`SQLINT2`|之前或之后|**smallint**|  
|`SQLINT4`|之前或之后|**int**|  
|`SQLMONEY`|之前或之后|**money**|  
|`SQLFLT8`|之前或之后|**float**|  
|`SQLDATETIME`|之前或之后|**datetime**|  
|`SQLBITN`|之前或之后|**bit-null**|  
|`SQLBIT`|之前或之后|**bit**|  
|`SQLBIGCHAR`|否|**char**|  
|`SQLCHARACTER`|否|**char**|  
|`SQLBIGVARCHAR`|否|**varchar**|  
|`SQLVARCHAR`|否|**varchar**|  
|`SQLTEXT`|之前或之后|**text**|  
|`SQLBIGBINARY`|否|**binary**|  
|`SQLBINARY`|否|**二进制**|  
|`SQLBIGVARBINARY`|否|**varbinary**|  
|`SQLVARBINARY`|否|**varbinary**|  
|`SQLIMAGE`|之前或之后|**Image**|  
|`SQLINTN`|之前或之后|**int-null**|  
|`SQLDATETIMN`|之前或之后|**datetime-null**|  
|`SQLMONEYN`|之前或之后|**money-null**|  
|`SQLFLTN`|之前或之后|**float-null**|  
|`SQLAOPSUM`|之前或之后|**Sum**|  
|`SQLAOPAVG`|之前或之后|**Avg**|  
|`SQLAOPCNT`|之前或之后|**Count**|  
|`SQLAOPMIN`|之前或之后|**Min**|  
|`SQLAOPMAX`|之前或之后|**Max**|  
|`SQLDATETIM4`|之前或之后|**smalldatetime**|  
|`SQLMONEY4`|之前或之后|**Smallmoney**|  
|`SQLFLT4`|之前或之后|**Real**|  
|`SQLUNIQUEID`|之前或之后|**uniqueidentifier**|  
|`SQLNCHAR`|否|**Nchar**|  
|`SQLNVARCHAR`|否|**Nvarchar**|  
|`SQLNTEXT`|之前或之后|**Ntext**|  
|`SQLVARIANT`|之前或之后|**sql_variant**|  
|`SQLINT8`|之前或之后|**Bigint**|  
|`SQLCHARACTER`|是|**varchar(max)**|  
|`SQLBIGCHAR`|是|**varchar(max)**|  
|`SQLBIGVARCHAR`|是|**varchar(max)**|  
|`SQLVARCHAR`|是|**varchar(max)**|  
|`SQLBINARY`|是|**varbinary(max)**|  
|`SQLBIGBINARY`|是|**varbinary(max)**|  
|`SQLBIGVARBINARY`|是|**varbinary(max)**|  
|`SQLVARBINARY`|是|**varbinary(max)**|  
|`SQLNCHAR`|是|**nvarchar(max)**|  
|`SQLNVARCHAR`|是|**nvarchar(max)**|  
|`SQLXML`|是|**Xml**|  
|`SQLUDT`|之前或之后|**Udt**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename 对日期和时间增强功能的支持  
 日期/时间类型的标记参数值在表中的"sqlncli.h 中的类型"列中所述[大容量复制更改的增强的日期和时间类型&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。 返回值位于“文件存储类型”列的对应行中。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
