---
title: 通过表达式访问自定义程序集 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ba5d3ec6958cf3dbc3cca0497f08feaac094b837
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265117"
---
# <a name="accessing-custom-assemblies-through-expressions"></a>通过表达式访问自定义程序集
  在创建自定义程序集、使其可用于报表设计器或报表服务器、添加适当的安全策略以及在报表定义中添加对自定义程序集的引用之后，您就可以使用报表表达式访问程序集中类的成员。 若要在表达式中引用自定义代码，您必须调用程序集中某个类的成员。 调用方式取决于该方法是静态方法还是基于实例的方法。  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>从报表定义文件调用静态成员  
 静态成员属于类或类型本身，而不属于实例化的对象。 可以通过从类中调用这些成员直接访问它们。 应尽可能使用静态成员在报表中调用自定义函数，因为静态成员的效果最佳。 若要调用某个静态成员，需要将其作为表达式（采用 =Namespace.Class.Method 格式）进行引用。  
  
#### <a name="to-call-static-members"></a>调用静态成员  
  
-   若要调用静态成员，请将表达式设置为等于成员的完全限定名称（包括命名空间、类名称和成员名称）。 以下示例调用“ToGBP”方法，该方法将“StandardCost”字段值从美元转换为英镑并在报表中显示该值：  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>有关静态字段和属性的重要信息  
 目前，所有报表都在同一个应用程序域中执行。 这意味着具有用户特定的静态数据的报表将向同一报表的其他实例公开此数据。 这种情况可能会使一个用户的静态数据可用于当前运行特定报表的所有用户。 因此，强烈建议不要在自定义程序集或“Code”元素中使用静态字段或属性；而是在报表中使用实例字段或属性。 仍可以使用静态方法，因为它们不存储状态或数据。  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>从报表定义文件调用实例成员  
 如果您的自定义程序集包含您在报表定义中需要访问的实例成员，则必须将类的实例名称添加到报表中。 可以使用“报表属性”对话框中的“代码”选项卡添加类的实例名称。 有关向报表添加类的实例的详细信息，请参阅[报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
 若要调用某个静态成员，需要将其作为表达式（采用 =Code.InstanceName.Method 格式）进行引用。  
  
#### <a name="to-call-instance-members"></a>调用实例成员  
  
-   若要调用自定义程序集的实例成员，必须引用“Code”关键字，后跟实例名称和方法。 以下示例调用实例方法“ToEUR”，该方法将“StandardCost”字段值从美元转换为欧元并在报表中显示该值：  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>请参阅  
 [将自定义程序集用于报表](using-custom-assemblies-with-reports.md)  
  
  
