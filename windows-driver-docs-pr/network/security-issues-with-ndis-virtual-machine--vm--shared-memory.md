---
title: NDIS 虚拟机 (VM) 共享内存的安全问题
description: NDIS 虚拟机 (VM) 共享内存的安全问题
ms.assetid: 42b903b0-6729-4314-9305-9345fff9b2ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c574d7cd2f299ae12234ff62ba5da27dcf406d4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382126"
---
# <a name="security-issues-with-ndis-virtual-machine-vm-shared-memory"></a>NDIS 虚拟机 (VM) 共享内存的安全问题





本主题讨论涉及从虚拟机 (VM) 中分配共享的内存，为虚拟机队列 (VMQ) 接收缓冲区的潜在安全问题。 本主题包括以下各节：

-   [概述与 VM 的安全问题的共享内存](#overview)

-   [Windows Server 2008 R2 如何解决安全问题](#ndis620)

-   [Windows Server 2012 和更高版本中如何解决安全问题](#ndis630)

**请注意**  HYPER-V 中，子分区也称为是 VM。

 

### <a href="" id="overview"></a>概述与 VM 的安全问题的共享内存

Vm 不受信任的软件实体。 它是恶意 VM 必须不能干扰其他 Vm 或管理操作系统的 HYPER-V 父分区中运行。 本部分提供背景信息和要求，以确保驱动程序编写人员了解 VMQ 安全问题和共享内存的要求。 有关共享内存的详细信息，请参阅[共享的内存资源分配](shared-memory-resource-allocation.md)中的主题[编写 VMQ 驱动程序](writing-vmq-drivers.md)部分。

在虚拟化环境中，可以查看或修改 VM 的 VM 共享内存。 但是，不允许查看或修改与其他 Vm 相关联的数据。 虚拟机也不允许访问管理操作系统地址空间。

必须保护接收数据包的标头部分。 VM 不能影响网络虚拟服务提供商 (VSP) 中的 HYPER-V 可扩展交换机的行为。 因此，VLAN (虚拟 LAN) 筛选必须发生之前的网络适配器使用 DMA 传输到 VM 的数据共享内存。 此外，不能受影响的交换机的媒体访问控制 (MAC) 地址学习。

如果 HYPER-V 可扩展交换机连接到 VM 的端口具有关联的 VLAN 标识符，在主计算机必须确保目标 MAC 地址和传入的帧的 VLAN 标识符匹配这些各自的属性的主机之前的端口将数据包转发到 VM 的虚拟网络适配器。 如果在框架的 VLAN 标识符与该端口的 VLAN 标识符不匹配，则丢弃数据包。 当从主机内存分配的虚拟网络适配器的接收缓冲区时，主机可以检查 VLAN 标识符放在帧如有必要使框架的内容到目标 VM 变得可见之前。 如果帧不会复制到虚拟机的地址空间，该 VM 不能访问它。

但是，当 VMQ 配置为使用共享的内存，网络适配器使用 DMA 将传入的帧传送到 VM 的地址空间直接。 此传输引入了安全问题在其中一个虚拟机可以而无需等待应用所需的 VLAN 筛选的可扩展交换机检查接收到的帧的内容。

### <a href="" id="ndis620"></a>Windows Server 2008 R2 如何解决安全问题

在 Windows Server 2008 R2 中，VSP 配置要从 VM 的地址空间，使用共享的内存分配的 VM 队列之前它使用以下筛选测试队列。

```syntax
(MAC address == x) && (VLAN identifier == n)
```

如果网络适配器硬件能够支持此测试，再到接收缓冲区的 DMA 传输，可以丢弃帧具有无效的 VLAN 标识符或将其发送到默认的队列，以便它们可以通过筛选出可扩展交换机的网络适配器。 如果微型端口驱动程序中使用此测试在队列上设置筛选器的请求成功，可扩展交换机可以使用该队列的共享的虚拟机内存。 但是，如果网络适配器硬件不能筛选根据目标 MAC 地址和 VLAN 标识符的帧，可扩展交换机会使用该队列的主机共享内存。

可扩展交换机检查的源接收到的帧，若要配置传输帧的路由信息的 MAC 地址 — 也就是说，它是类似于物理学习开关。 可以在主机堆栈; 安装防火墙筛选器驱动程序例如，上面的微型端口驱动程序的网络适配器硬件和下方可扩展切换驱动程序。 防火墙筛选器驱动程序可以访问在可扩展交换机之前接收到的帧中的数据。 如果从 VM 地址空间分配每个帧的整个接收缓冲区的恶意 VM 无法访问部分会由筛选器驱动程序或可扩展交换机在主机中运行的检查的帧。

若要解决此安全问题，请使用 VM 共享内存的虚拟机队列时，网络适配器必须拆分至少是预测先行大小，这是预先确定固定值的字节偏移量处的数据包。 任何预测先行数据 — 即数据预测先行大小的字节偏移量是 — 必须通过 DMA 传送至共享有关预测先行数据分配的内存。 开机自检预测先行数据 — 帧有效负载的其余部分 — 通过 DMA 应传送至 post 预测先行数据分配的共享内存。

下图显示了网络的关系数据结构时传入数据拆分为预测先行和 post 预测先行共享内存缓冲区。

![说明使用预测先行和 post 预测先行数据 vmq 数据包结构的关系图](images/vmqpacket.png)

VMQ 共享内存的摘要要求如下所示：

-   网络适配器可以拆分大于预期大小的标头的网络边界处接收的帧。 但是，当请求通过 NDIS 和无一例外，所有接收和分配给 VMQ 的帧必须拆分位置或后面 NDIS 请求的预期大小边界。

-   预测先行数据必须通过 DMA 传送至分配的微型端口驱动程序的共享内存。 微型端口驱动程序必须指定将用于预测先行数据使用内存的分配调用中。

-   开机自检预测先行数据必须通过 DMA 传送至分配的微型端口驱动程序的共享内存。 微型端口驱动程序必须将 post 预测先行数据使用内存的分配调用中指定。

-   微型端口驱动程序不能依赖于 NDIS 将用于完成共享的内存分配请求的地址空间。 也就是说，预测先行或 post 预测先行数据的共享的内存地址空间是特定于实现的。 在许多情况下，NDIS 或可扩展交换机可能满足所有请求，其中包含用于 post 预测先行使用，从主机内存地址空间。

-   在其中接收帧 VMQ 的顺序接收时该队列中的框架来指示驱动程序堆栈中向上必须保留队列。

-   网络适配器必须分配足够回填的内存空间中每个 post 预期缓冲区。 这种分配允许向的 post 预期缓冲区中，回填部分复制的预期数据，并允许帧传送到连续缓冲区中的 VM。

如果没有任何机制在硬件以满足这些要求的 VMQ 共享内存，散播-聚集 DMA 支持在接收端的硬件可能会获得相同的结果，通过为每个接收的帧分配两个接收缓冲区。 在这种情况下，第一个缓冲区的大小仅限于所请求的预期大小。

如果网络适配器不能满足 VMQ 的这些要求的任何方法共享内存，VSP 会分配内存，VMQ 从主机地址空间接收缓冲区，并将复制接收数据包的网络适配器从接收到 VM 地址的缓冲区空间。

### <a href="" id="ndis630"></a>Windows Server 2012 和更高版本中如何解决安全问题

从 Windows Server 2012 开始，到 VSP 不会分配共享的内存从虚拟机为 VMQ 接收缓冲区。 相反，VSP 的 VMQ 收到来自主机地址空间的缓冲区，然后副本接收的数据包的网络适配器从接收到 VM 的地址空间的缓冲区分配内存。

以下几点适用于 Windows Server 2012 和更高版本的 Windows 运行的 VMQ 微型端口驱动程序：

-   对于 NDIS 6.20 VMQ 微型端口驱动程序，任何更改不是必需的。 但是，当 VSP 会分配 VM 队列通过发出的 OID （对象标识符） 方法请求[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)，它将设置**LookaheadSize**的成员[ **NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)为零的结构。 这将强制的微型端口驱动程序不会拆分为 pre 预测先行和 post 预测先行缓冲区数据包。

-   从开始 NDIS 6.30，VMQ 微型端口驱动程序必须不播发将数据包数据拆分为 pre 预测先行和 post 预测先行缓冲区的支持。 当微型端口驱动程序注册其 VMQ 功能时，它初始化时，它必须遵循这些规则[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构：

    -   不能设置微型端口驱动程序**NDIS\_接收\_筛选器\_预测先行\_拆分\_支持**标志中**标志**成员。

    -   微型端口驱动程序必须设置**MinLookaheadSplitSize**并**MinLookaheadSplitSize**为零的成员。

    有关如何注册 VMQ 功能的详细信息，请参阅[确定网络适配器的 VMQ 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

 

 





