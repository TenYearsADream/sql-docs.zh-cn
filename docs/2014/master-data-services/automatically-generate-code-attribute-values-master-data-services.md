---
title: 自动生成代码属性值 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: bc686928863395217fa564ff04b7c26a52c1f1bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877254"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>自动生成 Code 属性值 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，当希望在每次创建新成员时自动为 Code 值分配一个整数时，自动为实体的 Code 属性设置值。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   实体必须存在。 有关详细信息，请参阅[创建实体 (Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-automatically-generate-code-values"></a>自动生成 Code 值  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  上**模型资源管理器**页上，从菜单栏中，依次指向**管理**然后单击**实体**。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  为您要生成其代码的实体选择行。  
  
5.  单击 **“编辑所选实体”**。  
  
6.  选中 **“自动创建代码值”** 复选框。  
  
7.  在 **“起始”** 框中，键入开始递增的数字。 如果成员已存在，则将基于最大的现有值设置 Code。 例如，如果最大的现有 Code 值为 299，则下一个成员的 Code 值将设置为 300。  
  
8.  单击**保存实体**。  
  
## <a name="see-also"></a>请参阅  
 [自动创建代码 (Master Data Services)](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [自动生成 Code 之外的属性值 (Master Data Services)](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
