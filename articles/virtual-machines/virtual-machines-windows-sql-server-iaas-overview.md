---
title: Azure 虚拟机上的 SQL Server 概述 | Microsoft Docs
description: 了解如何在 Azure 虚拟机上运行完整的 SQL Server 版本。获取到所有 SQL Server VM 映像和相关内容的直接链接。
services: virtual-machines-windows
documentationcenter: ''
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management

ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: jroth

---
# Azure 虚拟机上的 SQL Server 概述
本主题介绍用于 Azure 虚拟机上运行 SQL Server 的几个选项，以及[到门户映像的链接](#option-1-deploy-a-sql-vm-per-minute-licensing)和[常见任务](#manage-your-sql-vm)概述。

> [!NOTE]
> 如果你已经熟悉 SQL Server，并且只是想了解如何部署 SQL Server VM，请参阅[在 Azure 门户中设置 SQL Server 虚拟机](virtual-machines-windows-portal-sql-server-provision.md)。
> 
> 

## 概述
你可能是想要将本地 SQL Server 工作负荷移至云的数据库管理员。或者，可能是针对 Azure 应用程序考虑 SQL Server 关系数据库功能的开发人员。在 Azure 虚拟机中运行 SQL Server 工作负荷有何优势？ 以下概述视频将讨论其优势并提供技术概述。

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

## 评估优势
开始之前，先评估在 Azure VM 上使用 SQL Server 的收获。

当你将其他工作负荷（例如企业应用程序）移至 Azure 时，最好也将任何依赖 SQL Server 数据库移至 Azure，以改善性能。不过，在 Azure VM 中托管 SQL Server 可提供其他优势。例如，你会自动获取多个数据中心的访问权限，从而获得全局支持和灾难恢复能力。有关完整的方案和优势列表，请参阅 [Azure VM 产品页上的 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/)。

> [!NOTE]
> 当对 Azure VM 上的 SQL Server 进行评估时，也要查看 Azure 上的其他存储和 SQL 选项，例如 [SQL 数据库](../sql-database/sql-database-technical-overview.md)、[SQL 数据仓库](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)和 [SQL Server Stretch Database](../sql-server-stretch-database/sql-server-stretch-database-overview.md)。有关详细的比较，请参阅[选择云 SQL Server 选项：Azure SQL (PaaS) 数据库或 Azure VM 上的 SQL Server (IaaS)](../sql-database/sql-database-paas-vs-sql-server-iaas.md)。
> 
> 

当你决定要在 Azure VM 上运行 SQL Server 之后，所做的第一个决策之一即是否使用包含 SQL Server 许可成本的 VM 映像。另一个选项是自带许可 (BYOL)，而只支付 VM 本身。下面两节会介绍这些选项。

## 创建新的 SQL VM
以下部分提供了有关 SQL Server 虚拟机库映像到 Azure 门户的直接链接。根据你所选的映像，可以基于分钟支付 SQL Server 许可费用，或者可以自带许可 (BYOL)。

在本教程中查找该过程的逐步指导，[在 Azure PowerShell 中预配 SQL Server 虚拟机](virtual-machines-windows-portal-sql-server-provision.md)。另外，请查看 [SQL Server VM 的性能最佳实践](virtual-machines-windows-sql-performance.md)，其中介绍了如何选择适当的虚拟机大小和预配期间其他可用的功能。

## 选项 1：创建具有每分钟许可的 SQL 虚拟机
下表提供了虚拟机库中提供的 SQL Server 映像的矩阵。单击任何链接，即可开始创建具有指定版本和操作系统的新 SQL VM。

| 版本 | 操作系统 | 版本 |
| --- | --- | --- |
| **SQL 2016** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMStandardWindowsServer2012R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMWebWindowsServer2012R2)、[Dev](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMDeveloperWindowsServer2012R2)、[Express](https://portal.azure.com/#create/Microsoft.SQLServer2016RTMExpressWindowsServer2012R2) |
| **SQL 2014 SP1** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1StandardWindowsServer2012R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1WebWindowsServer2012R2)、[Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP1ExpressWindowsServer2012R2) |
| **SQL 2014** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014StandardWindowsServer2012R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2014WebWindowsServer2012R2) |
| **SQL 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2)、[Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |
| **SQL 2012 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2StandardWindowsServer2012R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2WebWindowsServer2012R2) |
| **SQL 2012 SP2** |Windows Server 2012 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2EnterpriseWindowsServer2012)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2StandardWindowsServer2012)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2WebWindowsServer2012)、[Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP2ExpressWindowsServer2012) |
| **SQL 2008 R2 SP3** |Windows Server 2008 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3EnterpriseWindowsServer2008R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3StandardWindowsServer2008R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3WebWindowsServer2008R2) |
| **SQL 2008 R2 SP3** |Windows Server 2012 |[Express](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3ExpressWindowsServer2012) |

