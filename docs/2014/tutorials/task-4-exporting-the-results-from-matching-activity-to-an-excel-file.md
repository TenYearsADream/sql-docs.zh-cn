---
title: 任务 4：将结果导出匹配到 Excel 文件的活动 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c9424f2ba21fb4b93e359c8662974a82c62b4895
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250895"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>任务 4：将匹配活动的结果导出到 Excel 文件
  在本任务中，您将匹配活动的结果导出到 Excel 文件。  
  
1.  在中**导出**页上，选择**Excel 文件**有关**目标类型**。  
  
2.  选择**存活结果**选项。 在存活过程中，DQS 确定基于每个群集的存活记录**存活规则**所选。  
  
3.  单击**浏览**并导航到要存储输出文件的文件夹。  
  
4.  类型**Cleansed and Matched Suppliers.xls**的名称，然后单击**打开**。  
  
5.  确认**透视记录**选择了**存活规则**。 当您选择此选项时，为分类的输出选择每个分类的透视记录。 存留规则的其他选项有：  
  
    1.  **最完整记录：** 存活记录是具有最大填充字段数。  
  
    2.  **最长记录：** 存活记录是具有源字段中的词的最大数目。  
  
    3.  **最完整且最长记录：** 存活记录是具有的最大填充字段数且在每个字段中具有的词的最大数目。  
  
     ![从匹配页导出结果](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "从匹配页导出结果")  
  
6.  单击**导出**将结果导出到 Excel 文件。  
  
7.  单击**关闭**以关闭**匹配的导出**对话框。  
  
8.  单击**完成**以完成匹配活动。  
  
9. 打开**Cleansed and Matched Suppliers.xlsx**文件并确认未看到任何重复项 (SupplierID)。  
  
 现在，您的供应商数据已经过清理和匹配，删除了重复项。  
  
## <a name="next-step"></a>下一步  
 [第 4 课：在 MDS 中存储供应商数据](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)  
  
  
