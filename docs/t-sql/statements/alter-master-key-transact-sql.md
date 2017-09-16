---
title: "ALTER MASTER KEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER MASTER KEY
- ALTER_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- ALTER MASTER KEY statement
- decryption [SQL Server], Database Master Key
- FORCE option
- encryption [SQL Server], Database Master Key
- database master key [SQL Server], modifying
- cryptography [SQL Server], Database Master Key
- modifying Database Master Key
- service master key [SQL Server], modifying
- DROP ENCRYPTION BY SERVICE MASTER KEY phrase
ms.assetid: 8ac501c3-4280-4d5b-b58a-1524fa715b50
caps.latest.revision: 49
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 638449f85daf7b13abc37c5750eb32ec5603d7ef
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-master-key-transact-sql"></a>ALTER MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  更改数据库主密钥的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Database
-- Note: DROP ENCRYPTION BY SERVICE MASTER KEY is not supported on Azure SQL Database.
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD ='password'<encryption_option> ::=  
    ADD ENCRYPTION BY SERVICE MASTER KEY   
    |   
    DROP ENCRYPTION BY SERVICE MASTER KEY  
```  
  
## <a name="arguments"></a>参数  
 密码 =*密码*  
 指定用于加密或解密数据库主密钥的密码。 *密码*必须符合 Windows 密码策略要求的计算机的运行的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="remarks"></a>注释  
 可使用 REGENERATE 选项重新创建数据库主密钥和所有受该主密钥保护的密钥。 首先使用旧的主密钥对这些密钥进行解密，然后使用新的主密钥对它们进行加密。 在不危及主密钥安全性的前提下，应当将这种大量消耗资源的操作安排在资源需求较低的时段执行。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 使用 AES-256 加密算法来保护服务主密钥 (SMK) 和数据库主密钥 (DMK)。 AES 是一种比早期版本中使用的 3DES 更新的加密算法。 在将[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例升级到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 后，应重新生成 SMK 和 DMK 以便将主密钥升级到 AES。 有关重新生成 SMK 的详细信息，请参阅[ALTER SERVICE MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md).  
  
 当使用 FORCE 选项时，即使主密钥不可用，或者服务器不能对所有加密的私钥进行解密，该密钥重新生成的过程也会继续执行。 如果无法打开主密钥，使用[RESTORE MASTER KEY](../../t-sql/statements/restore-master-key-transact-sql.md)语句从备份还原主密钥。 请仅在主密钥无法恢复或解密失败时，才使用 FORCE 选项。 仅由不可恢复密钥加密的信息将会丢失。  
  
 使用 DROP ENCRYPTION BY SERVICE MASTER KEY 选项，可以删除通过服务主密钥对数据库主密钥的加密。  
  
 使用 ADD ENCRYPTION BY SERVICE MASTER KEY，可以通过服务主密钥对主密钥的副本进行加密，然后将副本存储在当前数据库和 master 中。  
  
## <a name="permissions"></a>Permissions  
 要求对数据库具有 CONTROL 权限。 如果已使用密码对数据库主密钥进行了加密，则还需要了解该密码的相关信息。  
  
## <a name="examples"></a>示例  
 以下示例为 `AdventureWorks` 创建新的数据库主密钥，并且重新加密在加密层次结构中位于该主密钥之下的密钥。  
  
```  
USE AdventureWorks2012;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例创建新数据库主密钥的`AdventureWorksPDW2012`并重新对它下面加密层次结构中的密钥进行加密。  
  
```  
USE master;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [打开主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [关闭 MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [备份主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [还原 MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [删除 MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

