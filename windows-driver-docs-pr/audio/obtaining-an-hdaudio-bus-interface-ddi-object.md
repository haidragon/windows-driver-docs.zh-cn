---
title: 获取 HDAUDIO_BUS_INTERFACE DDI 对象
description: 获取 HDAUDIO_BUS_INTERFACE DDI 对象
ms.assetid: 78667254-62a6-41fe-af36-43dbdea63aa8
keywords:
- HDAUDIO_BUS_INTERFACE 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564ce09947de9b937ef48c5827b18d0542001fe3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363197"
---
# <a name="obtaining-an-hdaudiobusinterface-ddi-object"></a>获取 HDAUDIO\_总线\_接口 DDI 对象


下表显示了输入的参数值的函数驱动程序将写入到[ **IRP\_MN\_查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IOCTL，以获取[**HDAUDIO\_总线\_界面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)结构和版本的此结构定义 HD 音频 DDI 的上下文对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONST GUID *<em>InterfaceType</em></p></td>
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>大小</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>版本</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>接口</em></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"> <strong>HDAUDIO_BUS_INTERFACE</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

功能驱动程序分配的存储[ **HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)结构，并在 IOCTL 中包含指向此结构的指针。 在前面的表中，指向**HDAUDIO\_总线\_界面**结构转换为类型**PINTERFACE**，这是指向类型的结构的指针[**接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)。 名称和类型的前五个成员**HDAUDIO\_总线\_界面**匹配的五个成员**接口**。 **HDAUDIO\_总线\_接口**包含是 DDI 例程的函数指针的其他成员。 在响应功能驱动程序从接收 IOCTL，HD Audio 总线驱动程序填充整个**HDAUDIO\_总线\_接口**结构。

下表显示值 HD Audio 总线驱动程序将写入到的前五个成员[ **HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>USHORT<strong>大小</strong></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>版本</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>上下文</strong></p></td>
<td align="left"><p>必须作为第一个调用参数传递给每个 DDI 例程的上下文信息</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>指向上下文对象的引用计数会递增的例程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>指向例程递减上下文对象的引用计数</p></td>
</tr>
</tbody>
</table>

 

在上表中，**上下文**成员指向包含特定于基线的客户端获取从 IOCTL HD 音频 DDI 的特定实例的信息的上下文对象。 在调用任何例程中 DDI 时，客户端功能驱动程序必须始终指定**上下文**指针作为第一个调用参数的值。 不透明的客户端的上下文信息。 HD Audio 总线驱动程序为每个客户端创建不同的上下文对象。 当不再需要的上下文对象时，客户端通过调用释放上下文对象**InterfaceDereference**例程上表中所示。 如有必要，客户端可以通过调用创建的对象的其他参考**InterfaceReference**例程，但客户端负责释放这些引用，当不再需要它们。

 

 




