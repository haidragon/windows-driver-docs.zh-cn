---
title: 查询虚拟功能的 PCI 基址寄存器
description: 查询虚拟功能的 PCI 基址寄存器
ms.assetid: 99C2BF61-E87E-4C3B-BE7E-C16B5318EC1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774154db042ba94c4b4d2b42ea47b3786673811a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377045"
---
# <a name="querying-the-pci-base-address-registers-of-a-virtual-function"></a>查询虚拟功能的 PCI 基址寄存器

**请注意**此方法只能由过量的 HYPER-V 父分区在管理操作系统中运行的驱动程序。

PCI 总线驱动程序，它运行在管理操作系统的 HYPER-V 父分区中，查询的内存或 I/O 地址空间的要求的每个 PCI 基本注册 （的地址栏） 的网络适配器。 PCI 总线驱动程序第一次检测到总线上的适配器时执行此查询。

PCI 栏此查询中，通过 PCI 总线驱动程序确定：

-   无论网络适配器是否支持 PCI 栏。

-   如果支持一个栏，则是栏需要多少内存或 I/O 地址空间。

PCI 驱动程序按下述方式执行此 PCI 栏查询：

1.  PCI 驱动程序第一次写入都是 1 到栏。

2.  PCI 驱动程序然后读取确定所需的内存或地址空间所需的条形的条形图。 零值指示网络适配器不支持在栏。

在 HYPER-V 子分区的来宾操作系统中运行虚拟 PCI (VPCI) 总线驱动程序。 PCI Express (PCIe) 虚拟函数 (VF) 附加到子分区，VPCI 总线驱动程序公开的虚拟网络适配器，以便 VF (*VF 网络适配器*)。 它执行此操作之前，VPCI 总线驱动程序必须执行 PCI 栏查询以确定所需的内存或 VF 网络适配器所需的地址空间。

由于对 PCI 配置空间的访问是一项特权的操作，只能由管理操作系统的 HYPER-V 父分区中运行的组件执行。 NDIS 当 VPCI 总线驱动程序查询 PCI 条时，发出的对象标识符 (OID) 查询请求[OID\_SRIOV\_PROBED\_条](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-probed-bars)到 PF 微型端口驱动程序。 此 OID 查询请求返回的结果将转发到 VPCI 总线驱动程序，以便它可以确定需要多少内存地址空间 VF 网络适配器。

**请注意**  OID 请求的 OID\_SRIOV\_栏\_只可由 NDIS 发出资源。 不必须由基础驱动程序，例如协议或筛选器驱动程序颁发的 OID 请求。

 

OID\_SRIOV\_PROBED\_条查询请求包含[ **NDIS\_SRIOV\_PROBED\_条\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)结构。 当 PF 微型端口驱动程序处理此 OID 时，则驱动程序必须返回引用的数组中的 PCI 栏值**BaseRegisterValuesOffset**的成员**NDIS\_SRIOV\_PROBED\_条\_信息**结构。 每个数组内的偏移量，PF 微型端口驱动程序必须设置为在相同物理网络适配器的 PCI 配置空间内的偏移量的栏的 ULONG 值的数组元素。

每个条由驱动程序返回的值必须是将遵循 PCI 条查询，因为由管理操作系统中运行的 PCI 驱动程序执行的相同值。 PF 微型端口驱动程序可以调用[ **NdisMQueryProbedBars** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueryprobedbars)来确定此信息。

有关基址寄存器 PCI 设备的详细信息，请参阅*PCI 本地总线规范*。

 

 





