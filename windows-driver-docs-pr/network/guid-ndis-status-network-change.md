---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_NETWORK_CHANGE GUID。
ms.assetid: 4be2b79d-dc99-4096-bf13-54e75deeee56
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE，WDK GUID_NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55cadd37180a81e71cbbac256450f30bbf998d39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382682"
---
# <a name="guidndisstatusnetworkchange"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE 事件 GUID 表示的三层地址必须重新协商。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 或微型端口驱动程序才能生成[NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)状态指示报告网络状态中的更改。

当微型端口驱动程序或 NDIS 指示网络状态中的更改时，NDIS 将转换为 WMI GUID_NDIS_STATUS_NETWORK_CHANGE 事件的 WMI 客户端的状态指示。

NDIS 提供具有此 GUID 的数据缓冲区包含[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)跟 NDIS_NETWORK_CHANGE_TYPE 类型化值的结构。 有关可能的值的列表，请参阅[NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)。

