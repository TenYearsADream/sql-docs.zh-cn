---
title: 运行 SQL Server Profiler |Microsoft Docs
ms.custom: ''
ms.date: 07/07/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ef08bcecf3bf5478a8e6d076f8bed0d25e91754
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012968"
---
# <a name="run-sql-server-profiler"></a>运行 SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以通过多种方法运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，以支持在各种情况下收集跟踪输出。 启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的方法包括：从 Windows 10“开始”菜单启动、从[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问中的“工具”菜单启动以及从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的多个位置启动。  
  
首次启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 并从“文件”菜单中选择“新建跟踪”时，此应用程序将显示“连接到服务器”对话框，在该对话框中可以指定要连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>从 Windows 10“开始”菜单启动 SQL Server Profiler  
-  单击 Windows**启动**图标或按 Windows 键，并开始键入"SQL Server Profiler 17"。 当**SQL Server Profiler 17**磁贴时，请单击它。   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>在数据库引擎优化顾问中启动 SQL Server Profiler  
-  在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问的 **“工具”** 菜单上，单击 **SQL Server Profiler**。  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 启动 SQL Server Profiler  
 可以启动[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]从多个位置中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 在启动时将加载连接上下文、跟踪模板及其启动点的筛选上下文。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 启动的每个 SQL Server Profiler 会话处于自己的实例，并继续运行，如果你关闭 Profiler [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>从“工具”菜单启动 SQL Server Profiler  
-  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的“工具”菜单中，单击“SQL Server Profiler”。  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>从查询编辑器启动 SQL Server Profiler  
- 在查询编辑器中右键单击，然后选择“在 SQL Server Profiler 中跟踪查询” 。  

  > [!NOTE]  
  >  该连接上下文为编辑器连接，跟踪模板为 TSQL_SPs，应用的筛选器为 SPID = query window SPID。  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>从活动监视器启动 SQL Server Profiler  
- 在活动监视器中，单击“进程”窗格，右键单击要探查的进程，然后单击“在 SQL Server Profiler 中跟踪进程”。  

    > [!NOTE]  
    >  选定某个进程后，打开活动监视器时连接上下文为对象资源管理器连接。 跟踪模板为基于服务器类型的默认模板，并且 SPID 等于所选进程的 SPID。  
    
## <a name="net-framework-security"></a>.NET Framework 安全性  
- 在 Windows 身份验证模式下，运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的用户帐户必须拥有连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的权限。  
- 若要使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]执行跟踪，用户还必须拥有 ALTER TRACE 权限。  

## <a name="next-steps"></a>后续步骤  
 [SQL Server Profiler 概述](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [使用 SQL Server Management Studio](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
