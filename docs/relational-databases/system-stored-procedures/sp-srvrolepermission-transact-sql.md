---
title: sp_srvrolepermission (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_srvrolepermission_TSQL
- sp_srvrolepermission
dev_langs:
- TSQL
helpviewer_keywords:
- sp_srvrolepermission
ms.assetid: 5709667f-e3e4-48a2-93ec-af5e22a2ac58
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: f23d8766a89619654ba89bc6d70cec342b11b8fe
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534637"
---
# <a name="spsrvrolepermission-transact-sql"></a>sp_srvrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示固定服务器角色的权限。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_srvrolepermission [ [ @srvrolename = ] 'role']  
```  
  
## <a name="arguments"></a>参数  
`[ @srvrolename = ] 'role'` 是为其返回权限的固定的服务器角色的名称。 *角色* 是 **sysname** ，默认值为 NULL。 如果未指定角色，则返回所有固定服务器角色的权限。 *角色*可以具有以下值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**sysadmin**|系统管理员|  
|**securityadmin**|安全管理员|  
|**serveradmin**|服务器管理员|  
|**setupadmin**|安装程序管理员|  
|**processadmin**|进程管理员|  
|**diskadmin**|磁盘管理员|  
|**dbcreator**|数据库创建者|  
|**bulkadmin**|可执行 BULK INSERT 语句|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**ServerRole**|**sysname**|固定服务器角色的名称|  
|**权限**|**sysname**|与关联的权限**ServerRole**|  
  
## <a name="remarks"></a>备注  
 列出的权限包括可以执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和固定服务器角色成员可执行的其他特殊活动。 若要显示固定的服务器角色的列表，请执行**sp_helpsrvrole**。  
  
 **Sysadmin**固定的服务器角色具有所有其他固定的服务器角色的权限。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下查询返回与 `sysadmin` 固定服务器角色关联的权限。  
  
```  
EXEC sp_srvrolepermission 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
