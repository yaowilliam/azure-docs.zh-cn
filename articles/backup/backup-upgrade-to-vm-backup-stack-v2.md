---
title: 升级到 Azure VM 备份堆栈 V2 | Microsoft Docs
description: VM 备份堆栈 V2 的升级过程和常见问题解答
services: backup, virtual-machines
documentationcenter: ''
author: trinadhk
manager: vijayts
tags: azure-resource-manager, virtual-machine-backup
ms.assetid: ''
ms.service: backup, virtual-machines
ms.devlang: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/08/2018
ms.author: trinadhk, sogup
ms.openlocfilehash: 7e092dc1448a45277e01b1a8c6d2bc0e2a8a22a3
ms.sourcegitcommit: 59914a06e1f337399e4db3c6f3bc15c573079832
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="upgrade-to-vm-backup-stack-v2"></a>升级到 VM 备份堆栈 V2
虚拟机 (VM) 备份堆栈 V2 升级提供以下功能增强：
* 可以查看在执行备份作业期间创建的用于恢复的快照，而无需等待数据传输完成。
这可以减少将快照复制到保管库，然后再触发还原所需的等待时间。 此外，借助这项增强，无需添置额外的存储来备份高级 VM（首次备份除外）。  

* 在本地保留快照 7 天，缩短了备份和还原时间。 

* 最大支持 4 TB 的磁盘。  

* 针对非托管 VM 执行还原时可以使用原始存储帐户（即使 VM 包含分布在不同存储帐户中的磁盘）。 这可以加快各种 VM 配置的还原速度。 
    > [!NOTE] 
    > 此方法与覆盖原始 VM 不同。 
    > 
    >

## <a name="what-is-changing-in-the-new-stack"></a>新堆栈有哪些变化？
目前备份作业包括两个阶段：
1.  创建 VM 快照。 
2.  将 VM 快照传输到 Azure 备份保管库。 

只在完成阶段 1 和 2 之后，才认为已创建恢复点。 在新堆栈中，一旦完成快照，就会立即创建一个恢复点。 也可以使用相同的还原工作流从此恢复点还原。 可以使用“快照”作为恢复点类型，在 Azure 门户中识别此恢复点。 将快照传输到保管库后，恢复点类型将更改为“快照和保管库”。 

![VM 备份堆栈 V2 中的备份作业](./media/backup-azure-vms/instant-rp-flow.jpg) 

快照默认保留 7 天。 这样可以减少将数据复制回到客户存储帐户所需的时间，从而可以更快地从这些快照完成还原。 

## <a name="considerations-before-upgrade"></a>升级前的注意事项
* 这是 VM 备份堆栈的单向升级。 因此，将来的所有备份都要经历此工作流。 由于**此功能是在订阅级别启用的，所有 VM 都要经历此工作流**。 所有新功能补充都基于同一个堆栈。 将来的版本将会支持在策略级别控制此功能。 
* 对于包含高级磁盘的 VM，在首次备份期间，请确保在首次备份完成之前，存储帐户中能够提供与 VM 大小相当的存储空间。 
* 由于快照存储在本地以便大幅提升恢复点创建速度和加速还原速度，因此，在七天期限内，可以看到对应于快照的存储成本。
* 增量快照作为页 blob 存储。 将对所有使用非托管磁盘的客户收取快照存储在客户本地存储帐户 7 天的费用。 根据当前定价模型，不对托管磁盘上的客户收费。
* 如果从快照恢复点执行高级 VM 还原，在还原过程中创建 VM 时，会看到使用了一个临时存储位置。 
* 对于高级存储帐户，即时恢复所用的快照将占用高级存储帐户中分配的 10TB 空间。

## <a name="how-to-upgrade"></a>如何升级？
### <a name="the-azure-portal"></a>Azure 门户
如果使用 Azure 门户，保管库仪表板上会显示一条有关支持大型磁盘以及备份和还原速度得到改善的通知。

![VM 备份堆栈 V2 中的备份作业](./media/backup-azure-vms/instant-rp-banner.png) 

若要打开相应的屏幕以升级到新堆栈，请选择横幅。 

![VM 备份堆栈 V2 中的备份作业](./media/backup-azure-vms/instant-rp.png) 

### <a name="powershell"></a>PowerShell
从权限提升的 PowerShell 终端执行以下 cmdlet：
1.  登录到 Azure 帐户。 

```
PS C:> Connect-AzureRmAccount
```

2.  选择要注册其预览版的订阅：

```
PS C:>  Get-AzureRmSubscription –SubscriptionName "Subscription Name" | Select-AzureRmSubscription
```

3.  注册此订阅的个人预览版：

```
PS C:>  Register-AzureRmProviderFeature -FeatureName "InstantBackupandRecovery" –ProviderNamespace Microsoft.RecoveryServices
```

## <a name="verify-whether-the-upgrade-is-complete"></a>检查升级是否已完成
在权限提升的 PowerShell 终端中运行以下 cmdlet：

```
Get-AzureRmProviderFeature -FeatureName "InstantBackupandRecovery" –ProviderNamespace Microsoft.RecoveryServices
```

如果输出中显示 Registered，则表示订阅已升级到 VM 备份堆栈 V2。 



