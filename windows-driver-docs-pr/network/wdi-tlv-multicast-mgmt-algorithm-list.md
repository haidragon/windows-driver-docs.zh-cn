---
title: WDI_TLV_MULTICAST_MGMT_ALGORITHM_LIST
description: WDI_TLV_MULTICAST_MGMT_ALGORITHM_LIST 是 TLV 包含多播的管理算法对的数组。
ms.assetid: 96EAD5FE-71C7-4B3E-BB52-06FA50F375D8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_MULTICAST_MGMT_ALGORITHM_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 043476559e82a270988bcb7702365b07f01a9af5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371175"
---
# <a name="wditlvmulticastmgmtalgorithmlist"></a>WDI\_TLV\_多播\_MGMT\_算法\_列表


WDI\_TLV\_多播\_MGMT\_算法\_列表是 TLV 包含多播的管理算法对的数组。

## <a name="tlv-type"></a>TLV 类型


0x15

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_ALGO\_对元素。 该数组必须包含一个或多个元素。

**请注意**  WDI\_ALGO\_对不是 WDI 结构。 它定义在 WDI TLV 分析器生成器，并仅供文档使用。

 

算法对的数组大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                 | 描述                                            |
|----------------------|--------------------------------------------------------|
| WDI\_ALGO\_PAIRS\[\] | 身份验证和加密算法对的数组。 |

 

WDI\_ALGO\_对以下元素组成。

| 在任务栏的搜索框中键入  | 描述                                                                                     |
|-------|-------------------------------------------------------------------------------------------------|
| UINT8 | 如中所定义的身份验证算法[ **WDI\_身份验证\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)。 |
| UINT8 | 如中所定义的密码算法[ **WDI\_密码\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm)。     |

 

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

 

 




