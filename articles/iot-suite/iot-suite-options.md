---
title: Microsoft Azure IoT 选项 | Microsoft Docs
description: 选择如何使用 Azure IoT 解决方案加速器、Azure IoT Central 或 Azure IoT 中心实现 IoT 解决方案。
services: iot-suite
suite: iot-suite
author: dominicbetts
manager: timlt
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.topic: get-started-article
ms.date: 11/10/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d38a41a33632e2c6427b75e365db468940d025d
ms.sourcegitcommit: 688a394c4901590bbcf5351f9afdf9e8f0c89505
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/18/2018
ms.locfileid: "34300962"
---
# <a name="compare-azure-iot-options"></a>比较 Azure IoT 选项

[Azure 和物联网](../iot-accelerators/iot-accelerators-what-is-azure-iot.md)一文介绍了典型的具有以下层的 IoT 解决方案体系结构：

* 设备连接和管理
* 数据处理和分析
* 呈现和业务集成

若要实现此体系结构，可使用 Azure IoT 提供的几个选项，每个选项适用于不同组合的客户需求：

* [Azure IoT 解决方案加速器](index.md)是基于 Azure 平台即服务 (PaaS) 的企业级[解决方案加速器](../iot-accelerators/iot-accelerators-what-are-solution-accelerators.md)集合，用于加速自定义 IoT 解决方案的开发。

* [Azure IoT Central](https://www.microsoft.com/internet-of-things/iot-central-saas-solutions) 是一种软件即服务 (SaaS) 解决方案，此解决方案使用基于模型的方法，用于生成企业级 IoT 解决方案而不需云解决方案开发专业知识。

## <a name="azure-iot-hub"></a>Azure IoT 中心

Azure IoT 中心是核心的 Azure PaaS，可供 Azure IoT Central 和 Azure IoT 解决方案加速器使用。 可以通过 IoT 中心在数百万个 IoT 设备和一个云解决方案之间实现安全可靠的双向通信。 可以借助 IoT 中心克服 IoT 实现难题，例如：

* 大容量设备连接和管理。
* 大容量遥测引入。
* 设备的命令和控制。
* 设备安全措施实施。

## <a name="compare-azure-iot-solution-accelerators-and-azure-iot-central"></a>比较 Azure IoT 解决方案加速器和 Azure IoT Central

选择 Azure IoT 产品是规划 IoT 解决方案的重要一环。 IoT 中心是单项 Azure 服务，其本身不提供端到端 IoT 解决方案。 任何 IoT 解决方案都可以从 IoT 中心入手，不需使用 Azure IoT 解决方案加速器或 Azure IoT Central 即可使用它。 Azure IoT 解决方案加速器和 Azure IoT Central 都使用 IoT 中心以及其他 Azure 服务。 下表汇总了 Azure IoT 解决方案加速器和 Azure IoT Central 之间的主要差异，有助于根据要求进行正确的选择：

|                        | Azure IoT 解决方案加速器 | Azure IoT Central |
| ---------------------- | --------- | ----------- |
| 主要用途 | 加速开发需要最大灵活性的自定义 IoT 解决方案。 | 缩短不需深层服务自定义的直观 IoT 解决方案的面市时间。 |
| 访问基础 PaaS 服务          | 有权访问基础 Azure 服务，根据需要对其进行管理或替换。 | SaaS。 完全托管的解决方案，基础服务不公开。 |
| 灵活性            | 高。 微服务的代码是开源的，可以任意修改。 此外还可以自定义部署基础结构。| 中。 可以根据内置的基于浏览器的用户体验来自定义解决方案模型和 UI 的各个方面。 基础结构不可自定义，因为未公开各种不同的组件。|
| 技能级别                 | 中-高。 需要 Java 或 .NET 技能才能自定义解决方案后端。 需要 JavaScript 技能才能自定义可视化效果。 | 低。 需要建模技能才能自定义解决方案。 不需编码技能。 |
| 入门体验 | 解决方案加速器可实现常见的 IoT 方案。 可以在数分钟内部署。 | 应用程序模板和设备模板提供预建的模型。 可以在数分钟内部署。 |
| 定价                | 可以通过微调服务来控制成本。 | 简单且可预测的定价结构。 |

使用哪种产品来生成 IoT 解决方案最终取决于：

* 业务需求。
* 要生成的解决方案的类型。
* 组织生成解决方案并进行长期维护所需的技能组合。

## <a name="next-steps"></a>后续步骤

根据所选产品和方法，建议的后续步骤如下：

* **Azure IoT 解决方案加速器**[Azure IoT 解决方案加速器是什么？](../iot-accelerators/iot-accelerators-what-are-solution-accelerators.md)
* **Azure IoT Central**：[Azure IoT Central](https://www.microsoft.com/internet-of-things/iot-central-saas-solutions)。
* **IoT 中心**：[Azure IoT 中心服务概述](../iot-hub/iot-hub-what-is-iot-hub.md)。
