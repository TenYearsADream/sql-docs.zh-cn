---
title: 实现 Data Quality Services 与 Master Data Services 的集成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 51cefe654fa35284a2bab851d39ed560a362356b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62695599"
---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>实现 Data Quality Services 与 Master Data Services 的集成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，匹配功能由 Data Quality Services (DQS) 提供。 此功能必须启用后才能使用。  
  
## <a name="prerequisites"></a>先决条件  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 应用程序和数据库必须存在。  
  
-   Data Quality Services 功能和数据质量客户端必须安装在承载 MDS 数据库的同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上。 有关详细信息，请参阅 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
### <a name="to-enable-data-quality-services-integration"></a>启用 Data Quality Services 集成  
  
1.  打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  在左窗格中单击 **“Web 配置”**。  
  
3.  在 **“Web 配置”** 页上，选择网站和 Web 应用程序。  
  
4.  在 **“启用 DQS 集成”** 部分中，单击 **“启用与 Data Quality Services 的集成”**。  
  
5.  在确认对话框中，单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [用于 Excel 的 MDS 外接程序中的数据质量匹配](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [用于 Microsoft Excel 的 Master Data Services 外接程序](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
