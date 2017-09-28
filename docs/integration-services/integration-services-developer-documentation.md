---
title: "Integration Services 开发人员文档 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
caps.latest.revision: 76
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf7d7afba8ada3f6027db3053914b1822597792c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-developer-documentation"></a>集成服务开发人员文档
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含一个完全重写的对象模型，已使用使用功能改善了该模型，以使包扩展和编程更加方便、灵活和强大。 开发人员几乎可以对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包进行全方位的扩展和编程。  
  
 作为 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 开发人员，您有两种基本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 编程方法可选用：  
  
-   您可以通过编写 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中可用的组件来扩展包，以在包中提供自定义功能。  
  
-   您可以用编程方式从您自己的应用程序创建、配置和运行包。  
  
 如果你发现中的内置组件[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]不能满足你的要求，你可以扩展的能力[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]通过编码自己的扩展。 如果采用这种方法，则有两种不同的选择：  
  
-   对于单个包中的即席使用，可以通过在脚本任务中编写代码来创建自定义任务，或通过在脚本组件中编写代码来创建可配置为源、转换或目标的自定义数据流组件。 这些功能强大的包装可为您编写基础结构代码，使您可将注意力集中于开发您自己的自定义功能；但这些代码较难在别处重用。  
  
-   对于在多个包中使用时，可以创建自定义 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 扩展插件，如连接管理器、任务、枚举器、日志提供程序和数据流组件。 托管 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型包含一些基类，这些基类可作为开发自定义扩展插件的基础，使开发更加方便。  
  
 如果要动态创建包，或在开发环境外管理并运行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包，则可以采用编程方式来操作包。 您不但可以加载、修改和运行现有包，还可以用编程方式创建和运行全新的包。 如果采用这种方法，则有一系列选择：  
  
-   加载和运行现有包，不进行修改。  
  
-   加载现有包，对其进行重新配置（例如，指定一个不同的数据源），然后运行。  
  
-   创建一个新包，添加并配置组件（逐个对象和属性进行更改），保存并运行。  
  
 本节介绍这些 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 编程方法，并用示例加以说明。  
  
## <a name="in-this-section"></a>本节内容  
 [Integration Services 编程概述](../integration-services/integration-services-programming-overview.md)  
 介绍 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 开发中的控制流和数据流的角色。  
  
 [了解同步和异步转换](../integration-services/understanding-synchronous-and-asynchronous-transformations.md)  
 介绍同步输出与异步输出之间的重要差异以及在数据流中使用这些输出的组件。  
  
 [以编程方式使用连接管理器](../integration-services/working-with-connection-managers-programmatically.md)  
 列出的连接管理器可以使用从托管代码，以及在连接管理器时，该代码调用返回的值**AcquireConnection**方法。  
  
 [用脚本扩展包](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 介绍如何使用脚本任务扩展控制流或使用脚本组件扩展数据流。  
  
 [用自定义对象扩展包](../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 介绍在多个包中使用时，如何创建自定义任务、数据流组件和其他包对象以及如何进行相关的编程。  
  
 [以编程方式生成包](../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 介绍如何以编程方式创建、配置和保存 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
 [以编程方式运行和管理包](../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 介绍如何以编程方式枚举、运行和管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
## <a name="reference"></a>参考  
 [Integration Services 错误和消息引用](../integration-services/integration-services-error-and-message-reference.md)  
 列出预定义[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]错误代码，以及它们的符号名称和说明。  
  
## <a name="related-sections"></a>相关章节  
 [包开发的疑难解答工具](../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
 介绍 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供的用于在开发过程中对包进行故障排除的功能和工具。  
  
## <a name="external-resources"></a>外部资源  
  
-   CodePlex 示例[Integration Services 产品示例](http://go.microsoft.com/fwlink/?LinkID=131204)，www.codeplex.com/MSFTISProdSamples 上  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
  
  