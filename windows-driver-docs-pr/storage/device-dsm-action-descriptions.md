---
title: DEVICE_DSM_ACTION 说明
description: 此页介绍了可用于对设备的数据集属性执行数据集管理 (DSM) 操作的 DEVICE_DSM_ACTION 常量。
ms.assetid: cc64c7ad-7d1c-45c7-b236-a43e57086f8d
keywords: 存储数据设置管理操作, 数据设置管理操作, DSM 操作
ms.localizationpriority: medium
ms.date: 08/23/2019
ms.openlocfilehash: 2f53d1c7e7bb5bd6b3aecaa1971658178533c654
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70076023"
---
# <a name="device_dsm_action-descriptions"></a>DEVICE_DSM_ACTION 说明

此页介绍了可用于对设备的数据集执行数据集管理 (DSM) 操作的 DEVICE_DSM_ACTION 常量。 这些常量在*ntddstor*中定义。 标识为非破坏性的操作将不会更改任何数据。 有关如何处理 DSM 操作的信息, 请参阅[数据集管理概述](data-set-management-overview.md)。

| DEVICE_DSM_ACTION 常量 | 描述 |
| -------------------------- | ----------- |
| **DeviceDsmAction_None** | 仅用于结构初始化目的。 |
| **DeviceDsmAction_Trim** | 驱动程序将执行剪裁操作。 |
| **DeviceDsmAction_Notification** | 无损. 驱动程序将执行通知操作。 对于此操作, 紧跟在[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构后面的参数块的格式为[DEVICE_DSM_NOTIFICATION_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_dsm_notification_parameters)结构。 在 Windows 7 及更高版本中受支持。 |
| **DeviceDsmAction_OffloadRead** | 无损. 驱动程序执行卸载读取操作。 对于此操作, 紧跟在[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构后面的参数块的格式为[DEVICE_DSM_OFFLOAD_READ_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_dsm_offload_read_parameters)结构。 输出包含[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)结构, 后跟[STORAGE_OFFLOAD_READ_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_offload_read_output)结构。 在 Windows 8 及更高版本中受支持。 |
| **DeviceDsmAction_OffloadWrite** | 驱动程序将执行卸载写入操作。 对于此操作, 紧跟在[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构后面的参数块的格式为[DEVICE_DSM_OFFLOAD_WRITE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_dsm_offload_write_parameters)结构。 输出包含[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)结构, 后跟[STORAGE_OFFLOAD_WRITE_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_offload_write_output)结构。 在 Windows 8 及更高版本中受支持。 |
| **DeviceDsmAction_Allocation** | 无损. 驱动程序将执行逻辑块预配操作。 逻辑块范围是在单个[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构中指定的。 在 Windows 8 及更高版本中受支持。 |
| **DeviceDsmAction_Repair** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_Scrub** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_DrtQuery** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_DrtClear** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_DrtDisable** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_TieringQuery** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_Map** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_RegenerateParity** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_NvCache_Change_Priority** | 无损. 驱动程序将更改指定范围的逻辑块的缓存优先级。 新的目标优先级设置为[DEVICE_DSM_NVCACHE_CHANGE_PRIORITY_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_dsm_nvcache_change_priority_parameters)结构中, 该结构位于紧跟[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构的参数块中。 要更改优先级的逻辑块范围在一个或多个[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构中给定。 在 Windows 8.1 及更高版本中受支持。 |
| **DeviceDsmAction_NvCache_Evict** | 无损. 驱动程序将从缓存介质中逐出数据。 若要逐出所有数据, 请在[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)的**Flags**成员中设置 DEVICE_DSM_FLAG_ENTIRE_DATA_SET_RANGE 标志, 并且不要包含任何[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构。 要逐出的特定逻辑块范围在一个或多个[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构中提供。 **DeviceDsmAction_NvCache_Evict**操作以同步方式执行。 在逐出操作成功或失败之前, 不会对其他任何操作提供服务。 为了限制其对使用设备的应用程序的影响, 发出的每个**DeviceDsmAction_NvCache_Evict**操作应该包含相对较小的数据范围。 它们不应超过 10 MB, 理想情况下小于 2 MB。 这将最大限度地减少用户级应用程序在访问设备上的数据时遇到明显延迟的可能性。 在 Windows 8.1 及更高版本中受支持。 |
| **DeviceDsmAction_TopologyIdQuery** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_GetPhysicalAddresses** | 无损. 驱动程序将返回与一个或多个逻辑块范围对应的物理地址范围。 此操作仅在永久性内存磁盘上受支持。 逻辑块范围指定为紧随 DEVICE_DSM_INPUT 结构的一系列[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构。 输出包含[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)结构, 后跟填充, 然后是在输出块中请求的物理地址范围的[DEVICE_DSM_PHYSICAL_ADDRESSES_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_dsm_physical_addresses_output)结构。 每个物理地址范围都在[DEVICE_STORAGE_ADDRESS_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_storag_address_range)结构中返回。 如果输出缓冲区不够大, 无法保存所有数据, 则 DSM 返回 STATUS_BUFFER_OVERFLOW, DEVICE_DSM_PHYSICAL_ADDRESSES_OUTPUT 结构的**TotalNumberOfRanges**字段包含 DEVICE_STORAGE_ADDRESS_RANGE 的数目满足请求所需的元素。 包含内存错误的任何物理地址范围都将 DEVICE_DSM_PHYSICAL_ADDRESS_HAS_MEMORY_ERROR 作为其地址。 应用程序可以通过跟踪每个返回的物理地址范围的长度, 将返回的物理地址范围映射到输入逻辑块范围。 请注意, 单个逻辑块范围可以对应于许多物理地址范围。 如果 DEVICE_DSM_FLAG_PHYSICAL_ADDRESSES_OMIT_TOTAL_RANGES 是在[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构的 "**标志**" 字段中设置的, 则驱动程序将不会计算**TotalNumberOfRanges**。 这是不需要知道范围总数的调用方的性能优化。 |
| **DeviceDsmAction_ScopeRegen** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_ReportZones** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_OpenZone** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_FinishZone** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_CloseZone** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_ResetWritePointer** | 仅供内部使用。 |
| **DeviceDsmAction_GetRangeErrorInfo** | 无损. 驱动程序将返回有关一个或多个逻辑块范围是否包含任何媒体错误的信息。 这仅在永久性内存磁盘上受支持。 逻辑块范围指定为紧随[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构的一系列[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构。 输出由[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)结构组成, 后跟填充和[DEVICE_DSM_RANGE_ERROR_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_dsm_range_error_output)) 结构, 其中包含一个[DEVICE_STORAGE_RANGE_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_storage_range_attributes)数组。 如果输出缓冲区不够大, 无法保存所有数据, 则 DSM 返回 STATUS_BUFFER_OVERFLOW, 而 DEVICE_DSM_RANGE_ERROR_OUTPUT 结构的**TotalNumberOfRanges**字段包含 DEVICE_STORAGE_RANGE_ATTRIBUTES 元素数需要满足请求。 每个 DEVICE_STORAGE_RANGE_ATTRIBUTES 结构都包含一个**IsRangeBad**字段。 当逻辑块范围包含媒体错误时, 驱动程序将该字段设置为1。 如果任何所请求的范围中没有介质错误, 驱动程序将在 DEVICE_DSM_RANGE_ERROR_OUTPUT 的 "标志" 字段中设置 DEVICE_STORAGE_NO_ERRORS。 排序 DEVICE_STORAGE_RANGE_ATTRIBUTES 数组的元素, 使其顺序与输入范围的顺序相对应。 例如, 如果第一个输入范围分为3个输出范围, 则这些范围将是数组中的前3个范围。 调用方可以通过跟踪输出范围的长度来了解与输入范围对应的输出范围。 |
| **DeviceDsmAction_WriteZeroes** | 仅供内部使用。 |
| **DeviceDsmAction_LostQuery** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_GetFreeSpace** | 无损. 仅供内部使用。 |
| **DeviceDsmAction_ConversionQuery** | 无损. 仅供内部使用。 |
