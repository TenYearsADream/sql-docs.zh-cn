---
title: 指定对象计数 （基于使用情况的优化向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6f4bb5bcf2584cba8265fb175b7581b6b40ce08
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62746131"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>指定对象计数（基于使用情况的优化向导）
  可以使用 **“指定对象计数”** 页自动计算多维数据集中的对象计数，或者手动输入估计的计数。 基于使用情况的优化向导使用对象计数来估计存储要求。  
  
## <a name="options"></a>选项  
 **多维数据集对象**  
 显示多维数据集中的维度和属性。 属性不具有其`AggregationUsage`属性设置为 None 中**查看聚合使用情况**向导页面显示，因为这些是需要指定的计数的唯一属性。  
  
 **估计的计数**  
 显示度量值组中估计的行数和数据库维度中估计的属性成员计数。 您可以键入一个值，以用作估计的计数，或可以计算估计的计数值。 若要计算计数值，请在该字段中键入 0，然后单击 **“计数”**。 已显示计数的字段不会更新。  
  
 **分区计数**  
 （可选）键入度量值组中估计的行数和分区中估计的属性成员计数。  
  
 **Count**  
 计算并重新填充所有空字段的“估计的计数”列。 已显示计数的字段不会更新。  
  
## <a name="see-also"></a>请参阅  
 [聚合设计向导的 F1 帮助](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 向导&#40;多维数据&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
