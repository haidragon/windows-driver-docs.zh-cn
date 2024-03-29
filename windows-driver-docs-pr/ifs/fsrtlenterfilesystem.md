---
title: FsRtlEnterFileSystem 函数
description: FsRtlEnterFileSystem 宏暂时禁用普通的内核模式下异步过程调用 (APC) 的传递。 仍提供特殊的内核模式 Apc。
date: 06/25/2019
ms.assetid: 6aa6315d-e430-4189-8eb5-9427a2e5ba46
keywords:
- FsRtlEnterFileSystem 函数可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FsRtlEnterFileSystem
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df21f165ebb51f6a55de87d375b4226696e026ff
ms.sourcegitcommit: 61d5dccad989614313be2e59df6e08cd46364e76
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412218"
---
# <a name="fsrtlenterfilesystem-function"></a>FsRtlEnterFileSystem 函数

**FsRtlEnterFileSystem**宏暂时禁用的普通的内核模式下异步过程调用 (APC) 传递。 仍提供特殊的内核模式 Apc。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
VOID FsRtlEnterFileSystem(
   VOID
);
```

## <a name="parameters"></a>Parameters

无

## <a name="return-value"></a>返回值

此函数不返回值。

## <a name="remarks"></a>备注

必须调用每个文件系统驱动程序入口点例程**FsRtlEnterFileSystem**立即才会获取在执行文件 I/O 所需的资源请求并调用[ **FsRtlExitFileSystem**](fsrtlexitfilesystem.md)此后立即。 这可确保不能暂停该例程，但正在运行，因此其他块文件 I/O 请求。

每次成功调用**FsRtlEnterFileSystem**的后续调用必须匹配[ **FsRtlExitFileSystem**](fsrtlexitfilesystem.md)。

文件系统筛选器驱动程序可以通过调用禁用交付的正常内核 Apc **FsRtlEnterFileSystem**或[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)之前[**IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)仅当[ **FsRtlExitFileSystem** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)或[ **KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)处于相同的调度例程。 它们不应调用**FsRtlEnterFileSystem**或**KeEnterCriticalRegion**之前**IoCallDriver** ，然后调用**FsRtlExitFileSystem**或**KeLeaveCriticalRegion**中*完成例程*IRP。 驱动程序验证程序具有一个规则，以帮助捕获这种情况。

文件系统筛选器驱动程序应获取任何资源之前禁用正常内核 Apc。 文件系统筛选器驱动程序中获取以下例程使用的资源：

* [**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
* [**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)
* [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
* [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

作为一种替代方法**FsRtlEnterFileSystem**，可以使用微筛选器驱动程序[ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)， [ **FltAcquireResourceShared**](fltacquireresourceshared.md)，并[ **FltReleaseResource** ](fltreleaseresource.md)例程可正确处理 Apc 时获得和释放资源。

## <a name="requirements"></a>要求

|   |   |
| - | - |
| 目标平台 | 桌面设备 |
| Header | Ntifs.h （包括 Ntifs.h） |
| IRQL | <= APC_LEVEL |

## <a name="see-also"></a>请参阅

[**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

[**ExReleaseResource**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)

[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)
