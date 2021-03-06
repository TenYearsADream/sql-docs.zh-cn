---
title: 配置 Azure Kubernetes 服务
titleSuffix: SQL Server big data clusters
description: 了解如何配置用于 SQL Server 2019 大数据群集 （预览版） 部署的 Azure Kubernetes 服务 (AKS)。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ddf14cf97fc72acb4a7c44bbc123f171e31c20a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911129"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>为 SQL Server 的大数据群集部署中配置 Azure Kubernetes 服务

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何配置用于 SQL Server 2019 大数据群集 （预览版） 部署的 Azure Kubernetes 服务 (AKS)。

AKS 轻松创建、 配置和管理 Kubernetes 群集以运行容器化应用程序使用的预配置的虚拟机群集。 这使您可以使用现有技能或大量不断增长的社区专业知识，在部署和管理基于容器的 Microsoft Azure 上的应用程序。

本文介绍部署 Kubernetes AKS 使用 Azure CLI 上的步骤。 如果还没有 Azure 订阅，请在开始之前创建一个免费帐户。

> [!TIP] 
> 部署 AKS 和 SQL Server 大数据群集的示例 python 脚本，请参阅[快速入门：部署大数据群集在 Azure Kubernetes 服务 (AKS) 的 SQL Server](quickstart-big-data-cluster-deploy.md)。

## <a name="prerequisites"></a>先决条件

- [部署 SQL Server 2019 大数据工具](deploy-big-data-tools.md):
   - **Kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **Azure CLI**

- Kubernetes 服务器的最小值 1.10 版本。 适用于 AKS，您需要使用`--kubernetes-version`参数来指定默认值以外的版本。

- 验证在 AKS 上的基本方案时获得最佳体验，请使用：
   - 在所有节点之间的 8 个 Vcpu
   - 32 GB 的每个虚拟机的内存
   - 24 或更多附加磁盘的所有节点

   > [!TIP]
   > Azure 基础结构提供了多个 Vm 的大小选项，请参阅[此处](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)为计划部署的目标区域中的选择。

## <a name="create-a-resource-group"></a>创建资源组

Azure 资源组是在哪个 Azure 中部署和管理资源的逻辑组。 以下步骤登录到 Azure 并创建 AKS 群集的资源组。

1. 在命令提示符处，运行以下命令并按照提示登录到 Azure 订阅：

    ```azurecli
    az login
    ```

1. 如果有多个订阅可以通过运行以下命令来查看所有订阅：

   ```azurecli
   az account list
   ```

1. 如果你想要将更改为不同的订阅可以运行以下命令：

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. 创建一个包含资源组**az 组创建**命令。 下面的示例创建名为的资源组`sqlbigdatagroup`在`westus2`位置。

   ```azurecli
   az group create --name sqlbigdatagroup --location westus2
   ```

## <a name="create-a-kubernetes-cluster"></a>创建 Kubernetes 群集

1. 在与 AKS 创建 Kubernetes 群集[az aks 创建](https://docs.microsoft.com/cli/azure/aks)命令。 下面的示例创建名为的 Kubernetes 群集*kubcluster*具有一个 Linux 代理节点的大小**Standard_L8s**。 请确保你在前面几节中使用同一资源组中创建 AKS 群集。

    ```azurecli
   az aks create --name kubcluster \
    --resource-group sqlbigdatagroup \
    --generate-ssh-keys \
    --node-vm-size Standard_L8s \
    --node-count 1 \
    --kubernetes-version 1.12.6
    ```

   可以增加或减少 Kubernetes 代理节点数，方法是更改`--node-count <n>`其中`<n>`是你想要使用的代理节点数。 这不包括在后台由 AKS 主 Kubernetes 节点。 前面的示例仅供评估使用的单个节点。

   几分钟后，该命令完成并返回有关群集的 JSON 格式信息。

1. 保存 JSON 输出以供将来使用前一命令。

## <a name="connect-to-the-cluster"></a>连接到群集

1. 若要配置 kubectl 以连接到 Kubernetes 群集，运行[az aks get-credentials 来获取凭据](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials)命令。 此步骤下载凭据，并配置 kubectl CLI 来使用它们。

   ```azurecli
   az aks get-credentials --resource-group=sqlbigdatagroup --name kubcluster
   ```

1. 若要验证连接到群集，请使用[kubectl 获取](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)命令返回群集节点的列表。  下面的示例中显示的输出如你打算有个主节点和 3 个代理节点。

   ```
   kubectl get nodes
   ```

## <a name="next-steps"></a>后续步骤

在本文中的步骤配置在 AKS 中的 Kubernetes 群集。 下一步是将 SQL Server 2019 大数据部署到群集。 有关如何部署大数据群集的详细信息，请参阅以下文章：

[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)
