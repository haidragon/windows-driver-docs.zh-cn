---
title: ENCAPIPARAM\_PEAK\_BITRATE
description: ENCAPIPARAM\_PEAK\_BITRATE
ms.assetid: 444a20e0-f3af-4dbc-9272-44e992e059e8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23d9cc133b18d3ea490580d6a6bed85bc334ec76
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384139"
---
# <a name="encapiparampeakbitrate"></a>ENCAPIPARAM\_PEAK\_BITRATE


## <span id="ddk_encapiparam_peak_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_PEAK_BITRATE_KS"></span>


ENCAPIPARAM\_比特率属性用于描述设备的受支持的峰值位速率 （每秒位数） 范围。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 VT\_UI4 单步执行范围高峰期的比特率的中指定的设备**PropertyItem.Values**的成员[ **KSPROPERTY\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)结构。

### <a name="comments"></a>备注

微型驱动程序时需要提供一个静态**PropertyItem.Values**说明中的属性项或句柄基本支持的查询，并填充值。 微型驱动程序还必须指定此属性的默认值。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)， [ **VIDEOENCODER\_比特率\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 





