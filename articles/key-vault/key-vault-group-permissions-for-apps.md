---
title: 为多个应用程序授予 Azure 密钥保管库的访问权限 | Microsoft Docs
description: 了解如何为多个应用程序授予密钥保管库的访问权限
services: key-vault
documentationcenter: ''
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: ddeaf184138bd48d324799ddb45248b0a0ee8eeb
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a>为多个应用程序授予密钥保管库的访问权限

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>问：我有多个（超过 16 个）应用程序需要访问密钥保管库。 由于密钥保管库只允许 16 个访问控制条目，我应如何实现此操作？

密钥保管库的访问控制策略仅支持 16 个条目。 但是，可以创建一个 Azure Active Directory 安全组。 将所有关联的服务主体添加到此安全组，并为此安全组授予密钥保管库的访问权限。

以下是先决条件：
* [安装 Azure Active Directory V2 PowerShell 模块](https://www.powershellgallery.com/packages/AzureAD)。
* [安装 Azure PowerShell](/powershell/azure/overview)。
* 若要运行以下命令，需要具有在 Azure Active Directory 租户中创建/编辑组的权限。 如果没有权限，则可能需要与 Azure Active Directory 管理员联系。

接下来，在 PowerShell 中运行以下命令。

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionsToKeys all –PermissionsToSecrets all –PermissionsToCertificates all 
 
# Of course you can adjust the permissions as required 
```

如果需要为一组应用程序授予一组不同的权限，请为此类应用程序创建单独的 Azure Active Directory 安全组。

## <a name="next-steps"></a>后续步骤

深入了解如何[保护密钥保管库](key-vault-secure-your-key-vault.md)。
