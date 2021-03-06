---
title: 使用 C# 创建 Azure Service Fabric Reliable Service
description: 使用 Visual Studio 创建、部署和调试基于 Azure Service Fabric 的 Reliable Services 应用程序。
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/14/2018
ms.author: ryanwi
ms.openlocfilehash: 7e64bc34f5c39edaf87cc732d7c4702655df0e3e
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2018
ms.locfileid: "34212664"
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>创建你的第一个 C# Service Fabric 有状态 Reliable Services 应用程序

了解如何在数分钟内在 Windows 上部署你的第一个适用于 .NET 的 Azure Service Fabric 应用程序。 完成后，你会有一个本地群集，与 Reliable Services 应用程序一起运行。

## <a name="prerequisites"></a>先决条件

开始之前，请确保已[设置开发环境](service-fabric-get-started.md)。 此过程包括安装 Service Fabric SDK 和 Visual Studio 2017 或 2015。

## <a name="create-the-application"></a>创建应用程序

1. 以管理员身份启动 Visual Studio。

2. 创建一个项目，方法是选择 Ctrl+Shift+N。

3. 在“新建项目”对话框中，选择“云” > “Service Fabric 应用程序”。

4. 将应用程序命名为“MyApplication”， 然后选择“确定”。

   ![Visual Studio 中的“新建项目”对话框][1]

5. 可以在下一对话框中创建任何类型的 Service Fabric 应用程序。 对于本快速入门，请选择“.Net Core 2.0” > “有状态服务”。

6. 将服务命名为“MyStatefulService”， 然后选择“确定”。

    ![Visual Studio 中的“新建服务”对话框][2]

    Visual Studio 会创建应用程序项目和有状态服务项目， 然后在解决方案资源管理器中显示它们。

    ![创建使用有状态服务的应用程序之后的解决方案资源管理器][3]

    应用程序项目 (MyApplication) 没有任何代码。 而是引用一组服务项目。 它还有三个其他类型的内容：

    * 发布配置文件  
    部署到不同环境所需的配置文件。

    * 脚本  
    用于部署或升级应用程序的 PowerShell 脚本。

    * 应用程序定义  
在 ApplicationPackageRoot 下添加说明应用程序组合情况的 ApplicationManifest.xml 文件。 关联的应用程序参数文件位于 ApplicationParameters 下，这些文件可以用来指定特定于环境的参数。 Visual Studio 选择在关联的发布配置文件中指定的应用程序参数文件。
    
有关服务项目的内容概述，请参阅 [Reliable Services 入门](service-fabric-reliable-services-quick-start.md)。

## <a name="deploy-and-debug-the-application"></a>部署和调试应用程序

有了应用程序以后，即可通过以下步骤运行、部署和调试它。

1. 在 Visual Studio 中选择 F5，部署要调试的应用程序。

    >[!NOTE]
    >首次在本地运行和部署应用程序时，Visual Studio 会创建用于调试的本地群集。 这可能需要一些时间。 群集创建状态显示在 Visual Studio 输出窗口中。

    群集准备就绪时，将从 SDK 随附的本地群集系统托盘管理器应用程序收到通知。
    
    ![本地群集系统托盘通知][4]

    应用程序启动后，Visual Studio 会自动显示诊断事件查看器，可以在其中查看来自服务的跟踪输出。
    
    ![诊断事件查看器][5]

    >[!NOTE]
    >事件会自动在诊断事件查看器中开始跟踪。 如需手动配置诊断事件查看器，请先打开位于 **MyStatefulService** 项目中的 `ServiceEventSource.cs` 文件。 复制 `ServiceEventSource` 类顶部的 `EventSource` 属性的值。 在以下示例中，事件源称为 `"MyCompany-MyApplication-MyStatefulService"`，此项遇到你的情况可能有所不同。
>
    >![查找服务事件源名称][service-event-source-name]


2. 接下来，打开“ETW 提供程序”对话框。 然后选择位于“诊断事件”选项卡上的此轮图标。将复制的事件源的名称粘贴到“ETW 提供程序”输入框中。 然后选择“应用”按钮。 这会自动启动跟踪事件。

    ![设置诊断事件源名称][setting-event-source-name]

    此时会看到事件出现在“诊断事件”窗口。

    有状态服务模板显示在 **MyStatefulService.cs** 的 `RunAsync` 方法中递增的计数器值。

3. 展开事件之一可查看更多详细信息，包括运行代码的节点。 在此例中，它是 **\_Node\_0**，不过在你的计算机上可能会有所不同。
   
    ![诊断事件查看器详细信息][6]

4. 本地群集包含在单台计算机上托管的五个节点。 在生产环境中，每个节点都托管在不同的物理或虚拟机上。 在本地群集上取下一个节点，以模拟练习 Visual Studio 调试器时丢失一台计算机的情况。

5. 在“解决方案资源管理器”窗口中，打开“MyStatefulService.cs”。 

6. 找到 `RunAsync` 方法，然后在该方法的第一行中设置一个断点。

    ![有状态服务 RunAsync 方法中的断点][7]

7. 右键单击“本地群集管理器”系统托盘应用程序并选择“管理本地群集”，以便启动 Service Fabric Explorer 工具。

    ![从本地群集管理器启动 Service Fabric Explorer][systray-launch-sfx]

    [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 提供以视觉方式呈现群集的功能。 它包括部署到其中的应用程序集，以及充当组成成分的物理节点集。

8. 在左窗格中展开“群集” > “节点”，找到运行代码的节点。 然后，选择“操作” > “停用(重启)”来模拟计算机重启。

    ![在 Service Fabric 资源管理器中停止节点][sfx-stop-node]

    随着你在一个节点上进行的计算无缝地故障转移到另一个节点，应立即在 Visual Studio 中看到命中了断点。

9. 接下来，返回到诊断事件查看器并观察消息。 计数器在继续递增，即使事件实际上来自不同的节点。

    ![故障转移之后的诊断事件查看器][diagnostic-events-viewer-detail-post-failover]

## <a name="clean-up-the-local-cluster-optional"></a>清理本地群集（可选）

请记住，此本地群集是真实的。 停止调试器会删除应用程序实例，并注销应用程序类型。 不过，群集会继续在后台运行。 做好停止本地群集的准备以后，有多个选项可以选择。

### <a name="keep-application-and-trace-data"></a>保留应用程序和跟踪数据

右键单击“本地群集管理器”系统托盘应用程序，然后选择“停止本地群集”，以便关闭群集。

### <a name="delete-the-cluster-and-all-data"></a>删除群集和所有数据

右键单击“本地群集管理器”系统托盘应用程序，以便删除群集。 然后选择“删除本地群集”。 

如果选择此选项，Visual Studio 会在你下次运行应用程序时重新部署群集。 如果在一段时间内不想使用本地群集，或者需要回收资源，请选择此选项。

## <a name="next-steps"></a>后续步骤
阅读有关 [Reliable Services](service-fabric-reliable-services-introduction.md) 的更多内容。
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[service-event-source-name]: ./media/service-fabric-create-your-first-application-in-visual-studio/event-source-attribute-value.png
[setting-event-source-name]: ./media/service-fabric-create-your-first-application-in-visual-studio/setting-event-source-name.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[service-event-source-name]: ./media/service-fabric-create-your-first-application-in-visual-studio/event-source-attribute-value.png
[setting-event-source-name]: ./media/service-fabric-create-your-first-application-in-visual-studio/setting-event-source-name.png
