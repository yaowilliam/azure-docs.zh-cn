---
title: "Android 上 Azure Active Directory 基于证书的身份验证 | Microsoft Docs"
description: "了解 Android 设备的解决方案中配置基于证书的身份验证的支持方案和要求"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: mtillman
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 93fe73257378022a4e65f7e241d9a60056f403fb
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2018
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a>Android 上 Azure Active Directory 基于证书的身份验证


通过基于证书的身份验证 (CBA)，在 Windows、Android 或 iOS 设备上将 Exchange Online 帐户连接到以下对象时，可由 Azure Active Directory 使用客户端证书进行身份验证：

* Office 移动应用程序，例如 Microsoft Outlook 和 Microsoft Word   
* Exchange ActiveSync (EAS) 客户端

如果配置了此功能，就无需在移动设备上的某些邮件和 Microsoft Office 应用程序中输入用户名和密码组合。

本主题面向 Office 365 企业版、商业版、教育版、美国政府计划、中国计划和德国计划中的租户用户，提供在 iOS(Android) 设备上配置 CBA 时的要求和受支持方案。



此功能在 Office 365 US Government Defense 和 Federal 计划中以预览形式提供。


## <a name="microsoft-mobile-applications-support"></a>Microsoft 移动应用程序支持
| 应用 | 支持 |
| --- | --- |
| Azure 信息保护应用 |![勾选标记][1] |
| Intune 公司门户 |![勾选标记][1] |
| Microsoft Teams |![勾选标记][1] |
| OneNote |![勾选标记][1] |
| OneDrive |![勾选标记][1] |
| Outlook |![勾选标记][1] |
| Power BI |![勾选标记][1] |
| Skype for Business |![勾选标记][1] |
| Word/Excel/PowerPoint |![勾选标记][1] |
| Yammer |![勾选标记][1] |


### <a name="implementation-requirements"></a>实现要求

设备 OS 版本必须为 Android 5.0 (Lollipop) 及更高版本

必须配置联合服务器。  

若要让 Azure Active Directory 吊销客户端证书，ADFS 令牌必须具有以下声明：  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  （客户端证书的序列号）
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  （客户端证书颁发者的字符串）

如果 ADFS 令牌（或任何其他 SAML 令牌）具有这些声明，Azure Active Directory 会将这些声明添加到刷新令牌中。 当需要验证刷新令牌时，此信息可用于检查吊销。

作为最佳做法，应该使用有关如何获取用户证书的说明来更新 ADFS 错误页。  
有关更多详细信息，请参阅[自定义 AD FS 登录页面](https://technet.microsoft.com/library/dn280950.aspx)。  

某些 Office 应用（启用了新式身份验证）在请求中向 Azure AD 发送“*prompt=login*”。 默认情况下，Azure AD 会在请求中为 ADFS 将其转换为“*wauth=usernamepassworduri*”（要求 ADFS 执行 U/P 身份验证）和“*wfresh=0*”（要求 ADFS 忽略 SSO 状态并执行全新的身份验证）。 如果想要为这些应用启用基于证书的身份验证，需要修改默认 Azure AD 行为。 只需将联盟域设置中的“PromptLoginBehavior”设置为“已禁用”即可。
可使用 [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet 执行此任务：

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a>Exchange ActiveSync 客户端支持
支持 Android 5.0 (Lollipop) 或更高版本上的某些 Exchange ActiveSync 应用程序。 要确定电子邮件应用程序是否支持此功能，请联系应用程序开发人员。


## <a name="next-steps"></a>后续步骤

如果想要在环境中配置基于证书的身份验证，请参阅 [Android 上基于证书的身份验证入门](active-directory-certificate-based-authentication-get-started.md)了解相关说明。

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
