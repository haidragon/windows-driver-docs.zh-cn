---
title: 磁带 Miniclass 驱动的 DriverEntry 例程
description: DriverEntry 初始化磁带 miniclass 驱动程序。 此例程是必需的。
ms.assetid: dc082f31-5ec5-491e-a347-8f8e485c042b
keywords:
- DriverEntry 例程存储设备
topic_type:
- apiref
api_name:
- DriverEntry
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1407c3fc2fb9035754ae0b72659b3e94ac9bab4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368259"
---
# <a name="driverentry-of-tape-miniclass-driver-routine"></a>磁带 Miniclass 驱动的 DriverEntry 例程


**DriverEntry**初始化磁带 miniclass 驱动程序。 此例程是必需的。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
ULONG DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>Parameters
----------

*Argument1* \[中\]  
磁带 miniclass 驱动程序将传递给驱动程序上下文的指针[ **TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclassinitialize)。 上下文信息的格式是特定于操作系统的和可移植磁带 miniclass 驱动程序必须解释。

*Argument2* \[中\]  
磁带 miniclass 驱动程序将传递给第二个上下文结构的指针**TapeClassInitialize**。 上下文信息的格式是特定于操作系统的和可移植磁带 miniclass 驱动程序必须解释。

<a name="return-value"></a>返回值
------------

**DriverEntry**返回到其调用所返回的值**TapeClassInitialize**。

<a name="remarks"></a>备注
-------

**DriverEntry**是磁带 miniclass 驱动程序的初始入口点。

由于**TapeClassInitialize**执行所需的驱动程序初始化，磁带 miniclass 驱动程序的主要任务的大部分**DriverEntry**例程是分配，并填写磁带\_INIT\_数据\_例如包含特定于驱动程序常量和入口点的结构。

**DriverEntry**必须先调用[ **TapeClassZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclasszeromemory)以清除磁带\_INIT\_数据\_EX 结构。 **DriverEntry**然后结构中设置的值和指针。

**DriverEntry**调用**TapeClassInitialize** ，并将磁带的地址传递\_INIT\_数据\_EX 和两个指针传递给**DriverEntry**(*Argument1*并*Argument2*)。 **TapeClassInitialize**完成驱动程序初始化并返回到磁带 miniclass 驱动程序的状态**DriverEntry**例程。 **DriverEntry**返回其从收到的状态**TapeClassInitialize**。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Minitape.h</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**TAPE\_INIT\_DATA\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/ns-minitape-_tape_init_data_ex)

[**TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclassinitialize)

[**TapeClassZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclasszeromemory)

[**磁带\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/ne-minitape-_tape_status)

 

 






