---
title: "STGeomFromWKB (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STGeomFromWKB_TSQL
- STGeomFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromWKB method
ms.assetid: 79d39d88-5440-49a7-9247-190eafce3f4f
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22841fbeff43f2d81d3760057d501004e44de534
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stgeomfromwkb-geography-data-type"></a>STGeomFromWKB（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回**geography**开放地理空间联盟 (OGC) 熟知二进制 (WKB) 表示形式的实例。
  
这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STGeomFromWKB ( 'WKB_geography' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 *WKB_geography*  
 是的 WKB 表示形式**geography**实例返回。 *WKB_geography*是**varbinary （max)**表达式。  
  
 *SRID*  
 是**int**表达式表示空间引用标识符 (SRID) 的**geography**实例返回。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**返回实例`STGeomFromText()`设置为相应的 WKB 输入。  
  
 此方法将引发**FormatException**如果输入不是格式正确。  
  
 此方法将引发**ArgumentException**如果输入包含对跖边缘。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomFromWKB()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地域方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
