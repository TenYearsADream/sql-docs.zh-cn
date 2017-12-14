---
title: "sys.xml_schema_component_placements (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_component_placements
- xml_schema_component_placements_TSQL
- xml_schema_component_placements
- sys.xml_schema_component_placements_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_component_placements catalog view
ms.assetid: 2d3c8828-e4b3-423d-bf11-990464c1341b
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1b2627c338f0fad92f3d11aea6f1db821ce18829
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysxmlschemacomponentplacements-transact-sql"></a>sys.xml_schema_component_placements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于每个 XML 架构组件位置，相应地返回一行。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|拥有此位置的 XML 架构组件的 ID。|  
|**placement_id**|**int**|位置的 ID。 在拥有它的 XML 架构组件中，位置 ID 是唯一的。|  
|**placed_xml_component_id**|**int**|所放置的 XML 架构组件的 ID。|  
|**is_default_fixed**|**bit**|1 = 默认值是一个固定的值。 不能在 XML 实例中覆盖此值。<br /><br /> 0 = 可以覆盖该值。（默认）|  
|**min_occurrences**|**int**|所放置的组件的最小出现次数。|  
|**max_occurrences**|**int**|所放置的组件的最大出现次数。|  
|**默认值**|**nvarchar (4000)**|如果提供值，则该值为默认值。 如果未提供默认值，则为 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构 &#40;XML 类型系统 &#41;目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  