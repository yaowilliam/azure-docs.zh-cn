---
title: 使用 Azure 媒体服务分析视频 | Microsoft Docs
description: 按照本教程的步骤，使用 Azure 媒体服务分析视频。
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: tutorial
ms.custom: mvc
ms.date: 04/09/2018
ms.author: juliako
ms.openlocfilehash: 54c49645722b6545d8ae872151b9b82674d44523
ms.sourcegitcommit: e14229bb94d61172046335972cfb1a708c8a97a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
---
# <a name="tutorial-analyze-videos-with-azure-media-services"></a>教程：使用 Azure 媒体服务分析视频 

本教程介绍如何使用 Azure 媒体服务分析视频。 在很多情况下，用户可能会希望深入了解录制的视频或音频内容。 例如，若要提高客户满意度，组织可采取语音转文本操作，将客户支持录音转换为具有索引和仪表板的可搜索目录。 然后，即可获得有关其业务的见解，如常见投诉列表、此类投诉的来源等等。

本教程演示如何：    

> [!div class="checklist"]
> * 启动 Azure Cloud Shell
> * 创建媒体服务帐户
> * 访问媒体服务 API
> * 配置示例应用
> * 仔细检查示例代码
> * 运行应用程序
> * 检查输出
> * 清理资源

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>先决条件

如果没有安装 Visual Studio，可下载 [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)。

## <a name="download-the-sample"></a>下载示例

使用以下命令将包含 .NET 示例的 GitHub 存储库克隆到计算机：  

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git
 ```

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="examine-the-sample-code-in-detail"></a>仔细检查示例代码

本节讨论 AnalyzeVideos 项目的 [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/AnalyzeVideos/Program.cs) 文件中定义的函数。

### <a name="start-using-media-services-apis-with-net-sdk"></a>开始结合使用媒体服务 API 与 .NET SDK

若要开始将媒体服务 API 与 .NET 结合使用，需要创建 AzureMediaServicesClient 对象。 若要创建对象，需要提供客户端所需凭据以使用 Azure AD 连接到 Azure。 首先需要获取令牌，然后从返回的令牌创建 ClientCredential 对象。 在本文开头克隆的代码中，ArmClientCredential 对象用于获取令牌。  

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateMediaServicesClient)]

### <a name="create-an-output-asset-to-store-the-result-of-a-job"></a>创建输出资产用于存储作业结果 

输出资产会存储作业结果。 项目定义 DownloadResults 函数，该函数将结果从此输出资产中下载到“输出”文件夹中，便于用户查看获取的内容。

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateOutputAsset)]

### <a name="create-a-transform-and-a-job-that-analyzes-videos"></a>创建转换和分析视频的作业

对媒体服务中的内容进行编码或处理时，一种常见的模式是将编码设置设为脚本。 然后，需提交**作业**，将该脚本应用于视频。 为每个新视频提交新作业后，即可将该脚本应用于库中的所有视频。 媒体服务中的脚本称为**转换**。 有关详细信息，请参阅[转换和作业](transform-concept.md)。 本教程中所述的示例定义了分析指定视频的脚本。 

#### <a name="transform"></a>转换

创建新转换实例时，需要指定希望生成的输出内容。 所需参数是 TransformOutput 对象，如上述代码所示。 每个 TransformOutput 包含一个预设。 预设介绍视频和/或音频处理操作的各个步骤，这些操作可生成所需 TransformOutput。 在此示例中，使用了 VideoAnalyzerPreset 预设，且将语言 (“en-US”) 传递给了其构造函数。 凭借此预设，可以从视频提取多个音频和视频见解。 如需从视频提取多个音频见解，可以使用**AudioAnalyzerPreset** 预设。 

在创建时**转换**，首先应检查是否其中一个已存在使用**获取**方法，如下面的代码中所示。  在 Media Services v3**获取**实体上的方法返回**null**如果实体不存在 （不区分大小写的名称检查）。

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#EnsureTransformExists)]

#### <a name="job"></a>作业

如上所述，转换对象为脚本，作业则是对媒体服务的实际请求，请求将转换应用到给定输入视频或音频内容。 作业指定输入视频位置和输出位置等信息。 可使用以下方法指定视频位置：HTTPS URL、SAS URL 或媒体服务帐户中的资产。 

在此示例中，作业输入是一个本地视频。  

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#SubmitJob)]

### <a name="wait-for-the-job-to-complete"></a>等待作业完成

此作业需要一些时间才能完成，完成时可发出通知。 可通过不同选项在作业完成后获取通知。 最简单的选项（如下所示）是使用轮询。 

对于生产应用程序，由于可能出现延迟，并不建议将轮询作为最佳做法。 如果在帐户上过度使用轮询，轮询会受到限制。 开发者应改用事件网格。

事件网格旨在实现高可用性、一致性能和动态缩放。 使用事件网格，应用可以侦听和响应来自几乎所有 Azure 服务和自定义源的事件。 处理基于 HTTP 的反应事件非常简单，这有助于通过对事件的智能筛选和路由生成高效的解决方案。 请参阅[将事件路由到自定义 Web 终结点](job-state-events-cli-how-to.md)。

作业通常将经历以下状态：“已计划”、“已排队”、“正在处理”、“已完成”（最终状态）。 如果作业出错，则显示“错误”状态。 如果作业正处于取消过程中，则显示“正在取消”，完成时则显示“已取消”。

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#WaitForJobToFinish)]

### <a name="download-the-result-of-the-job"></a>下载作业结果

以下函数将输出资产的结果下载到“输出”文件夹中，以便检查作业结果。 

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#DownloadResults)]

### <a name="clean-up-resource-in-your-media-services-account"></a>清理媒体服务帐户中的资源

通常情况下，除了打算重复使用的对象，用户应清理所有内容（通常将重复使用转换并保留 StreamingLocators 等）。 如果希望帐户在试验后保持干净状态，则应删除不打算重复使用的资源。 例如，以下代码可删除作业。

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CleanUp)]

## <a name="run-the-sample-app"></a>运行示例应用

按 Ctrl+F5 运行 AnalyzeVideos 应用程序。

运行该程序时，作业会生成其在视频中发现的每张人脸的缩略图。 它还会生成 insights.json 文件。

## <a name="examine-the-output"></a>检查输出

分析视频得到的输出文件称为 insights.json。 此文件包含有关视频的见解。 可以从[媒体智能](intelligence-concept.md)一文中获取对 json 文件中找到的元素的说明。

## <a name="clean-up-resources"></a>清理资源

如果不再需要资源组中的任何一个资源（包括为本教程创建的媒体服务和存储帐户），请删除之前创建的资源组。 可以使用 CloudShell 工具。

在 CloudShell 中，执行以下命令：

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="multithreading"></a>多线程处理

Azure 媒体服务 v3 SDK 不是线程安全的。 使用多线程应用程序时，应在每个线程上生成一个新的 AzureMediaServicesClient 对象。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [教程：上传、编码和流式处理文件](stream-files-tutorial-with-api.md)
