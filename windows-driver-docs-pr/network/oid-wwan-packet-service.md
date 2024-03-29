---
title: OID_WWAN_PACKET_SERVICE
description: OID_WWAN_PACKET_SERVICE 用于指示微型端口驱动程序为基于 GSM 的和基于 CDMA 的 MB 设备的当前已注册提供程序的网络上执行数据包服务附加/分离操作。
ms.assetid: 97bb9324-8052-437c-baa5-fb9a8176c779
ms.date: 04/04/2019
keywords: -从 Windows Vista 开始 OID_WWAN_PACKET_SERVICE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 96229795d60683f4185809b5ba47ee8f73b0604e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360783"
---
# <a name="oidwwanpacketservice"></a>OID\_WWAN\_PACKET\_SERVICE


OID\_WWAN\_数据包\_服务用来指示微型端口驱动程序为基于 GSM 的和基于 CDMA 的 MB 设备的当前已注册提供程序的网络上执行数据包服务附加/分离操作。 除了数据包服务附加/分离状态，此 OID 用于确定数据的可用性和当前使用的数据类信息。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_数据包\_服务**](ndis-status-wwan-packet-service.md)状态通知包含[ **NDIS\_WWAN\_数据包\_服务\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_packet_service_state)结构，以便提供而不考虑完成组的当前数据包服务状态有关的信息或查询请求。

调用方请求以设置当前数据包服务状态提供[ **NDIS\_WWAN\_设置\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service)结构微型端口驱动程序的相应信息。

<a name="remarks"></a>备注
-------

请参阅[WWAN 数据包服务附加操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-service-attach-operations)有关使用此 OID 的详细信息。

微型端口驱动程序可以访问提供程序网络时处理查询或设置操作，但不是应访问用户识别模块 （SIM 卡）。

基于 CDMA 的设备应使用此机会来释放网络资源分配在可能的情况。

某些 SIM 卡启用 MB 设备仅在数据包域和非电路交换域上注册。 一旦数据调用结束，VAN UI 会发送一个 OID\_WWAN\_数据包\_服务集分离数据包服务的请求。 这会导致要从数据包域分离的 MB 设备。 从网络中的 MB 设备取消注册并进入 power 保存模式。 因此，设备从作为要注销，结果 VAN UI 中消失，并且只能通过重新启动恢复。 在此方案中，微型端口驱动程序应通过返回正数据而无需设置到此类模式的 MB 设备欺骗数据包附加/分离操作。

有关不支持数据包附加的技术，微型端口驱动程序应欺骗的附加状态，以便知道它可以继续进行上下文激活 MB 服务。 微型端口驱动程序还应伪造集 OID\_WWAN\_数据包\_微型端口驱动程序中的服务请求。 微型端口驱动程序应发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](ndis-status-wwan-packet-service.md)通知查询操作和为未经请求事件。 如果设备数据包服务状态未设置为微型端口驱动程序应失败 PDP 激活*WwanPacketServiceStateAttached*。

之前已达到数据包服务状态，MB 服务应继续上下文激活*WwanPacketServiceStateAttached*。

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

在 Windows 10，版本 1903年开始支持此 OID 的新修订版本 2。 该扩展使宿主能够查询中的调制解调器当前操作系统 5g 中的频率范围。

主机可以查询在任何时间的扩展的数据包服务状态信息。 响应是修订版 1，与相同，只不过修订版本 2 有两个新字段。

如果调制解调器在 5g 域中注册，则返回的承运人的 5g 频率范围。 如果存在多个 5g 运营商，则返回所有的有效范围。

5 G 数据类支持的详细信息，请参阅[MB 5g 数据类支持](mb-5g-data-class-support.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_SET\_PACKET\_SERVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_packet_service)

[**NDIS\_STATUS\_WWAN\_PACKET\_SERVICE**](ndis-status-wwan-packet-service.md)

[WWAN 数据包服务附加操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-packet-service-attach-operations)

 

 




