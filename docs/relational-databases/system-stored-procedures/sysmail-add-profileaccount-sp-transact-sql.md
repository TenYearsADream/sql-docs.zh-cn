---
title: sysmail_add_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44dc2d5341e536179fe0bf6ef152ef7d39afe966
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532099"
---
# <a name="sysmailaddprofileaccountsp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在数据库邮件配置文件中添加一个数据库邮件帐户。 执行**sysmail_add_profileaccount_sp**使用创建数据库帐户后[sysmail_add_account_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)，并使用创建数据库配置文件[sysmail_add_profile_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>参数  
`[ @profile_id = ] profile_id` 若要将帐户添加到配置文件 id。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @profile_name = ] 'profile_name'` 若要将帐户添加到配置文件名称。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @account_id = ] account_id` 要添加到配置文件的帐户 id。 *account_id*是**int**，默认值为 NULL。 任一*account_id*或*account_name*必须指定。  
  
`[ @account_name = ] 'account_name'` 要添加到配置文件的帐户的名称。 *account_name*是**sysname**，默认值为 NULL。 任一*account_id*或*account_name*必须指定。  
  
`[ @sequence_number = ] sequence_number` 配置文件中帐户的序列号。 *sequence_number*是**int**，无默认值。 序列号可以确定帐户在配置文件中的使用顺序。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 配置文件和帐户都必须已经存在。 否则，存储过程将返回错误。  
  
 请注意，此存储过程不会更改已与指定的配置文件关联的帐户的序列号。 有关更新的帐户的序列号的详细信息，请参阅[sysmail_update_profileaccount_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)。  
  
 序列号可以确定数据库邮件使用配置文件中帐户的顺序。 对于新的电子邮件，数据库邮件将从序列号最小的帐户开始。 如果该帐户失败，数据库邮件就使用具有下一个序列号较大的帐户，依此类推，直到数据库邮件成功发送邮件，或者序列号最大的帐户也失败为止。 如果序列号最大的帐户失败，数据库邮件将暂停尝试发送邮件，暂停时间在 *sysmail_configure_sp* 的 **AccountRetryDelay**参数中配置，然后从最小序列号再次开始尝试发送邮件的过程。 使用 *sysmail_configure_sp* 的 **AccountRetryAttempts**参数可以配置外部邮件进程尝试使用指定配置文件中的每个帐户发送电子邮件的次数。  
  
 如果存在具有相同序列号的多个帐户，则数据库邮件将只使用这些帐户中的某一个来处理给定的电子邮件。 在此情况下，数据库邮件不能保证使用具有该序列号的特定帐户，也不能保证使用同一个帐户发送各个邮件。  
  
 存储的过程**sysmail_add_profileaccount_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将配置文件 `AdventureWorks Administrator` 与帐户 `Audit Account` 关联。 审核帐户的序列号为 1。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
