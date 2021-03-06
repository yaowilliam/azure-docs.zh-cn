---
title: 将证书添加到 Java CA 存储
description: 了解如何将证书颁发机构 (CA) 证书添加到 Twilio 服务或 Azure 服务总线的 Java CA 证书 (cacerts) 存储。
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/11/2018
ms.author: robmcm
ms.openlocfilehash: 1c432aa9da9637675262313d935edd38bd7b698b
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="adding-a-certificate-to-the-java-ca-certificates-store"></a>将证书添加到 Java CA 证书存储
以下步骤演示如何将证书颁发机构 (CA) 证书添加到 Java CA 证书 (cacerts) 存储。 使用的示例适用于 Twilio 服务所需的 CA 证书。 本主题中稍后提供的信息介绍如何安装 Azure 服务总线的 CA 证书。 

可以在压缩 JDK 并将其添加到 Azure 项目的 **approot** 文件夹之前使用 keytool 来添加 CA 证书，也可以运行使用 keytool 的启动任务来添加证书。 （此示例假设在压缩 JDK 之前添加 CA 证书。）此示例中还将使用一个特定 CA 证书，但获取其他 CA 证书并将其导入 cacerts 存储的步骤将类似。

## <a name="to-add-a-certificate-to-the-cacerts-store"></a>将证书添加到 cacerts 存储
1. 在设置为 JDK 的 **jdk\jre\lib\security** 文件夹的管理员命令提示符下，运行以下命令可查看将安装的证书：
   
    `keytool -list -keystore cacerts`
   
    系统会提示输入存储密码。 默认密码为 **changeit**。 （如果想更改密码，请参阅位于 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html> 的 keytool 文档。）此示例假定 MD5 指纹为 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 的证书未列出，并且你想要导入该证书（这是 Twilio API 服务所需的特定证书）。
2. 获取 [GeoTrust 根证书](http://www.geotrust.com/resources/root-certificates/)上列出的证书列表中的证书。 右键单击序列号为 35:DE:F4:CF 的证书的链接，并将该证书保存到 **jdk\jre\lib\security** 文件夹。 在此示例中，该证书已保存到名为 **Equifax\_Secure\_Certificate\_Authority.cer** 的文件。
3. 通过以下命令导入证书：
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    当系统提示信任 MD5 指纹为 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 的证书时，通过键入 **y** 进行响应。
4. 运行以下命令可确保已成功导入 CA 证书：
   
    `keytool -list -keystore cacerts`
5. 压缩 JDK 并将其添加到 Azure 项目的 **approot** 文件夹。

有关 keytool 的信息，请参阅 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>。

## <a name="azure-root-certificates"></a>Azure 根证书
使用 Azure 服务（如 Azure Service Bus）的应用程序需要信任 Baltimore CyberTrust 根证书。 （Azure 已在 2013 年 4 月 15 日开始从 GTE CyberTrust 全局根迁移到 Baltimore CyberTrust 根。 完成这种迁移花费了几个月的时间。）

Baltimore 证书可能已安装到 cacerts 存储中，因此请务必先运行 **keytool -list** 命令来查看它是否已存在。

如果需要添加 Baltimore CyberTrust 根，它具有序列号 02:00:00:b9 和 SHA1 指纹 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74。 可以从 <https://cacert.omniroot.com/bc2025.crt> 下载它，将其保存到扩展名为 **.cer** 的一个本地文件，然后使用 **keytool** 将其导入，如前面的步骤中所示。

## <a name="next-steps"></a>后续步骤
有关 Azure 使用的根证书的详细信息，请参阅 [Azure 根证书迁移](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx)。

有关 Java 的详细信息，请参阅[面向 Java 开发人员的 Azure](/java/azure)。

