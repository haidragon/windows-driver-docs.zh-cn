---
title: 响应来自文件系统的 Check-Verify 请求
description: 响应来自文件系统的 Check-Verify 请求
ms.assetid: 227e65d6-d746-4b16-978d-4d42be9aeb2c
keywords:
- 可移动媒体 WDK 内核检查验证请求
- 检查验证请求 WDK 可移动媒体
- 媒体的更改请求 WDK 可移动媒体
- 检查可移动介质的更改
- 验证可移动介质进行的更改
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c62e86aee271216507619a3825b0b24e5071f946
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373391"
---
# <a name="responding-to-check-verify-requests-from-the-file-system"></a>响应来自文件系统的 Check-Verify 请求





自行，文件系统可以将 IRP 发送到设备驱动程序的调度入口点[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) 请求**Parameters.DeviceIoControl.IoControlCode**中 I/O 堆栈设置为以下位置：

<a href="" id="ioctl-xxx-check-verify"></a>IOCTL\_*XXX*\_检查\_验证  
其中*XXX*是设备，如磁盘、 磁带或光盘的类型。

类型为磁盘包括两个 unpartitionable （软盘） 和分区的可移动媒体设备。

如果基础设备驱动程序确定媒体未更改，该驱动程序应完成 IRP，返回**IoStatus**块具有以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>状态</strong></p></td>
<td><p>设置为 STATUS_SUCCESS</p></td>
</tr>
<tr class="even">
<td><p><strong>信息</strong></p></td>
<td><p>设置为零</p></td>
</tr>
</tbody>
</table>

 

此外，如果设备类型为 DISK 或 CDROM 和调用方指定的输出缓冲区，该驱动程序将返回媒体更改缓冲区中的计数**Irp-&gt;AssociatedIrp.SystemBuffer** ，并设置**Irp&gt;IoStatus.Information**到**sizeof**(ULONG)。 通过返回此计数，该驱动程序使调用方有机会以确定是否已从其角度来看更改媒体。

如果基础设备驱动程序确定媒体已发生更改，它将不同的操作，具体取决于是否装载卷。 如果装载卷 (VPB\_VPB 中设置安装标志)，该驱动程序应执行以下操作：

1.  设置**标志**中**DeviceObject**通过实现或运算**标志**使用\_验证\_卷。

2.  设置**IoStatus**中所示 IRP 块：
    -   **状态**将设置为 STATUS\_验证\_必需
    -   **信息**设置为零

3.  调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP 中的输入。

如果未装入卷，该驱动程序必须未设置 DO\_验证\_卷位。 该驱动程序应设置**IoStatus.Status**于状态\_IO\_设备\_错误，设置**IoStatus.Information**为零，并调用**IoCompleteRequest**与 IRP。

 

 




