---
title: "StartMode 属性 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: StartMode Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2c999c38e41ccb370a1edfa182f987a90935709
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]获取服务的启动模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务模式的 uint32 值。  
  
 可以是下列值之一。  
  
 启动  
 值 = 0。 服务由操作系统加载程序启动。 此选项只对驱动程序服务有效。  
  
 系统  
 值 = 1。 通过启动服务**IoInitSystem**方法。 此选项只对驱动程序服务有效。  
  
 自动  
 值 = 2。 服务将在系统启动期间由服务控制管理器自动启动。  
  
 Manual  
 值 = 3。 服务启动的计算机管理器时的进程调用**StartService**方法。  
  
 禁用  
 值 = 4。 无法启动服务。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  