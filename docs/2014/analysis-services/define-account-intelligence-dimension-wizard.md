---
title: 定义帐户智能 （维度向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 927442d1fe46fc42998643d4f7de47b438cbaa49
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732450"
---
# <a name="define-account-intelligence-dimension-wizard"></a>定义帐户智能（维度向导）
  可以使用 **“定义帐户智能”** 页，将 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型映射到与维度中的 **“帐户类型”** 属性类型关联的维度属性中定义的帐户类型。  
  
> [!NOTE]  
>  仅当你在“选择维度类型”页中选择“标准维度”以及在“指定维度类型”页上将维度属性映射到“帐户类型”属性类型时，才会显示此页。  
  
## <a name="options"></a>选项  
 **源表帐户类型**  
 显示分配给“指定维度键和类型”页中“帐户类型”属性类型的维度属性中包含的值。  
  
 **内置帐户类型**  
 选择在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型，该帐户类型将映射到源表中的帐户类型。  
  
 下表列出了在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**资产**|在特定时间拥有的物品的价值。|  
|**平衡**|在特定时间某物的计数。|  
|**费用**|所花费的价值。|  
|**流**|事物的增量计数。|  
|**收入**|收到的价值。|  
|**负债**|在特定时间所拖欠的价值。|  
|**统计**|某事物的计算比率，或者未聚合的某事物的计数。|  
  
## <a name="see-also"></a>请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [维度&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
