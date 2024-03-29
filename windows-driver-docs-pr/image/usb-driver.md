---
title: USB 驱动程序
description: USB 驱动程序
ms.assetid: c20bd393-98d0-498e-a3e8-bbd1958ed774
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa18b333309f23a08e2eebbcc8587737f3b5e83d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358224"
---
# <a name="usb-driver"></a>USB 驱动程序





内核模式下的仍映像驱动程序对于 USB 总线支持的单个控件终结点，以及多个中断、 大容量 IN 和 OUT 终结点的大容量。 控件和中断终结点都使用 I/O 控制代码可以访问并[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)。 大容量终结点都可以访问使用**ReadFile**并**WriteFile**。

然后再调用[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)， **ReadFile**，或者**WriteFile**，必须调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) （所有的 Microsoft Windows SDK 文档中介绍） 以获得设备句柄。 支持不超过每个终结点类型之一的设备 （控制、 中断、 大容量 IN，大容量），调用一次**CreateFile**打开将管道传输到每个终结点。

对于支持多个中断或大容量的终结点的设备，将单个调用到[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)打开将管道传输到每种类型的编号最高的终结点。 如果你想要使用不同的终结点，必须执行以下操作：

1.  调用[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)，指定的 I/O 控制代码[ **IOCTL\_获取\_管道\_配置** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_pipe_configuration)，以确定端口的终结点的索引编号 (即，通过索引返回[ **USBSCAN\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_pipe_information)结构数组）。 请注意，这些索引编号*不*中所述的终结点号*通用串行总线规范*。

2.  将反斜杠和终结点的索引号追加到返回的端口名称[ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)调用 CreateFile 时。

例如，假设 （具有"usbscan0"的端口名称） 的设备具有每种类型的两个终结点 （中断，大容量 IN，大容量），使用索引号，如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>索引</th>
<th>在任务栏的搜索框中键入</th>
<th>终结点 #</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>中断</p></td>
<td><p>0x01</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>大容量中</p></td>
<td><p>0x82</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>大容量中</p></td>
<td><p>0x83</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>扩展大容量</p></td>
<td><p>0x04</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>扩展大容量</p></td>
<td><p>0x05</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>中断</p></td>
<td><p>0x06</p></td>
</tr>
</tbody>
</table>

 

如果您调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) "usbscan0"为端口名称，函数将打开具有索引 2、 4 和 5，值的终结点，以及控制终结点的传输管道。

如果您调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)端口名称为"usbscan0\\1"，该函数将打开具有索引值 1、 4 和 5，终结点，以及控制终结点的传输管道。

为此设备，如果你想要使用中断终结点 0、 大容量 IN 终结点 1，以及输出终结点 3 大容量，则调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)三次，指定的端口名称"usbscan0\\0"，"usbscan0\\1"和"usbscan0\\3"。 这将创建三个设备句柄。 每当的后续调用[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)， **ReadFile**，或者**WriteFile**进行时，与关联的设备句柄应指定所需的管道。

由于支持只有一个控制终结点，指定任何使用控制管道的 I/O 控制代码会导致驱动程序使用正确的终结点，而不考虑哪个终结点 （如果有） 指定给[ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea).

所有的 I/O 控制代码的说明，请参阅[USB 仍映像 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)。

内核模式 USB 驱动程序未实现包或消息的协议。 读取操作不需要任何特定的数据包的对齐方式，但如果在读取请求最大数据包大小边界对齐，则可以实现更好的性能。 可以使用获取的最大数据包大小[ **IOCTL\_获取\_通道\_对齐\_用户心声**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_channel_align_rqst) I/O 控制代码。

 

 




