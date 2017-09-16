---
title: "PowerShell：使用自有 Azure Key Vault 密钥启用 TDE | Microsoft Docs"
description: "了解如何配置 Azure SQL 数据库和数据仓库，以开始使用透明数据加密 (TDE) 通过 PowerShell 进行静态加密。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: cf8f46ab01c08e68fa22f65a4f86f4ff16f16ba3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---


# <a name="powershell-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell：使用 Azure Key Vault 中的自有密钥启用透明数据加密

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

本操作指南介绍了如何使用 Azure Key Vault 的密钥在 SQL 数据库或数据仓库中进行透明数据加密 (TDE)。 若要了解更多有关使用自带密钥 (BYOK) 支持进行 TDE 的信息，请访问 [Azure SQL 的 TDE 自带密钥](transparent-data-encryption-byok-azure-sql.md)。 

## <a name="prerequisites"></a>先决条件

- 必须有 Azure 订阅，并且成为订阅中的管理员。
- [推荐但可选]具有硬件安全性模块 (HSM) 或本地密钥存储，用于创建 TDE 保护程序密钥材料的本地副本。
- 必须安装和运行 Azure PowerShell 版本 4.2.0 或更高版本。 
- 创建用于 TDE 的 Azure Key Vault 和密钥。
   - [密钥保管库中的 PowerShell 说明](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [有关使用硬件安全模块 (HSM) 和 Key Vault 的说明](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
- 密钥必须具有以下用于 TDE 的属性：
   - 无过期日期
   - 未禁用
   - 能够执行 get、wrap key 和 unwrap key 操作

## <a name="step-1-assign-an-aad-identity-to-your-server"></a>步骤 1. 将 AAD 标识分配给服务器 

如果具有现有服务器，执行以下步骤将 AAD 标识添加到服务器：

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

如果正在创建服务器，在服务器创建过程中使用带有标记标识的 [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) cmdlet 添加 AAD 标识：

   ```powershell
   $server = New-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -Location <RegionName> `
   -ServerName <LogicalServerName> `
   -ServerVersion "12.0" `
   -SqlAdministratorCredentials <PSCredential> `
   -AssignIdentity 
   ```

## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>步骤 2. 向服务器授予密钥保管库权限

将密钥保管库中的密钥用于 TDE 之前，使用 [Set-AzureRmKeyValutAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet 向服务器授予密钥保管库的访问权限。

   ```powershell
   Set-AzureRmKeyVaultAccessPolicy  `
   -VaultName <KeyVaultName> `
   -ObjectId $server.Identity.PrincipalId `
   -PermissionsToKeys get, wrapKey, unwrapKey
   ```

## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>步骤 3. 将 Key Vault 密钥添加到服务器，并设置 TDE 保护程序

- 使用 [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) cmdlet 将 Key Vault 的密钥添加到服务器。
- 使用 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet 将密钥设为所有服务器资源的 TDE 保护程序。
- 使用 [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) cmdlet 确认 TDE 保护程序已按照预期配置。

> [!Note]
> 密钥保管库名称和密钥名称的组合长度不能超过 94 个字符。
> 

>[!Tip]
>Key Vault 中的 KeyId 示例：https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>

   ```powershell
   <# Add the key from Key Vault to the server #>
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>

   <# Set the key as the TDE protector for all resources under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> 

   <# To confirm that the TDE protector was configured as intended: #>
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> 
   ```

## <a name="step-4-turn-on-tde"></a>步骤 4. 启用 TDE 

使用 [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) cmdlet 启用 TDE。

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `
   -State "Enabled"
   ```

现在数据库或数据仓库已使用 Key Vault 中的加密密钥启用了 TDE。

## <a name="step-5-check-the-encryption-state-and-encryption-activity-of-the-database-or-data-warehouse"></a>步骤 5. 检查数据库或数据仓库的加密状态和加密活动

使用 [Get AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) 获取加密状态，使用 [Get AzureRMSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) 检查数据库或数据仓库的加密过程。

   ```powershell
   # Get the encryption state
   Get-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `

   <# Check the encryption progress for a database or data warehouse #>
   Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName>  
   ```

## <a name="other-useful-powershell-cmdlets"></a>其他有用的 PowerShell cmdlet

- 使用 [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) cmdlet 可关闭 TDE。

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -DatabaseName <DatabaseName> `
   -State "Disabled”
   ```
 
- 使用 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) cmdlet 可返回已添加到服务器的 Key Vault 密钥的列表。

   ```powershell
   <# KeyId is an optional parameter, to return a specific key version #>
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```
 
- 使用 [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) 可从服务器删除 Key Vault 密钥。

   ```powershell
   <# The key set as the TDE Protector cannot be removed. #>
   Remove-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>   
   ```
 
## <a name="troubleshooting"></a>故障排除

如果发生问题，请检查以下内容：
- 如果不能找到密钥保管库，请使用 [Get-azurermsubscription](/powershell/module/azurerm.profile/get-azurermsubscription) cmdlet 确保在正确的订阅中。

   ```powershell
   Get-AzureRmSubscription `
   -SubscriptionId <SubscriptionId>
   ```

- 如果不能在服务器中添加新密钥，或新密钥不能随 TDE 保护程序更新，请检查以下内容：
   - 密钥不应有过期日期
   - 密钥必须已启用 get、wrap key 和 unwrap key 操作。

## <a name="next-steps"></a>后续步骤

- 了解如何轮换服务器的 TDE 保护程序以符合安全要求：[使用 PowerShell 轮换透明数据加密保护程序](transparent-data-encryption-byok-azure-sql-key-rotation.md)。
- 如果存在安全风险，了解如何删除可能已泄露的 TDE 保护程序：[删除可能已泄露的密钥](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)。 


