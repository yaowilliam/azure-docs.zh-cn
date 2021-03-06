---
title: Azure SKU 不可用错误 | Microsoft Docs
description: 介绍如何在部署过程中解决 SKU 不可用错误。
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/09/2018
ms.author: tomfitz
ms.openlocfilehash: 490c912a6abd6570c9bc74de8b86a516a8e6f807
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
---
# <a name="resolve-errors-for-sku-not-available"></a>解决 SKU 不可用的错误

本文介绍如何解决 SkuNotAvailable 错误。

## <a name="symptom"></a>症状

在部署资源（通常为虚拟机）时，收到以下错误代码和错误消息：

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

## <a name="cause"></a>原因

当所选的资源 SKU（如 VM 大小）不可用于所选的位置时，会收到此错误。

## <a name="solution-1---powershell"></a>解决方案 1 - PowerShell

要确定区域中可用的 SKU，请使用 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 命令。 按位置筛选结果。 必须拥有最新版本 PowerShell 才能运行此命令。

```powershell
Get-AzureRmComputeResourceSku | where {$_.Locations -icontains "southcentralus"}
```

结果包括位置的 SKU 列表以及针对该 SKU 的任何限制。

```powershell
ResourceType                Name      Locations Restriction                      Capability Value
------------                ----      --------- -----------                      ---------- -----
availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
virtualMachines      Standard_A0 southcentralus
virtualMachines      Standard_A1 southcentralus
virtualMachines      Standard_A2 southcentralus
```

## <a name="solution-2---azure-cli"></a>解决方案 2 - Azure CLI

要确定区域中可用的 SKU，请使用 `az vm list-skus` 命令。 然后，可以使用 `grep` 或类似的实用工具来筛选输出。

```bash
$ az vm list-skus --output table
ResourceType      Locations           Name                    Capabilities                       Tier      Size           Restrictions
----------------  ------------------  ----------------------  ---------------------------------  --------  -------------  ---------------------------
availabilitySets  eastus              Classic                 MaximumPlatformFaultDomainCount=3
avilabilitySets   eastus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Aligned                 MaximumPlatformFaultDomainCount=3
```

## <a name="solution-3---azure-portal"></a>解决方案 3 - Azure 门户

要确定区域中可用的 SKU，请使用[门户](https://portal.azure.com)。 登录到门户，并通过接口添加资源。 设置值时，可看到该资源的可用 SKU。 无需完成该部署。

![可用的 SKU](./media/resource-manager-sku-not-available-errors/view-sku.png)

## <a name="solution-4---rest"></a>解决方案 4 - REST

要确定区域中可用的 SKU，请对虚拟机使用 REST API。 发送以下请求：

```HTTP 
GET
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
```

它会以下列格式返回可用 SKU 和区域：

```json
{
  "value": [
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A0",
      "tier": "Standard",
      "size": "A0",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A1",
      "tier": "Standard",
      "size": "A1",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    ...
  ]
}
```

如果在该区域或满足业务需求的备用区域中找不到合适的 SKU，请将 [SKU 请求](https://aka.ms/skurestriction)提交到 Azure 支持。
