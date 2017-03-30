---
title: "Azure 虚拟机 PowerShell 示例 | Microsoft 文档"
description: "Azure 虚拟机 PowerShell 示例"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
translationtype: Human Translation
ms.sourcegitcommit: 97acd09d223e59fbf4109bc8a20a25a2ed8ea366
ms.openlocfilehash: 4973a78b069e27e0ca30a9b82389992fb9c10ff2
ms.lasthandoff: 03/10/2017


---
# <a name="azure-virtual-machine-powershell-samples"></a>Azure 虚拟机 PowerShell 示例

下表包含用于创建和管理 Linux 虚拟机的 PowerShell 脚本示例的链接。

| | |
|---|---|
|**创建虚拟机**||
| [创建完全配置的虚拟机](./scripts/virtual-machines-linux-powershell-sample-create-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) | 创建资源组、虚拟机以及所有相关资源。|
| [创建已启用 Docker 的 VM](./scripts/virtual-machines-linux-powershell-sample-create-docker-host.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) | 创建一个虚拟机，将此 VM 配置为 Docker 主机，并运行 NGINX 容器。 |
| [创建 VM 并运行配置脚本](./scripts/virtual-machines-linux-powershell-sample-create-vm-nginx.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) | 创建一个虚拟机，并使用 Azure 自定义脚本扩展安装 NGINX。 |
| [创建安装有 WordPress 的 VM](./scripts/virtual-machines-linux-powershell-sample-create-vm-wordpress.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) | 创建一个虚拟机，并使用 Azure 自定义脚本扩展安装 WordPress。 |
|**监视虚拟机**||
| [使用 Operations Management Suite 监视 VM](./scripts/virtual-machines-linux-powershell-sample-create-vm-oms.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) | 创建一个虚拟机，安装 Operations Management Suite 代理，并在 OMS 工作区中注册该 VM。  |
| | |