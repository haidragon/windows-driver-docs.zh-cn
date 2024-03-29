---
title: 带宽分配
description: 带宽分配
ms.assetid: 775B4085-6028-441F-9D52-341077FF1647
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cba524d36fafd814797c7768573200555bf7fd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354651"
---
# <a name="bandwidth-allocation"></a>带宽分配


带宽分配是增强传输选择 (ETS) 算法的一个组件。 在 IEEE 802.1Qaz 中指定 ETS 草案标准。 此标准是 framework 的 IEEE 802.1 数据中心桥接 (DCB) 接口的一部分。

下 ETS，每个流量类是分配给可用于将两个直接连接的对等方之间的数据包传输的带宽的百分比。 如果完全未使用的带宽分配给流量类，ETS 允许未使用的带宽流量类具有不同的 IEEE 802.1p 优先级级别的共享。

通过指定 NDIS 服务质量 (QoS) 参数[ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构。 **TcBandwidthAssignmentTable**成员包含一个数组，指定使用 ETS 算法的流量类的带宽分配。

有关优先级级别的详细信息，请参阅[IEEE 802.1p 优先级](ieee-802-1p-priority-levels.md)。

 

 





