---
title: OID_PM_ADD_WOL_PATTERN
description: 作为一组协议的 NDIS 驱动程序使用 OID_PM_ADD_WOL_PATTERN OID 将电源管理唤醒 LAN 模式添加到网络适配器。 NDIS_OID_REQUEST 结构的 InformationBuffer 成员包含指向 NDIS_PM_WOL_PATTERN 结构的指针。
ms.assetid: 1005cebb-8ead-4d16-b3ea-5a74da0b054f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_ADD_WOL_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2c1883914b91b8c4316433adbb880b9e91eb5879
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383245"
---
# <a name="oidpmaddwolpattern"></a>OID\_PM\_添加\_WOL\_模式


作为一组协议的 NDIS 驱动程序使用 OID\_PM\_添加\_WOL\_模式 OID 将电源管理唤醒 LAN 模式添加到网络适配器。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID\_PM\_添加\_WOL\_模式，以将唤醒 LAN (WOL) 模式添加到网络适配器。 OID 请求包含处于低功耗状态时，网络适配器必须比较对传入数据包的条件。 网络适配器必须生成唤醒事件时接收的数据包，匹配模式条件。

已成功将其绑定到基础的网络适配器后，只要它具有所需的数据 （如接口的 IP 地址） 来设置 WOL 模式，协议驱动程序可以添加 WOL 模式。 协议驱动程序还可以添加一些其他电源管理事件通知，例如拒绝以前添加的 WOL 模式或卸载的协议的响应的 WOL 模式。

若要避免 NDIS 和 NDIS 启动将网络适配器设置为低功耗状态后绑定到相同的微型端口适配器，其他协议驱动程序中的争用条件，操作将失败尝试向该网络适配器上添加新模式唤醒。 例如，如果 NDIS 协议驱动程序尝试处理的上下文中添加新的 WOL 模式**NetEventSetPower**为该网络适配器，NDIS 事件通知将会使请求失败。

NDIS 发送到基础的 NDIS 驱动程序此 OID 请求或对基础驱动程序的请求完成之前，它会设置 ULONG **PatternId**的成员[ **NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)为唯一值的结构。 协议驱动程序和 NDIS 使用与此模式标识符[OID\_PM\_删除\_WOL\_模式](oid-pm-remove-wol-pattern.md)OID 请求将从基础的网络适配器中删除的 WOL 模式。

**请注意**  模式标识符是为每个网络适配器设置的模式的唯一值。 但是，模式标识符不是全局唯一跨所有微型端口适配器。

 

如果 NDIS 或基础的网络适配器中删除的 WOL 模式，它将生成[ **NDIS\_状态\_PM\_WOL\_模式\_已拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)状态指示。 **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含已拒绝的 ULONG WOL 模式标识符WOL 模式。

微型端口驱动程序返回请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
已成功添加请求的模式。 **PatternId**成员的 NDIS\_PM\_WOL\_模式结构包含的模式标识符。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求之后。

<a href="" id="ndis-status-pm-wol-pattern-list-full"></a>NDIS\_状态\_PM\_WOL\_模式\_列表\_完整  
请求失败，因为模式列表已满，网络适配器不能添加另一种模式。

<a href="" id="ndis-status-resources"></a>NDIS\_状态\_资源  
NDIS 或基础网络适配器无法添加新的模式因缺少资源。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
一个或多个参数在 NDIS\_PM\_WOL\_模式结构无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓冲区\_过\_短  
信息缓冲区太短。 NDIS 集**数据。设置\_信息。BytesNeeded** NDIS 中的成员\_OID\_结构到最小缓冲区大小的请求是必需的。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状态\_不\_支持  
网络适配器不支持所请求的 WOL 模式。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求失败，而原因并非前面的原因。

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
<td><p>支持 NDIS 6.20 及更高版本。 对于微型端口驱动程序是必需的。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_WOL\_PATTERN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状态\_PM\_WOL\_模式\_已拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)

[OID\_PM\_REMOVE\_WOL\_PATTERN](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_ADD\_WAKE\_UP\_PATTERN](oid-pnp-add-wake-up-pattern.md)

 

 




