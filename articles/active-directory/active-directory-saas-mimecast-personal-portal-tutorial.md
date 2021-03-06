---
title: 教程：Azure Active Directory 与 Mimecast Personal Portal 的集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 Mimecast Personal Portal 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2018
ms.author: jeedes
ms.openlocfilehash: 4b976481e60926e6ab95a679e6dcc8aa0818b48b
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>教程：Azure Active Directory 与 Mimecast Personal Portal 的集成

本教程介绍如何将 Mimecast Personal Portal 与 Azure Active Directory (Azure AD) 集成。

将 Mimecast Personal Portal 与 Azure AD 集成提供以下优势：

- 可在 Azure AD 中控制谁有权访问 Mimecast Personal Portal。
- 可以让用户使用其 Azure AD 帐户自动登录到 Mimecast Personal Portal（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Mimecast Personal Portal 的集成，需要以下项：

- Azure AD 订阅
- 启用了 Mimecast Personal Portal 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Mimecast Personal Portal
2. 配置和测试 Azure AD 单一登录

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a>从库中添加 Mimecast Personal Portal
要配置 Mimecast Personal Portal 与 Azure AD 的集成，需要从库中将 Mimecast Personal Portal 添加到托管 SaaS 应用列表。

若要从库中添加 Mimecast Personal Portal，请执行以下步骤：

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]
    
3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

