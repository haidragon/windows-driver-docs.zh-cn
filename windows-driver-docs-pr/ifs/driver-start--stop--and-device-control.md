---
title: 驱动程序启动、停止和设备控制
description: 驱动程序启动、停止和设备控制
ms.assetid: d3608a5f-3bf4-43b1-8c32-55a6fcd4fbe8
keywords:
- 最小重定向程序 WDK，启动
- 最小重定向程序 WDK，停止
- 最小重定向程序 WDK，设备控件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b53fc50e8a1b5b1c314a9e1dc239f797dfa7c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386095"
---
# <a name="driver-start-stop-and-device-control"></a>驱动程序启动、停止和设备控制


在中处理驱动程序注册**DriverEntry**例程的网络的最小重定向程序驱动程序。 网络微型重定向的第一次启动 (在其**DriverEntry**例程)，该驱动程序必须调用 RDBSS [ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)例程，以注册网络微型重定向与 RDBSS。 网络微型重定向传入 MINIRDR\_调度结构包括网络微型重定向程序驱动程序实现的例程的配置数据和例程的指针 （调度表） 的表。

[ **MRxStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx)并[ **MRxStop** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)例程必须实现网络微型重定向程序驱动程序，以允许将驱动程序启动和停止。

要启动或停止网络微型重定向的序列很复杂。 此序列通常由用户模式应用程序或使用网络微型重定向程序驱动程序提供的服务控制管理和管理目的的驱动程序启动。 网络微型-重定向程序可以使用配置为在操作系统启动时自动启动的服务。 此服务可以请求每次操作系统启动时启动网络微型重定向。

[**MRxStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx) RDBSS 调用时[ **RxStartMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr)调用例程。 **RxStartMinirdr**例程通常从启动网络微型重定向的用户模式应用程序或服务调用 FSCTL 或 IOCTL 请求的结果。 在调用**RxStartMinirdr**不能从进行**DriverEntry**网络微型-重定向程序在成功调用后的日常[ **RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)因为一些开始处理需要完成驱动程序初始化。 一次**RxStartMinirdr**接收到调用、 RDBSS 完成启动过程通过调用**MRxStart**网络微型重定向的例程。 如果在调用**MRxStart**返回成功，RDBSS 设置最小-重定向程序的内部状态中到 RDBSS RDBSS\_已启动。

[**MRxStop** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop) RDBSS 调用时[ **RxStopMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr)调用例程。 RDBSS **RxStopMinirdr**例程通常从停止网络微型重定向的用户模式应用程序或服务调用 FSCTL 或 IOCTL 请求的结果。 此调用也可从网络微型重定向，或关闭过程的一部分操作系统。 一次**RxStopMinirdr**接收到调用、 RDBSS 通过调用来完成该过程**MRxStop**网络微型重定向的例程。

[ **MRxDevFcbXXXControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile)例程用于接收来自通过 IOCTL 或 FSCTL 调用 FCB 的设备上控制网络微型重定向的用户模式应用程序或服务请求。

此外，有两个较低的 I/O 例程处理 IOCTL 和 FSCTL 驱动程序对象上的操作：[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]**  ](https://msdn.microsoft.com/library/windows/hardware/ff550709)并[ **MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](https://msdn.microsoft.com/library/windows/hardware/ff550715)。

网络微型重定向也可以使用这些较低的 I/O 例程提供控制和管理网络微型-重定向程序从用户模式应用程序或服务。

下表列出了可以由网络微型重定向的启动 （停止） 和设备控制操作实现的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile" data-raw-source="[&lt;strong&gt;MRxDevFcbXXXControlFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile)"><strong>MRxDevFcbXXXControlFile</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将传递给网络微型重定向的设备 FCB 控制请求。 RDBSS 发出响应 FCB 的设备上接收 IRP_MJ_DEVICE_CONTROL、 IRP_MJ_FILE_SYSTEM_CONTROL 或 IRP_MJ_INTERNAL_DEVICE_CONTROL 此调用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以启动网络微型重定向。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以停止网络微型重定向。</p></td>
</tr>
</tbody>
</table>

 

 

 




