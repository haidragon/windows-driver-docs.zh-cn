---
title: NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 状态指示通知 NDIS 和基础驱动程序已被封装设置中的更改。
ms.assetid: 2db2a42e-85a2-41a6-b6ab-13b493057648
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9f066bb82d5fdbc9fddb8a67772a7195944fbf5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383278"
---
# <a name="ndisstatusoffloadencaspulationchange"></a>NDIS\_状态\_卸载\_ENCASPULATION\_更改


微型端口驱动程序使用 NDIS\_状态\_卸载\_ENCASPULATION\_更改状态指示通知 NDIS 和基础驱动程序已被封装设置中的更改。

<a name="remarks"></a>备注
-------

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含[ **NDIS\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)结构。 NDIS\_卸载\_封装指定封装设置。

有关封装设置的详细信息，请参阅[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)

 

 




