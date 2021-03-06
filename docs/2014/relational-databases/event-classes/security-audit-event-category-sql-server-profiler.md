---
title: “安全审核”事件类别 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f2f854c7a6dbd0d1ab569f87bf053a5b9f45058
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63044206"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Security Audit 事件类别 (SQL Server Profiler)
  **Security Audit** 事件类别包含安全审核事件。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[Audit Add DB User 事件类](audit-add-db-user-event-class.md)|指示已在数据库中添加或删除作为数据库用户的登录名。|  
|[Audit Add Login to Server Role 事件类](audit-add-login-to-server-role-event-class.md)|指示已在固定服务器角色中添加或删除登录名。|  
|[Audit Add Member to DB Role 事件类](audit-add-member-to-db-role-event-class.md)|指示已在角色中添加或删除登录名。|  
|[Audit Add Role 事件类](audit-add-role-event-class.md)|指示已在数据库中添加或删除数据库角色。|  
|[Audit Addlogin 事件类](audit-addlogin-event-class.md)|指示已添加或删除登录名。|  
|[Audit App Role Change Password 事件类](audit-app-role-change-password-event-class.md)|指示已针对应用程序角色更改密码。|  
|[审核备份和还原事件类](audit-backup-and-restore-event-class.md)|指示已发出备份或还原语句。|  
|[Audit Broker Conversation 事件类](broker-conversation-event-class.md)|报告与 Service Broker 对话安全性相关的审核消息。|  
|[Audit Broker Login 事件类](audit-broker-login-event-class.md)|报告与 Service Broker 传输安全性相关的审核消息。|  
|[Audit Change Audit 事件类](audit-change-audit-event-class.md)|指示已进行审核跟踪修改。|  
|[Audit Change Database Owner 事件类](audit-change-database-owner-event-class.md)|指示已检查更改数据库所有者的权限。|  
|[Audit Database Management 事件类](audit-database-management-event-class.md)|指示已创建、更改或删除数据库。|  
|[Audit Database Mirroring Login 事件类](audit-database-mirroring-login-event-class.md)|报告与数据库镜像传输安全性相关的审核消息。|  
|[Audit Database Object Access 事件类](audit-database-object-access-event-class.md)|指示已访问数据库对象（如架构）。|  
|[Audit Database Object GDR 事件类](audit-database-object-gdr-event-class.md)|指示已发生数据库对象的 GDR 事件。|  
|[Audit Database Object Management 事件类](audit-database-object-management-event-class.md)|指示已针对数据库对象执行 CREATE、ALTER 或 DROP 语句。|  
|[Audit Database Object Take Ownership 事件类](audit-database-object-take-ownership-event-class.md)|指示已在数据库范围中更改对象所有者。|  
|[Audit Database Operation 事件类](audit-database-operation-event-class.md)|指示已发生各种操作（如检查点操作或订阅查询通知）。|  
|[Audit Database Principal Impersonation 事件类](audit-database-principal-impersonation-event-class.md)|指示已在数据库范围中发生模拟。|  
|[Audit Database Principal Management 事件类](audit-database-principal-management-event-class.md)|指示已在数据库中创建、更改或删除主体。|  
|[Audit Database Scope GDR 事件类](audit-database-scope-gdr-event-class.md)|指示在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中用户已针对语句权限发出 GRANT、REVOKE 或 DENY。|  
|[Audit DBCC 事件类](audit-dbcc-event-class.md)|指示已发出 DBCC 命令。|  
|[审核全文事件类](audit-fulltext-event-class.md)|指示全文事件已发生。|  
|[Audit Login Change Password 事件类](audit-login-change-password-event-class.md)|指示用户已更改其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录密码。|  
|[Audit Login Change Property 事件类](audit-login-change-property-event-class.md)|指示已使用 **sp_defaultdb**、 **sp_defaultlanguage**或 ALTER LOGIN 修改登录属性。|  
|[Audit Login 事件类](audit-login-event-class.md)|指示用户已成功登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|[Audit Login Failed 事件类](audit-login-failed-event-class.md)|指示用户尝试登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，但是失败。|  
|[Audit Login GDR 事件类](audit-login-gdr-event-class.md)|指示已添加或删除 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录权限。|  
|[Audit Logout 事件类](audit-logout-event-class.md)|指示用户已注销 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|[Audit Object Derived Permission 事件类](audit-object-derived-permission-event-class.md)|指示已针对对象发出 CREATE、ALTER 或 DROP。|  
|[Audit Schema Object Access 事件类](audit-schema-object-access-event-class.md)|指示已使用对象权限（如 SELECT）。|  
|[Audit Schema Object GDR 事件类](audit-schema-object-gdr-event-class.md)|指示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中用户已针对架构对象权限发出 GRANT、REVOKE 或 DENY。|  
|[Audit Schema Object Management 事件类](audit-schema-object-management-event-class.md)|指示已创建、更改或删除服务器对象。|  
|[Audit Schema Object Take Ownership 事件类](audit-schema-object-take-ownership-event-class.md)|指示已检查更改架构对象所有者的权限。|  
|[Audit Server Alter Trace 事件类](audit-server-alter-trace-event-class.md)|指示已检查 ALTER TRACE 权限。|  
|[Audit Server Object GDR 事件类](audit-server-object-gdr-event-class.md)|指示已发生架构对象的 GDR 事件。|  
|[Audit Server Object Management 事件类](audit-server-object-management-event-class.md)|指示已针对服务器对象发生 CREATE、ALTER 或 DROP 事件。|  
|[Audit Server Object Take Ownership 事件类](audit-server-object-take-ownership-event-class.md)|指示已更改服务器对象所有者。|  
|[Audit Server Operation 事件类](audit-server-operation-event-class.md)|指示已在服务器中发生审核操作。|  
|[Audit Server Principal Impersonation 事件类](audit-server-principal-impersonation-event-class.md)|指示已在服务器范围中发生模拟。|  
|[Audit Server Principal Management 事件类](audit-server-principal-management-event-class.md)|指示已针对服务器主体发生 CREATE、ALTER 或 DROP。|  
|[Audit Server Scope GDR 事件类](audit-server-scope-gdr-event-class.md)|指示已针对服务器权限发生 GDR 事件。|  
|[Audit Server Starts and Stops 事件类](audit-server-starts-and-stops-event-class.md)|指示已修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务状态。|  
|[Audit Statement Permission 事件类](audit-statement-permission-event-class.md)|指示已使用语句权限。|  
  
## <a name="related-content"></a>相关内容  
 [扩展事件](../extended-events/extended-events.md)  
  
  
