---
title: 查看可用性组属性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server]
ms.assetid: 61243c87-bd62-4510-863f-2a8f347caf1f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 102b3defa150707412012d506e0e9e542d80b9a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813240"
---
# <a name="view-availability-group-properties-sql-server"></a>查看可用性组属性 (SQL Server)
  本主题说明如何通过使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]查看 AlwaysOn 可用性组的属性。  
  

  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **查看和更改可用性组的属性**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  右键单击要查看其属性的可用性组，然后选择“属性”命令。  
  
4.  在 **“可用性组属性”** 对话框中，使用 **“常规”** 和 **“备份首选项”** 页查看所选可用性组的属性，在某些情况下，还可以更改这些属性。 有关详细信息，请参阅[可用性组属性和新的可用性组&#40;常规页&#41;](availability-group-properties-new-availability-group-general-page.md)并[可用性组属性：新的可用性组&#40;备份首选项页&#41;](availability-group-properties-new-availability-group-backup-preferences-page.md)。  
  
     使用 **“权限”** 页可以查看当前登录名、角色以及与可用性组关联的显式权限。 有关详细信息，请参阅 [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md)。  
  

  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **查看可用性组的属性和状态**  
  
 若要查询服务器实例为其承载可用性副本的可用性组的属性和状态，请使用以下视图：  
  
 [sys.availability_groups](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的本地实例承载其可用性副本的每个可用性组返回一行。 每一行都包含可用性组元数据的缓存的副本。  
  
 **列名：** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](/sql/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql)  
 为 WSFC 群集中的每个可用性组返回一行。 每一行均包含 Windows Server 故障转移群集 (WSFC) 群集中的可用性组元数据。  
  
 **列名：** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
 为在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的本地实例上拥有可用性副本的每个可用性组返回一行。 每行显示定义给定可用性组的运行状况的状态。  
  
 **列名：** group_id、primary_replica、primary_recovery_health、primary_recovery_health_desc、secondary_recovery_health、secondary_recovery_health_desc、synchronization_health、synchronization_health_desc  
  

  
##  <a name="RelatedTasks"></a> 相关任务  
 **查看有关可用性组的信息**  
  
-   [查看可用性副本属性 (SQL Server)](view-availability-replica-properties-sql-server.md)  
  
-   [查看可用性组侦听程序属性 (SQL Server)](view-availability-group-listener-properties-sql-server.md)  
  
-   [针对 AlwaysOn 可用性组运行问题的 AlwaysOn 策略&#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)
  
-   [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [监视可用性组 (Transact-SQL)](monitor-availability-groups-transact-sql.md)  
  
 **配置现有的可用性组**  
  
-   [将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [将次要副本从可用性组删除 (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)  
  
-   [将辅助数据库从可用性组删除 (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [删除可用性组侦听程序 (SQL Server)](remove-an-availability-group-listener-sql-server.md)  
  
-   [将主数据库从可用性组删除 (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [删除可用性组 (SQL Server)](remove-an-availability-group-sql-server.md)  
  
 **对可用性组执行手动故障转移**  
  
-   [执行可用性组的计划手动故障转移 (SQL Server)](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [执行可用性组的强制手动故障转移 (SQL Server)](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  

  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41; ](overview-of-always-on-availability-groups-sql-server.md) [监视可用性组&#40;TRANSACT-SQL&#41; ](monitor-availability-groups-transact-sql.md) [针对运行问题的 AlwaysOn 的 AlwaysOn 策略可用性组&#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md) 
  
  
