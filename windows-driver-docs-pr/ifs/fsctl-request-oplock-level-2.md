---
title: FSCTL_REQUEST_OPLOCK_LEVEL_2 控制代码
description: FSCTL\_请求\_OPLOCK\_级别\_2 的控制代码请求文件中的级别 2 机会锁 (oplock)。
ms.assetid: 418fbbc7-5dca-4c73-8ea0-d4b4e0a2efff
keywords:
- FSCTL_REQUEST_OPLOCK_LEVEL_2 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_REQUEST_OPLOCK_LEVEL_2
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9abd44005006ee6e2e937571cea4d3bdf73d6786
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519303"
---
# <a name="fsctlrequestoplocklevel2-control-code"></a>FSCTL\_请求\_OPLOCK\_级别\_2 控制代码


**FSCTL\_请求\_OPLOCK\_级别\_2**控件的代码请求文件中的级别 2 机会锁 (oplock)。

若要处理此控制代码，微筛选器调用[ **FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)使用以下参数。 文件系统或旧筛选器驱动程序调用[ **FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)。

有关详细信息，有关伺机锁定和大约**FSCTL\_请求\_OPLOCK\_级别\_2**控制代码，请参阅 Microsoft Windows SDK 文档。

**参数**

<a href="" id="oplock"></a>*Oplock*  
该文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)仅。 回调数据 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 的 IRP 结构\_MJ\_文件\_系统\_控件 FSCTL请求。 *FsControlCode*操作的参数必须为 FSCTL\_请求\_OPLOCK\_级别\_2。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)仅。 IRP 的 IRP\_MJ\_文件\_系统\_控件 FSCTL 请求。 *FsControlCode*操作的参数必须为 FSCTL\_请求\_OPLOCK\_级别\_2。

<a href="" id="opencount"></a>*OpenCount*  
指定文件的锁定状态。 如果没有字节范围锁定在该文件，则为零; 否则为，此参数设置为非零的 ULONG 值。

<a name="status-block"></a>状态块
------------

[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)返回 FLT\_PREOP\_PENDING 如果 oplock 已被授予此操作。 否则，它将返回 FLT\_PREOP\_完成。

[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)返回值对于此操作的以下 NTSTATUS 之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>被授予 oplock。 这是一个成功代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>IRP FSCTL_REQUEST_OPLOCK_LEVEL_2 操作已完成之前取消。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>不被授予 oplock。 这是一个错误代码。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FLT\_IRP 的参数\_MJ\_文件\_系统\_控件**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff543398)

[**FSCTL\_OPBATCH\_ACK\_CLOSE\_PENDING**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL\_OPLOCK\_BREAK\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_BREAK\_ACKNOWLEDGE**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_BREAK\_NOTIFY**](fsctl-oplock-break-notify.md)

[**FSCTL\_REQUEST\_BATCH\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_REQUEST\_FILTER\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_REQUEST\_OPLOCK\_LEVEL\_1**](fsctl-request-oplock-level-1.md)

[**FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 





