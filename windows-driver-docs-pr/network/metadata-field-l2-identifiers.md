---
title: 元数据字段 L2 标识符
description: 本部分介绍 Windows 筛选平台标注驱动程序的元数据字段 L2 标识符。
ms.assetid: 4A03C593-3760-48F0-A082-A9D1AD90EAD6
keywords:
- 元数据字段 L2 标识符网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36239d3d8397a74cf6aad9a1081e3428e7b42fa2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373982"
---
# <a name="metadata-field-l2-identifiers"></a>元数据字段 L2 标识符

Windows 8 和 Windows Server 2012 引入了元数据字段 L2 标识符。

每个由位域元数据字段 L2 标识符表示。 这些标识符定义，如下所示：

| 元数据字段标识符 | 描述 |
| --- | --- |
| FWPS_L2_METADATA_FIELD_ETHERNET_MAC_HEADER_SIZE | 以字节为单位，MAC 标头的大小。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_DESTINATION_PORT_ID | 在虚拟交换机上的目标端口的标识符。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_PACKET_CONTEXT | 一个**处理**到虚拟交换机数据包上下文。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_NIC_INDEX | 源 NIC 的虚拟交换机上的索引。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_PORT_ID | 在虚拟交换机上的源端口标识符。 |
| FWPS_L2_METADATA_FIELD_WIFI_OPERATION_MODE | 当前本机 802.11 操作模式。 |

## <a name="related-topics"></a>相关主题

[元数据的字段标识符](metadata-field-identifiers.md)

[在每个筛选层的元数据字段](metadata-fields-at-each-filtering-layer.md)

[FWPS_INCOMING_METADATA_VALUES0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)

