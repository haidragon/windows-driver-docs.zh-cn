---
title: GUID_NDIS_GEN_LINK_STATE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_LINK_STATE GUID。
ms.assetid: 0b0ebb57-33fb-4a18-b6e5-3f4300729280
keywords:
- GUID_NDIS_GEN_LINK_STATE，WDK GUID_NDIS_GEN_LINK_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6048b362463c2ca2bd8c01e4c4f4be74b4a611f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382710"
---
# <a name="guidndisgenlinkstate"></a>GUID_NDIS_GEN_LINK_STATE

WMI 客户端可以使用 GUID_NDIS_GEN_LINK_STATE 方法 GUID 来确定当前的链接状态。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 处理此 GUID 和微型端口驱动程序不会收到一个 OID 查询。

当 WMI 客户端发出 GUID_NDIS_GEN_LINK_STATE WMI 方法请求时，NDIS 返回微型端口适配器或 NDIS 端口的当前链接状态。

WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID，且应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

包含此 GUID 与的 NDIS 返回的数据缓冲区[NDIS_LINK_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构。

微型端口驱动程序在初始化过程中提供的链接状态，并提供更新与状态的指示。 WMI 客户端可以使用 GUID_NDIS_GEN_LINK_STATE GUID 链接状态更改时接收更新。

有关链接状态的详细信息，请参阅[OID_GEN_LINK_STATE](oid-gen-link-state.md)并[NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)。

