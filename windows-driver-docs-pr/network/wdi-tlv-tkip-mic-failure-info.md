---
title: WDI_TLV_TKIP_MIC_FAILURE_INFO
description: WDI_TLV_TKIP_MIC_FAILURE_INFO 是 TLV 包含 TKIP MIC 失败信息。
ms.assetid: BBF168BE-6223-4C54-AFF5-17878D07EFBD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TKIP_MIC_FAILURE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 76aa968fae4c3be1ce61d052e9bfe83db1a6c7b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357312"
---
# <a name="wditlvtkipmicfailureinfo"></a>WDI\_TLV\_TKIP\_MIC\_FAILURE\_INFO


WDI\_TLV\_TKIP\_MIC\_失败\_信息是包含 TKIP MIC 失败信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x57

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                                                                                              |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 指定哪个密码密钥类型检测到出现 TKIP MIC 失败。 如果此值为 1，TKIP MIC 故障检测到通过默认的密码密钥。 如果此值为 0，TKIP MIC 故障检测到通过密钥映射密码密钥。 |
| UINT32                                            | 默认密钥数组中指定密码密钥的索引。 有效的值范围是从 0 到 3。                                                                                                                                                   |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定传输的数据包的 MIC 验证失败的对等方的 MAC 地址。                                                                                                                                                          |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




