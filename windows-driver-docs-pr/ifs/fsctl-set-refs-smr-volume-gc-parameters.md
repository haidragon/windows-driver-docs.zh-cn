---
title: FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS 控制代码
description: FSCTL\_设置\_REFS\_SMR\_卷\_GC\_参数用于控制代码控件 Shingled 磁录制 (SMR) 卷上的垃圾回收。
ms.assetid: 782542C4-CFC5-4BF7-AF38-3247A3AC6AB9
keywords:
- FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS
api_location:
- WinIoctl.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75fb4d1f260bfff1624575680709df6efbd60ada
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366249"
---
# <a name="fsctlsetrefssmrvolumegcparameters-control-code"></a>FSCTL\_设置\_REFS\_SMR\_卷\_GC\_参数用于控制代码


**FSCTL\_设置\_REFS\_SMR\_卷\_GC\_参数**控件代码控制 Shingled 磁录制 （垃圾回收SMR) 卷。

```ManagedCPlusPlus
BOOL
   DeviceIoControl( (HANDLE)       hDevice,         // handle to volume
                    FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                     NULL,     // output buffer
                     0,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

<a name="parameters"></a>Parameters
----------

*hDevice* \[in\]  
设备句柄。 若要获取设备句柄，请调用[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。

*dwIoControlCode* \[in\]  
操作的控制代码。 使用**FSCTL\_设置\_REFS\_SMR\_卷\_GC\_参数**对于此操作。

*lpInBuffer*   
指向调用方分配的指针[ **REFS\_SMR\_卷\_GC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_refs_smr_volume_gc_parameters)结构。

*nInBufferSize* \[in\]  
输入缓冲区，以字节为单位的大小。

*lpOutBuffer* \[out\]  
不用于此操作;设置为**NULL**。

*nOutBufferSize* \[in\]  
不用于此操作;设置为零。

*lpBytesReturned* \[out\]  
不用于此操作;设置为**NULL**。

*lpOverlapped* \[in\]  
一个指向[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)结构。

如果*hDevice*而无需指定打开**文件\_标志\_OVERLAPPED**， *lpOverlapped*将被忽略。

如果*hDevice*以打开**文件\_标志\_OVERLAPPED**重叠 （异步） 操作的形式执行的标志，该操作。 在这种情况下， *lpOverlapped*必须指向有效[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)结构，其中包含一个事件对象的句柄。 否则，该函数将失败不可预知的方式。

对于重叠操作， [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)会立即返回，并在操作完成后，发出信号的事件对象。 否则，该函数不返回直到操作完成或发生错误。

<a name="return-value"></a>返回值
------------

如果操作成功，完成[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)返回非零值。

如果操作失败或已挂起[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)返回零。 若要获得扩展错误信息，请调用[ **GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>从 Windows 10，版本 1709年开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">WinIoctl.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

 

 






