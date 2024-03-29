---
title: 拆分上层协议标头开头的帧
description: 拆分上部的层协议标头的开始处的帧
ms.assetid: 2559ac20-46dc-4116-9d12-b2cd634e501b
keywords:
- 以太网帧拆分 WDK 连接网络、 的上层协议的开头
- 上层协议 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80e240f7aeacc537ef6af82441008899f9109aaf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383624"
---
# <a name="splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers"></a>拆分上部的层协议标头的开始处的帧





*上层协议*是如 TCP、 UDP 或 ICMP 的 IP 传输协议。

**请注意**  IPsec 不被视为标头数据拆分要求中右上层协议。 有关拆分 IPsec 帧的详细信息，请参阅[拆分 IPsec 帧](splitting-ipsec-frames.md)。

 

如果 NIC 会拆分上限层协议标头，所指示的开始处的以太网帧[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)必须包含正好两个 MDLs。 缓冲区的第一个 MDL 介绍必须以与以太网帧 （MAC 标头） 的第一个字节，并且介绍了第二个 MDL 缓冲区必须开头上限层协议标头的第一个字节。

**请注意**  NIC 可以拆分的 TCP 或 UDP 负载在 TCP 和 UDP 帧。 有关详细信息，请参阅[拆分帧 TCP 有效负载](splitting-frames-at-the-tcp-payload.md)并[拆分帧 UDP 负载](splitting-frames-at-the-udp-payload.md)。

 

如果标头数据拆分提供程序将拆分上限层协议标头，所指示的开始处的帧[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构必须具有NDIS\_NBL\_标志\_拆分\_处\_上部\_层\_协议\_中设置标头标志**NblFlags**成员。 有关详细信息，有关设置标头数据拆分 NET\_缓冲区\_标志列表，请参阅[设置 NET\_缓冲区\_列表信息](setting-net-buffer-list-information.md)。

如果得到的标头缓冲区具有更高版本长度超过了最大标头大小，NIC 必须不会拆分一个帧。 当超过最大标头大小拆分帧的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

 

 





