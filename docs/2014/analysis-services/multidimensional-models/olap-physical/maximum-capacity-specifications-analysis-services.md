---
title: 最大容量规范 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 561cbbb64734c117b295ca6d97420b6980fa5428
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725491"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>最大容量规范 (Analysis Services)
  以下各表基于不同的服务器部署模式指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 组件中定义的各种对象的最大大小和最大数量。  
  
 本主题包含以下各节：  
  
 [多维和数据挖掘 (DeploymentMode = 0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode=1)](#bkmk_sharepoint)  
  
 [表格 (DeploymentMode = 2)](#bkmk_vertipaq)  
  
##  <a name="bkmk_OLAP"></a> 多维和数据挖掘 (DeploymentMode = 0)  
 MOLAP 存储模式（既存储数据，也存储元数据）具有针对文件大小的附加物理限制。 字符串存储文件的默认最大大小是 4 GB。 如果您要求更大的文件来用于字符串存储，则可以指定其他字符串存储体系结构。 有关详细信息，请参阅[维度和分区的配置字符串存储](../configure-string-storage-for-dimensions-and-partitions.md)。  
  
|Object|最大大小/最大数量|  
|------------|----------------------------|  
|实例中的数据库|2^31-1 = 2,147,483,647|  
|数据库中的维度|2^31-1 = 2,147,483,647|  
|维度中的属性|2^31-1 = 2,147,483,647|  
|维度属性中的成员|2^31-1 = 2,147,483,647|  
|维度中的用户定义层次结构|2^31-1 = 2,147,483,647|  
|用户定义层次结构中的级别|2^31-1 = 2,147,483,647|  
|数据库中的多维数据集|2^31-1 = 2,147,483,647|  
|多维数据集中的度量值组|2^31-1 = 2,147,483,647|  
|度量值组中的度量值|2^31-1 = 2,147,483,647|  
|多维数据集中的计算|2^31-1 = 2,147,483,647|  
|多维数据集中的 KPI|2^31-1 = 2,147,483,647|  
|多维数据集中的操作|2^31-1 = 2,147,483,647|  
|多维数据集中的分区|2^31-1 = 2,147,483,647|  
|多维数据集中的翻译|2^31-1 = 2,147,483,647|  
|分区中的聚合|2^31-1 = 2,147,483,647|  
|查询返回的单元|2^31-1 = 2,147,483,647|  
|源查询的记录大小|64K|  
|对象名的长度|100 个字符|  
|数据挖掘模型属性列中的最大不同状态数|2^31-1 = 2,147,483,647|  
|考虑的最大属性数（功能选择）|2^31-1 = 2,147,483,647|  
  
 有关对象命名指南的详细信息，请参阅[ASSL 对象和对象特征](../scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
 有关联机分析处理 (OLAP) 和数据挖掘的数据源限制的详细信息，请参阅[支持数据源&#40;SSAS 多维&#41;](../supported-data-sources-ssas-multidimensional.md)，[数据源支持&#40;SSAS 多维&#41;](../supported-data-sources-ssas-multidimensional.md)，并[ASSL 对象和对象特征](../scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
##  <a name="bkmk_sharepoint"></a> SharePoint (DeploymentMode = 1)  
  
|Object|最大大小/最大数量|  
|------------|----------------------------|  
|实例中的数据库|2^31-1 = 2,147,483,647|  
|数据库中的表|2^31-1 = 2,147,483,647|  
|表中的列|2 ^31-1 = 2,147,483,647**警告：** 与同一个表相关联的计算列和表中的列的总数取决于度量值的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的行|无限制**警告：** 具有任何单一列可能包含超过 1,999,999,997 个非重复值的限制。|  
|表中的层次结构|2^31-1 = 2,147,483,647|  
|层次结构中的级别|2^31-1 = 2,147,483,647|  
|关系|2^31-1 = 2,147,483,647|  
|表中的键列|2^31-1 = 2,147,483,647|  
|表中的度量值|2 ^31-1 = 2,147,483,647**警告：** 表中度量值的总数取决于总列数和计算列关联到同一个表。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的计算列|2 ^31-1 = 2,147,483,647**警告：** 表中的计算列总数取决于列和度量值与同一个表相关联的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|查询返回的单元|2^31-1 = 2,147,483,647|  
|源查询的记录大小|64K|  
|对象名的长度|100 个字符|  
  
##  <a name="bkmk_vertipaq"></a> 表格 (DeploymentMode = 2)  
  
|Object|最大大小/最大数量|  
|------------|----------------------------|  
|实例中的数据库|2^31-1 = 2,147,483,647|  
|数据库中的表|2^31-1 = 2,147,483,647|  
|表中的列|2 ^31-1 = 2,147,483,647**警告：** 与同一个表相关联的计算列和表中的列的总数取决于度量值的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的行|无限制**警告：** 具有单列的表中可以有超过 1,999,999,997 个非重复值的限制。|  
|表中的层次结构|2^31-1 = 2,147,483,647|  
|层次结构中的级别|2^31-1 = 2,147,483,647|  
|关系|2^31-1 = 2,147,483,647|  
|表中的键列|2^31-1 = 2,147,483,647|  
|表中的度量值|2 ^31-1 = 2,147,483,647**警告：** 表中度量值的总数取决于总列数和计算列关联到同一个表。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的计算列|2 ^31-1 = 2,147,483,647**警告：** 表中的计算列总数取决于列和度量值与同一个表相关联的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|查询返回的单元|2^31-1 = 2,147,483,647|  
|源查询的记录大小|64K|  
|对象名的长度|100 个字符|  
  
## <a name="see-also"></a>请参阅  
 [确定 Analysis Services 实例的服务器模式](../../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [常规属性](../../server-properties/general-properties.md)  
  
  
