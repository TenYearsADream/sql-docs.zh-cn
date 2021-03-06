---
title: 元数据 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined metadata [Master Data Services], about user-defined metadata
- metadata [Master Data Services], about metadata
- metadata [Master Data Services]
- user-defined metadata [Master Data Services]
ms.assetid: ac1aabe3-d8d4-4d7a-8954-50ee3c185d81
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f45d9d2a50327259c987cd41fefc6039c629eb77
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62764707"
---
# <a name="metadata-master-data-services"></a>元数据 (Master Data Services)
  在[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，用户定义元数据是您用于描述模型对象的信息。 例如，您可能要跟踪特定模型或实体的所有者，或者跟踪向实体提供数据的源系统。  
  
 用户定义的元数据由模型称为**元数据**。 时，此模型将自动包括[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]安装时，它是与所有其他 MDS 模型相似，区别在于你不能创建它的版本。  
  
 在使用用户定义元数据填充元数据模型之后，可以在订阅视图中包含该模型，以便它可由订阅系统使用。  
  
## <a name="metadata-entities"></a>元数据实体  
 “元数据”模型包括五个实体，每个实体都表示支持用户定义元数据的一种主数据模型对象。 例如，**模型元数据定义**实体包含成员表示模型，并**属性元数据定义**实体具有表示所有模型中的所有属性的成员。  
  
 为了定义某一模型对象的元数据，您填充其中一个成员的属性。 例如，在**实体元数据定义**实体，您可以填充 Price 成员的 Description 属性与文本：**当销售给客户的产品价格**。  
  
 只要添加或删除支持用户定义元数据的模型对象，元数据模型中的成员就会自动更新。  
  
 不能对元数据模型进行版本控制，添加或更改版本标志，也不能将该模型另存为模型部署包。 但是，该模型具有可用于其他主数据模型的其他所有功能。 例如，您可以对元数据模型实现一组业务规则，以便强制执行数据策略。  
  
## <a name="customizing-your-metadata-model"></a>自定义元数据模型  
 每个元数据定义实体都包括 Name、Code 和 Description 属性。 您可能要创建附加的属性以便进一步描述您的模型对象。  
  
 例如，您可以创建：  
  
-   名为 Owner 的基于域的属性，可用于跟踪各模型对象的所有者。  
  
-   名为 Last Review Date 的自由格式的属性，可用于跟踪所有者上次审核某一对象的日期。  
  
-   基于域的属性名为源，用于跟踪和管理与之交互的源系统[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]实例。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|向模型对象添加元数据。|[添加元数据&#40;Master Data Services&#41;](add-metadata-master-data-services.md)
|&nbsp;|&nbsp;|
  
## <a name="related-content"></a>相关内容  
  
-   [将数据导出&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
