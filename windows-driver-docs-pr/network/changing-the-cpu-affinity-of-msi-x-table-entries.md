---
title: 更改 MSI-X 表项的 CPU 关联
description: 更改 MSI-X 表项的 CPU 关联
ms.assetid: 46ce91ad-76eb-4d05-af9d-a295c665640a
keywords:
- 网络、 MSI X 表条目 CPU 关联的 MSI X WDK
- 消息信号中断 WDK 网络，MSI X 表条目 CPU 关联
- Msi WDK 网络，MSI X 表条目 CPU 关联
- 中断 WDK 网络、 MSI X 表条目 CPU 关联
- CPU af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fbf3b077c67658fecba9e8d8b36eed8b952aa16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382776"
---
# <a name="changing-the-cpu-affinity-of-msi-x-table-entries"></a>更改 MSI-X 表项的 CPU 关联





NDIS 6.1 和更高版本支持 MSI X 的微型端口驱动程序可以调用[ **NdisMConfigMSIXTableEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismconfigmsixtableentry)函数屏蔽，取消屏蔽，或将 MSI X 表条目映射到设备分配的 MSI X 消息。 支持 RSS 使用的微型端口驱动程序**NdisMConfigMSIXTableEntry**若要在运行时更改 MSI X 表条目的 CPU 关联。

**NdisMConfigMSIXTableEntry**周围的包装[GUID\_MSIX\_表\_CONFIG\_接口](https://msdn.microsoft.com/library/windows/hardware/ff546563)查询。 微型端口驱动程序可以调用**NdisMConfigMSIXTableEntry** NDIS 调用之后[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数之前将驱动程序返回从[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数。

分配每个 RSS 队列的 MSI X 表条目，并具有较少的队列不是 RSS 处理器的数目可以添加 MSI X 消息中的其他资源的微型端口驱动程序[ *MiniportFilterResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)函数。 有关如何修改设备的已分配的资源的详细信息，请参阅[MSI X 资源筛选](msi-x-resource-filtering.md)。

微型端口驱动程序可以设置 MSI X 中断资源的 CPU 关联，以便该设备已为每个 RSS 处理器的至少一个 MSI X 消息。 请注意，PCI 总线驱动程序最初将映射*n* MSI X 表条目 (其中*n*是 NIC 硬件报告到总线 MSI-X 表条目数) 与第一个*n*中已修改的资源的 MSI X 消息。 在 NDIS 后调用*MiniportInitializeEx*，当微型端口驱动程序更改特定 MSI X 表条目，驱动程序调用的目标处理器**NdisMConfigMSIXTableEntry**映射该表条目MSI X 消息已设置为所需的处理器关联。

 

 





