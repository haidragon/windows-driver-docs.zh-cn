---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 是包含 Wi-Fi Direct TLV 发送操作帧结果参数。
ms.assetid: A0B234F2-081B-4027-9B42-76401F600707
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 214aed1e2bf69476a68d96911eb38fac840fb97d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353292"
---
# <a name="wditlvp2psendactionframeresultparameters"></a>WDI\_TLV\_P2P\_发送\_操作\_帧\_结果\_参数


WDI\_TLV\_P2P\_发送\_操作\_帧\_结果\_参数是包含 Wi-Fi Direct TLV 发送操作帧结果参数。

## <a name="tlv-type"></a>TLV 类型


0xAE

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                           |
|---------------------------------------------------|-------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目标 Wi-Fi Direct 设备的设备地址。 |
| UINT8                                             | Wi-Fi Direct 对话框标记，表示此事务。   |

 

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

 

 




