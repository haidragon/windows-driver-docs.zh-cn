---
title: 发出 OID_NIC_SWITCH_FREE_VF 请求
description: 发出 OID_NIC_SWITCH_FREE_VF 请求
ms.assetid: D9A8548C-02D8-4537-9053-6B262004CBC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d56ee45376cc9e3f3a53d424ee08d384bfe1ebf7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356250"
---
# <a name="issuing-oidnicswitchfreevf-requests"></a>发出 OID\_NIC\_交换机\_免费\_VF 请求


基础驱动程序发出的一个对象标识符 (OID) 组请求[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放资源的 PCI Express (PCIe) 虚拟函数 (VF)。 这些资源之前通过 OID 方法请求的分配[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

过量的驱动程序问题[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)微型端口驱动程序集请求 PCIe 物理函数 (PF) 有关。 它会发出此 OID 请求之前，基础驱动程序必须执行以下操作：

1.  基础驱动程序必须确保，VF 未附加到任何虚拟端口 (VPort) NIC 交换机的网络适配器上。 基础驱动程序必须发出的 OID 集请求[OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)若要删除所有附加到 VF 的 VPorts。 有关详细信息，请参阅[删除虚拟端口](deleting-a-virtual-port.md)。

2.  基础驱动程序初始化[ **NDIS\_NIC\_交换机\_免费\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构。 该驱动程序必须设置**VFId**成员添加到返回的 OID 方法请求中的取景器标识符[OID\_NIC\_开关\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf).

基础驱动程序将发出的 OID 集请求[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)通过执行以下步骤：

1.  基础驱动程序初始化[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID 方法请求的结构。 驱动程序集**InformationBuffer**指向一个已初始化的指针到成员[ **NDIS\_NIC\_开关\_免费\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构。

2.  过量的驱动程序调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest) OID 请求发出到基础 PF 微型端口驱动程序。

基础驱动程序请求 VF 的资源分配后，该驱动程序将是可以请求的同一 VF 释放资源的唯一组件。 基础驱动程序必须发出的 OID 集请求[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 VF 资源。 可以暂停基础驱动程序之前，它必须释放资源的已分配的驱动程序的每个 VF [OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)请求。

**请注意**  如果过量的驱动程序发出的 OID 方法请求[OID\_NIC\_开关\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)为 VF 分配资源，驱动程序是可以请求的同一 VF 释放资源的唯一组件。 基础驱动程序必须发出的 OID 集请求[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 VF 资源。 可以暂停基础驱动程序之前，它必须释放资源，为每个已分配的驱动程序的 OID 的 VF\_NIC\_交换机\_分配\_VF 请求。

 

 

 