4. 在搜索框中键入 Mimecast Personal Portal，在结果面板中选择“Mimecast Personal Portal”，并单击“添加”按钮添加该应用程序。

    ![结果列表中的 Mimecast Personal Portal](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，将基于名为“Britta Simon”的测试用户配置和测试 Mimecast Personal Portal 的 Azure AD 单一登录。

为使单一登录能正常工作，Azure AD 需要知道与 Azure AD 用户相对应的 Mimecast Personal Portal 用户。 换句话说，需要在 Azure AD 用户与 Mimecast Personal Portal 中相关用户之间建立链接关系。

若要配置和测试 Mimecast Personal Portal 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. [创建 Mimecast Personal Portal 测试用户](#create-a-mimecast-personal-portal-test-user) - 在 Mimecast Personal Portal 中创建 Britta Simon 的对应用户，将其链接到用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Mimecast Personal Portal 应用程序中配置单一登录。

若要配置 Mimecast Personal Portal 的 Azure AD 单一登录，请执行以下步骤：

1. 在 Azure 门户中的“Mimecast Personal Portal”应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![“单一登录”对话框](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. 在“Mimecast Personal Portal 域和 URL”部分中，执行以下步骤：

    ![Mimecast Personal Portal 域和 URL 单一登录信息](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. 在“登录 URL”文本框中，键入 URL： 

    | 区域  |  值 | 
    | --------------- | --------------- | 
    | 欧洲          | `https://eu-api.mimecast.com/login/saml`|
    | 美国   | `https://us-api.mimecast.com/login/saml`|
    | 南非    | `https://za-api.mimecast.com/login/saml`|
    | 澳大利亚       | `https://au-api.mimecast.com/login/saml`|
    | 海外        | `https://jer-api.mimecast.com/login/saml`|

    b. 在“标识符”文本框中，使用以下模式键入 URL：

    | 区域  |  值 | 
    | --------------- | --------------- |
    | 欧洲          | `https://eu-api.mimecast.com/sso/<accountcode>`|
    | 美国   | `https://us-api.mimecast.com/sso/<accountcode>`|    
    | 南非    | `https://za-api.mimecast.com/sso/<accountcode>`|
    | 澳大利亚       | `https://au-api.mimecast.com/sso/<accountcode>`|
    | 海外        | `https://jer-api.mimecast.com/sso/<accountcode>`|

    c. 在“回复 URL”文本框中键入 URL： 

    | 区域  |  值 | 
    | --------------- | --------------- | 
    | 欧洲          | `https://eu-api.mimecast.com/login/saml`|
    | 美国   | `https://us-api.mimecast.com/login/saml`|
    | 南非    | `https://za-api.mimecast.com/login/saml`|
    | 澳大利亚       | `https://au-api.mimecast.com/login/saml`|
    | 海外        | `https://jer-api.mimecast.com/login/saml`|
    
    > [!NOTE] 
    > 标识符非实际值。 请使用实际标识符更新此值。 请联系 [Mimecast Personal Portal 客户端支持团队](http://www.mimecast.com/customer-success/technical-support/)来获取这些值。 

4. 在“SAML 签名证书”部分中，单击“证书(base64)”，并在计算机上保存证书文件。

    ![证书下载链接](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. 单击“保存”按钮。

    ![配置单一登录“保存”按钮](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. 在“Mimecast Personal Portal 配置”部分中，单击“配置 Mimecast Personal Portal”以打开“配置登录”窗口。 从“快速参考”部分中复制“注销 URL”、“SAML 实体 ID”和“SAML 单一登录服务 URL”。

    ![Mimecast Personal Portal 配置](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. 在另一个 Web 浏览器窗口中，以管理员身份登录到 Mimecast Personal Portal。

8. 转到“服务”\>“应用程序”。
   
    ![应用程序](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "应用程序")

9. 单击“身份验证配置文件”。
   
    ![身份验证配置文件](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "身份验证配置文件")

10. 单击“新建身份验证配置文件”。
   
    ![新建身份验证配置文件](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "新建身份验证配置文件")

11. 在“身份验证配置文件”部分中，执行以下步骤：
   
    ![身份验证配置文件](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "身份验证配置文件")
   
    a. 在“描述”文本框中，键入配置名称。
   
    b. 选择“对 Mimecast Personal Portal 强制实施 SAML 身份验证”。
   
    c. 对于“提供程序”，选择“Azure Active Directory”。
   
    d. 在“颁发者 URL”文本框中，粘贴从 Azure 门户复制的“SAML 实体 ID”的值。
   
    e. 在“登录 URL”文本框中，粘贴从 Azure 门户复制的“SAML 单一登录服务 URL”的值。
   
    f. 在“注销 URL”文本框中，粘贴从 Azure 门户复制的“注销 URL”的值。

    g. 在记事本中打开从 Azure 门户下载的“base-64”编码证书，将其内容复制到剪贴板，然后再粘贴到“标识提供者证书（元数据）”文本框。

    h. 选择“允许单一登录”。
   
    i. 单击“ **保存**”。

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

   ![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png)

2. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。

    ![“用户和组”以及“所有用户”链接](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png)

3. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。

    ![“添加”按钮](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png)

4. 在“用户”对话框中，执行以下步骤：

    ![“用户”对话框](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png)

    a. 在“姓名”框中，键入“BrittaSimon”。

    b. 在“用户名”框中，键入用户 Britta Simon 的电子邮件地址。

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。
 
### <a name="create-a-mimecast-personal-portal-test-user"></a>创建 Mimecast Personal Portal 测试用户

为了使 Azure AD 用户能够登录到 Mimecast Personal Portal，必须将其预配到 Mimecast Personal Portal 中。 对于 Mimecast Personal Portal，需要手动执行预配。

需要注册一个域，才能创建用户。

**若要配置用户预配，请执行以下步骤：**

1. 以管理员身份登录到 **Mimecast Personal Portal**。

2. 转到“目录”\>“内部”。
   
    ![目录](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "目录")

3. 单击“注册新域”。
   
    ![注册新域](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "注册新域")

4. 在创建新域后，单击“新建地址”。
   
    ![新建地址](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "新建地址")

5. 在“新建地址”对话框中，对要预配的有效 Azure AD 帐户执行下列步骤：
   
    ![保存](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "保存")
   
    a. 在“电子邮件地址”文本框中，将用户的“电子邮件地址”键入为“BrittaSimon@contoso.com”。
    
    b. 在“全局名称”文本框中，将“用户名”键入为“BrittaSimon”。

    c. 在“密码”和“确认密码”文本框中，键入用户的“密码”。
   
    b. 单击“ **保存**”。

>[!NOTE]
>可以使用 Mimecast Personal Portal 提供的任何其他 Mimecast Personal Portal 用户帐户创建工具或 API 来预配 Azure AD 用户帐户。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Mimecast Personal Portal 的权限，允许她使用 Azure 单一登录。

![分配用户角色][200] 

要将 Britta Simon 分配到 Mimecast Personal Portal，请执行以下步骤：

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

2. 在应用程序列表中，选择“Mimecast Personal Portal”。

    ![应用程序列表中的“Mimecast Personal Portal”链接](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png)  

3. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202]

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

单击访问面板中的“Mimecast Personal Portal”磁贴时，用户应自动登录到 Mimecast Personal Portal 应用程序。
有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)（访问面板简介）。 

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](active-directory-saas-tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