## 选项 2：使用现有许可创建 SQL VM
你也可以自带许可 (BYOL)。在此方案中，你只需支付 VM 费用，SQL Server 许可不需要任何额外的费用。若要使用自己的许可证，请参考下面的 SQL Server 版本和操作系统对照表。在门户中，这些映像名称带有 **{BYOL}** 前缀。

| 版本 | 操作系统 | 版本 |
| --- | --- | --- |
| **SQL Server 2016** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016RTMStandardWindowsServer2012R2)、[Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016RTMStandardWindowsServer2012R2) |
| **SQL Server 2014 SP1** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP1EnterpriseWindowsServer2012R2)、[Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP1StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2)、[Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

> [!IMPORTANT]
> 若要使用 BYOL VM 映像，必须具有包含 [Azure 上通过软件保障实现的许可移动性](https://azure.microsoft.com/pricing/license-mobility/)的企业协议。此外，还需要有所要使用的 SQL Server 版本的有效许可证。必须在预配 VM 的 **10** 天内[向 Microsoft 提供必要的 BYOL 信息](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf)。
> 
> 

## 管理 SQL VM
预配 SQL Server VM 之后，有几项可选的管理任务。在许多方面，完全可以像管理本地 SOL Server 实例一样配置和管理 SQL Server。但某些任务是 Azure 特有的。下列各节重点介绍上述某些领域并提供详细信息链接。

### 迁移数据
如果已有数据库，你会想要将该数据库移至新预配的 SQL VM。有关迁移选项的列表和指导，请参阅[将数据库迁移到 Azure VM 上的 SQL Server](virtual-machines-windows-migrate-sql.md)。

### 配置高可用性
如果你需要高可用性，请考虑配置 SQL Server 可用性组。这涉及虚拟网络中的多个 Azure VM。Azure 门户提供了一个模板用于设置此配置。有关详细信息，请参阅[在 Azure Resource Manager 虚拟机中配置 AlwaysOn 可用性组](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)。如果你想要手动配置可用性组和关联的侦听器，请参阅[在 Azure VM 中配置 AlwaysOn 可用性组](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。

有关其他高可用性注意事项，请参阅 [Azure 虚拟机中 SQL Server 的高可用性和灾难恢复](virtual-machines-windows-sql-high-availability-dr.md)。

### 备份数据
Azure VM 可以利用[自动备份](virtual-machines-windows-sql-automated-backup.md)，定期创建数据库到 Blob 存储的备份。你也可以手动使用此技术。有关详细信息，请参阅[使用 Azure 存储空间进行 SQL Server 备份和还原](virtual-machines-windows-use-storage-sql-server-backup-restore.md)。有关所有备份和还原选项的概述，请参阅 [Azure 虚拟机中 SQL Server 的备份和还原](virtual-machines-windows-sql-backup-recovery.md)。

### 自动更新
Azure VM 可以使用[自动修补](virtual-machines-windows-sql-automated-patching.md)来安排维护时段，以便自动安装重要的 Windows 和 SQL Server 更新。

### 客户体验改善计划 (CEIP)
客户体验改善计划 (CEIP) 默认情况下已启用。这不是一项管理任务，除非你想在预配之后禁用 CEIP。你可以通过远程桌面连接到 VM，以自定义或禁用 CEIP。然后运行 **SQL Server 错误和使用情况报告**实用工具。请按照说明禁用报告功能。

## 后续步骤
[探索学习路径](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/)：Azure 虚拟机上的 SQL Server。

其他问题？ 请先参阅 [Azure 虚拟机中的 SQL Server 常见问题解答](virtual-machines-windows-sql-server-iaas-faq.md)。同时将你的问题或看法添加在任何 SQL VM 主题的底部，以便与 Microsoft 和社区互动。

<!---HONumber=AcomDC_0921_2016-->