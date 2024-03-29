---
title: OID_WWAN_DEVICE_SLOT_MAPPING_INFO
description: OID_WWAN_DEVICE_SLOT_MAPPING_INFO 设置或返回的 MB 设备 （即执行器-slot 映射） 的设备-slot 映射。
ms.assetid: 54AF3447-7918-49CE-945A-DC8DC1E78CBF
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SLOT_MAPPING_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 31294f80732f686d84ca212f31865e9b1458dc10
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358600"
---
# <a name="oidwwandeviceslotmappinginfo"></a>OID\_WWAN\_设备\_槽\_映射\_信息


OID\_WWAN\_设备\_槽\_映射\_信息设置或返回的 MB 设备 （即执行器-slot 映射） 的设备-slot 映射。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[ **NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)状态通知包含[ **NDIS\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)结构，以提供了有关执行器槽映射信息。

下图说明了查询请求。

![插槽映射查询](images/multi-SIM_8_slotMappingQuery.png)

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[ **NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)状态通知包含[ **NDIS\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)结构，其中又包含[ **WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_slot_mapping_info)结构，以指示当前映射状态。 即使集请求失败，这为 true。 有关 OID 的集请求的结构\_WWAN\_设备\_槽\_映射\_信息[ **NDIS\_WWAN\_设置\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)。

下图说明了 set 请求。

![插槽映射集](images/multi-SIM_7_slotMappingSet.png)

<a name="remarks"></a>备注
-------

主机需要，在首次启动调制解调器具有槽和执行器之间的默认映射。 宿主执行设置操作中的使用 OID\_WWAN\_设备\_槽\_映射\_信息来定义绑定到每个执行器的槽。 主机需要调制解调器，若要在重新启动和删除/插入维护映射。 此 OID 不特定于执行器的可能会发送到任何设备上的 NDIS 实例。 它还可能会查询当前映射，如上所示。

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
<td><p>Windows 10，版本 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)

[**NDIS\_WWAN\_DEVICE\_SLOT\_MAPPING\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

[**NDIS\_WWAN\_SET\_DEVICE\_SLOT\_MAPPING\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)

 

 




