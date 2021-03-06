---
title: 选择源多维数据集维度 （数据挖掘向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.selectsourcecube.f1
ms.assetid: 556e216b-5e21-4160-967d-4c57591fbab4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0f61dea4488e67c8b8c7ebd30920df2ef1774acd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62746889"
---
# <a name="select-the-source-cube-dimension-data-mining-wizard"></a>选择源多维数据集维度（数据挖掘向导）
  可以使用 **“选择源多维数据集维度”** 页，从包含要分析的事例的多维数据集中选择维度。 例如，如果您在生成一个依据人口统计信息对客户的购买行为进行分析的模型，您会选择 Customer 维度，该维度中通常包含每个客户的唯一记录以及表示人口统计信息（如性别、住址或收入）的各种属性。 在该向导的后面部分，您将可以添加一个与此事例表相关的表：例如，您可能添加一个列出该客户已购买产品的嵌套表。  
  
> [!NOTE]  
>  只有在向导的“选择定义方法”页上选择了“从现有多维数据集”之后，才会显示此页。  
  
## <a name="options"></a>选项  
 **选择源多维数据集维度**  
 选择将为挖掘结构提供源数据的多维数据集的维度。  
  
## <a name="choosing-a-dimension"></a>选择维度  
 因为只能选择一个维度在模型中使用，因此请务必了解多维数据集结构并选择可为您的模型提供最佳信息的维度。 如果无法确定要使用的维度，使用维度设计器浏览多维数据集并查看其中的字段和数据可能会很有用。 有关详细信息，请参阅[在维度设计器中浏览维度数据](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)。  
  
 如果你不熟悉维度，请参阅[维度简介（Analysis Services - 多维数据）](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)。  
  
 有关单个维度中通常包含的信息类型（包括可能对数据挖掘有用的属性和度量值）的详细信息，请参阅 [Dimension Relationships](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
 如果选择的维度未包含生成数据挖掘模型所需的所有相关属性，则可能需要修改该维度。 有关详细信息，请参阅 [定义数据库维度](multidimensional-models/define-database-dimensions.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘向导的 F1 帮助&#40;Analysis Services-数据挖掘&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [创建数据挖掘结构&#40;数据挖掘向导&#41;](create-the-data-mining-structure-data-mining-wizard.md)   
 [选择事例键&#40;数据挖掘向导&#41;](select-the-case-key-data-mining-wizard.md)  
  
  
