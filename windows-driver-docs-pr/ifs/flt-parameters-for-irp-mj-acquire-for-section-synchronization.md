---
title: FLT_PARAMETERS for IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION union
description: 当操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段为 IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 时, 使用以下联合组件。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- FLT_PARAMETERS for IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION union 可安装的文件系统驱动程序
- FLT_PARAMETERS 可安装的可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7a379a78263a001816c4e4ad28815685faec231e
ms.sourcegitcommit: b9a65cb309bea3d35048968bdc708e0067276e68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68313215"
---
# <a name="fltparameters-for-irpmjacquireforsectionsynchronization-union"></a>FLT_PARAMETERS for IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION union

当操作的[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MAJORFUNCTION**字段为 IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 时, 使用以下联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    FS_FILTER_SECTION_SYNC_TYPE SyncType;
    ULONG POINTER_ALIGNMENT     PageProtection;
    PFS_FILTER_SECTION_SYNC_OUTPUT OutputInformation;
  } AcquireForSectionSynchronization;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>Members

### <a name="synctype"></a>SyncType  

节请求的同步的类型。 如果正在创建一个节, 此参数将设置为**SyncTypeCreateSection** ;否则, 将其设置为**SyncTypeOther**。

### <a name="pageprotection"></a>PageProtection

节请求的页保护的类型。 如果**SyncType**为 SyncTypeOther, 则必须为零。 否则, 此参数必须为定义的[内存保护常量值](https://docs.microsoft.com/windows/win32/memory/memory-protection-constants)之一。

### <a name="outputinformation"></a>OutputInformation

[**FS_FILTER_SECTION_SYNC_OUTPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fs_filter_section_sync_output)结构, 指定描述正在创建的节的属性的信息。

## <a name="remarks"></a>备注

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作的[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据 ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 表示的**AcquireForSectionSynchronization**操作的参数构造. 它包含在 FLT_IO_PARAMETER_BLOCK 结构中。

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 是一个文件系统 (FSFilter) 回调操作。

如果**SyncType**成员的枚举值设置为**SyncTypeOther**, 则文件系统筛选器或旧筛选器驱动程序不能使此操作失败。 如果将**SyncType**设置为**SyncTypeCreateSection**, 则在没有足够的内存来创建分区时, 将允许文件系统微筛选器或旧版筛选器驱动程序失败并出现 STATUS_INSUFFICIENT_RESOURCES 错误。

有关 FSFilter 回调操作的详细信息, 请参阅[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

## <a name="requirements"></a>要求

| | |
| ------- | ------- |
| Version | 在 windows XP 和更高版本的 Windows 操作系统中可用。 |
| Header    | Fltkernel (包括 Fltkernel) |

## <a name="see-also"></a>请参阅

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)
