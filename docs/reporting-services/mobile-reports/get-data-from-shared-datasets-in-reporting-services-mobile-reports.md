---
title: 在 Reporting Services 移动报表中从共享数据集获取数据 | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1437d9394a372ba9a0aa3510db8f903f9b737e16
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298176"
---
# <a name="get-data-from-shared-datasets-in-reporting-services-mobile-reports"></a>Get data from shared datasets in Reporting Services mobile reports
除了[从 Excel 文件中加载数据](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)外，SQL Server 移动报表发布服务器还可以访问几乎任何来源的数据。 访问数据需要在 Reporting Services Web 门户上配置的共享数据源。 了解有关 [创建共享数据源](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) 和 [创建共享数据集](../../reporting-services/report-data/manage-shared-datasets.md)的详细信息。  
  
在 Reporting Services 服务器上配置共享数据源和共享数据集后，可以在 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 中创建的移动报表中使用它们。   
  
从 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 连接到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]服务器后，将移动报表连接到共享数据集非常简单。   
  
1. 在 **数据** 选项卡上，选择 **添加数据**。  
  
2. 选择 **报表服务器**。   
  
3.  如果这是首次连接到服务器，请填写服务器名称以及你的用户名和密码。 将服务器名称按以下格式放入服务器地址框：  
  
    \<"servername">/reports/  
  
    在此示例中:  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. 选择 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 服务器时，会看到文件夹中的可用数据集。 选择数据集将数据导入 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
导入数据集后，可以按照自己的意愿使用模拟数据或 Excel 文件中的本地数据设计移动报表。  
  
默认情况下，共享数据集始终确保是最新数据，因为每次用户查看基于该数据集的移动报表时，SQL Server 都会运行基础查询并返回最新数据。 显然，如果很多人查看你的移动报表，这个方法可能并不适合，因此你可以设置缓存，以定期运行查询并缓存生成的数据集。 此博客文章介绍 [Web 门户中缓存和数据刷新的工作原理](https://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/)。  
  
## <a name="add-edit-or-remove-a-report-server"></a>添加、编辑或删除报表服务器  
  
如果已连接到报表服务器，在“数据”选项卡上选择“添加数据”后，看不到用于添加另一个报表服务器的选项。 这时应执行以下步骤：  
  
1. 选择左上角的“连接”。  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   “服务器连接”窗格在右侧打开。  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. 添加新的服务器连接，或者编辑或删除现有的连接。  
  
### <a name="see-also"></a>另请参阅  
- [使用 SQL Server Mobile Report Publisher 创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [Web 门户（SSRS 本机模式）](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  [在 iPad 应用中查看 SQL Server 移动报表和 KPI](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI for iOS)  
-  [View SQL Server mobile reports and KPIs in the iPhone app (Power BI for iOS)（在 iPhone 应用 (Power BI for iOS) 中查看 SQL Server 移动报表和 KPI）](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  

