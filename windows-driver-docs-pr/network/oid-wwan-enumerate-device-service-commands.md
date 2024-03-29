---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS
description: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 返回设备服务支持的命令列表。包含描述操作的结果的 NDIS_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 结构 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状态通知。
ms.assetid: 9888E4EC-D4BB-4BAC-B20B-DFA51005EEDA
ms.date: 08/08/2017
keywords: -OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 388538b352ad2b280ed31d5829fc4284eb0e1b8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385493"
---
# <a name="oidwwanenumeratedeviceservicecommands"></a>OID\_WWAN\_ENUMERATE\_设备\_服务\_命令


OID\_WWAN\_ENUMERATE\_设备\_服务\_命令返回的设备服务支持的命令的列表。

不支持组的请求。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_服务\_支持\_命令**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)状态通知包含[ **NDIS\_WWAN\_ENUMERATE\_设备\_服务\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands)结构描述操作的结果。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持指定的设备服务或操作支持。

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
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_WWAN\_设备\_服务\_支持\_命令**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)

[**NDIS\_WWAN\_ENUMERATE\_DEVICE\_SERVICE\_COMMANDS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands)

 

 




