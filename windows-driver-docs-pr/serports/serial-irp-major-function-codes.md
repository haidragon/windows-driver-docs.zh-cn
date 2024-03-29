---
title: 串行 IRP 主要函数代码
description: 文档串行 IRP 主要函数代码
keywords:
- 串行设备 WDK
- 串行驱动程序 WDK
- 串行 IRP 代码
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc55bec9961072ea7d8595ccbcda269a563124c1
ms.sourcegitcommit: da49bbd01df836def12aae732f9a0e85c15a8a9f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2019
ms.locfileid: "67395213"
---
# <a name="serial-irp-major-function-codes"></a>串行 IRP 主要函数代码
本主题介绍串行 IRP 主要函数代码。

标头：Wdm.h 中 （包括 wdm.h 中或 Ntddk.h）

## <a name="irpmjcreate"></a>IRP_MJ_CREATE

[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求打开串行设备。

### <a name="when-sent"></a>发送时

它可以访问该端口或连接到该端口的设备之前，客户端必须打开串行设备。

### <a name="input-parameters"></a>输入参数

无。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

**信息**字段设置为零。

**状态**字段设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|已成功打开串行设备。|
|STATUS_ACCESS_DENIED|设备已打开。|
|STATUS_DELETE_PENDING|删除设备正在序列。|
|STATUS_INSUFFICIENT_RESOURCES|设备不处于插已启动状态，或者驱动程序无法分配内部数据结构。|
|STATUS_NOT_A_DIRECTORY|不能作为目录打开串行设备。|
|STATUS_PENDING|串行排入队列供以后处理的请求。|
|STATUS_SHARED_IRQ_BUSY|分配给设备的中断正由另一个打开的设备使用。|

### <a name="operation"></a>操作

必须打开串行设备，然后才能使用。 串行设备是独占的设备;只有一个文件可以是开放的端口上在任何给定时间。

## <a name="irpmjdevicecontrol"></a>IRP_MJ_DEVICE_CONTROL

IRP_MJ_DEVICE_CONTROL 请求的操作串行端口。

### <a name="when-sent"></a>发送时

客户端使用到的设备控制请求：

* 获取有关该端口的信息
* 获取和设置寄存器
* 获取和设置运行模式

有关支持序列的设备控制请求的说明，请参阅[ntddser.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ntddser/)标头。

### <a name="input-parameters"></a>输入的参数

特定请求

### <a name="output-parameters"></a>输出参数

特定请求

### <a name="io-status-block"></a>I/O 状态块

特定请求

### <a name="operation"></a>操作

特定请求

## <a name="irpmjflushbuffers"></a>IRP_MJ_FLUSH_BUFFERS

[IRP_MJ_FLUSH_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)请求刷新的串行设备内部写入缓冲区。

### <a name="when-sent"></a>发送时

客户端使用刷新请求以确定何时序列已完成所有写入请求发送之前刷新请求的客户端。

### <a name="input-parameters"></a>输入的参数

无。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

**信息**成员设置为零。

**状态**成员设置为以下状态的值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端取消了请求。 如果设备出错且序列配置为取消请求，如果设备错误时，序列也将取消请求。|
|STATUS_DELETE_PENDING|在过程中删除设备驱动程序。|
|STATUS_PENDING|串行排入队列供以后处理的请求。|

### <a name="operation"></a>操作

串行队列并开始处理写入和刷新在其中接收请求的顺序中的请求。 序列完成刷新请求之后它将调用, **IoCompleteRequest**进行的所有写入它之前刷新请求接收的请求。 *但是，完成刷新请求并不表示设备堆栈中其他驱动程序的所有先前启动的写入请求都已完成。* 例如，筛选器驱动程序可能仍在处理写入请求。 客户端必须检查客户端尝试释放或重复使用的写入请求的 IRP 之前由设备堆栈中的所有驱动程序完成写入请求。

## <a name="irpmjinternaldevicecontrol"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求串行设备上设置内部操作模式。

### <a name="when-sent"></a>发送时

客户端使用到的内部设备控制请求：

* 获取和重置基本设置
* 控制等待/唤醒操作

内部设备控制请求的说明，请参阅[ntddser.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/)标头。

### <a name="input-parameters"></a>输入的参数

特定请求

### <a name="output-parameters"></a>输出参数

特定请求

### <a name="io-status-block"></a>I/O 状态块

特定请求

### <a name="operation"></a>操作

特定请求

## <a name="irpmjpnp"></a>IRP_MJ_PNP

[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)请求支持插。

### <a name="when-sent"></a>发送时

PnP 管理器将 IRP_MJ_PNP 请求发送到查询设备并启动、 停止和删除设备。

### <a name="input-parameters"></a>输入的参数

特定请求

### <a name="output-parameters"></a>输出参数

特定请求

### <a name="io-status-block"></a>I/O 状态块

特定请求

### <a name="operation"></a>操作

序列支持以下插请求：

* [IRP_MN_CANCEL_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)
* [IRP_MN_CANCEL_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)
* [IRP_MN_FILTER_RESOURCE_REQUIREMENTS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)
* [IRP_MN_QUERY_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)
* [IRP_MN_QUERY_DEVICE_RELATIONS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)
* [IRP_MN_QUERY_ID](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)
* [IRP_MN_QUERY_PNP_DEVICE_STATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)
* [IRP_MN_QUERY_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)
* [IRP_MN_QUERY_RESOURCE_REQUIREMENTS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)
* [IRP_MN_QUERY_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)
* [IRP_MN_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)
* [IRP_MN_START_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)
* [IRP_MN_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)
* [IRP_MN_SURPRISE_REMOVAL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

序列将向设备堆栈下的所有其他插请求发送无需进一步处理。

序列将执行以下序列的特定处理的插请求：

**IRP_MN_QUERY_ID** （键入 BusQueryHardwardIDs）

如果串行设备多端口的 ISA 卡上，序列将宽字符字符串追加"* PNP0502"硬件 Id 的字符串。

**IRP_MN_FILTER_RESOURCE_REQUIREMENTS**

在多端口 ISA 卡上的串行设备共享同一个中断状态寄存器和相同的中断。

有关泛型的插请求操作的说明，请参阅[即插即用和播放次要 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)。

## <a name="irpmjpower"></a>IRP_MJ_POWER

[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)控制电源管理的请求。

### <a name="when-sent"></a>发送时

电源管理器使用电源请求来查询和设置的电源状态。

###  <a name="input-parameters"></a>输入的参数

特定请求

### <a name="output-parameters"></a>输出参数

特定请求

### <a name="io-status-block"></a>I/O 状态块

特定请求

### <a name="operation"></a>操作

序列支持以下 power 请求：

* [IRP_MN_QUERY_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)
* [IRP_MN_SET_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

序列所有其他 power 将请求发送关闭设备堆栈的较低级驱动程序要完成。

序列是为功能驱动程序或较低级别筛选器驱动程序使用序列的串行设备堆栈的默认电源策略所有者。

有关泛型这些请求的操作的详细信息，请参阅[规则处理 Power Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)。

## <a name="irpmjqueryinformation"></a>IRP_MJ_QUERY_INFORMATION

[IRP_MJ_QUERY_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)请求查询是串行设备的最终文件信息。 

### <a name="when-sent"></a>发送时

客户端使用的查询信息请求以获取标准信息和有关串行设备上打开的文件位置信息。

### <a name="input-parameters"></a>输入的参数

**Parameters.QueryFile.FileInformationClass**设置为**FileStandardInformation**或**FilePositionInformation**。

### <a name="output-parameters"></a>输出参数

|参数|描述|
|----|----|
|**FileStandardInformation**|**AssociatedIrp.SystemBuffer**成员指向客户端分配 FILE_STANDARD_INFORMATION 结构序列使用标准的信息输出。|
|**FilePositionInformation**|**AssociatedIrp.SystemBuffer**成员指向客户端分配 FILE_POSITION_INFORMATION 结构使用的串行输出位置信息。|

### <a name="io-status-block"></a>I/O 状态块

如果请求成功，**信息**成员设置为零。

**状态**成员设置为以下状态的值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端取消了请求。 如果设备出错且序列配置为取消请求，如果设备错误时，序列也将取消请求。|
|STATUS_DELETE_PENDING|删除设备正在序列。|
|STATUS_INVALID_PARAMETER|不支持所需的信息。|
|STATUS_PENDING|串行排入队列供以后处理的请求。|

### <a name="operation"></a>操作

序列支持类型的请求**FileStandardInformation**并**FilePositionInformation**。

标准文件信息始终设置为零或**FALSE**根据。 位置信息始终设置为零。

## <a name="irpmjread"></a>IRP_MJ_READ

一个[IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求将数据从串行设备传输到客户端。

### <a name="when-sent"></a>发送时

客户端使用的读取的请求时它会读取串行设备上的数据。

### <a name="input-parameters"></a>输入的参数

**Parameters.Read.Length**成员设置为的字节数将传输到客户端的读取缓冲区。

### <a name="output-parameters"></a>输出参数

**AssociatedIrp.SystemBuffer**成员指向串行设备的串行复制数据读取到的客户端分配的读取缓冲区。

### <a name="io-status-block"></a>I/O 状态块

**信息**成员设置为传输到客户端的读取缓冲区的字节数。

**状态**成员设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端取消了请求。 如果设备出错且序列配置为取消请求，如果设备错误时，序列也将取消请求。|
|STATUS_DELETE_PENDING|删除设备正在序列。|
|STATUS_PENDING|串行排入队列供以后处理的请求。|
|STATUS_TIMEOUT|若要完成该请求的时间超过了总超时值或间隔超时值。|

### <a name="operation"></a>操作

客户端可以使用的超时事件终止的读取的请求。 但是，请注意，当打开串行设备时，设备的超时设置是不确定。 内核模式下客户端可以使用[IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)将超时参数设置为零 （无超时使用事件）。 用户模式和内核模式下客户端可以使用[IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)请求设置超时参数。 

有关详细信息大约读取和写入超时，请参阅[设置读取和写入串行设备超时](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))。

## <a name="irpmjsetinformation"></a>IRP_MJ_SET_INFORMATION

[IRP_MJ_SET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)请求设置串行设备有关的文件尾信息。

### <a name="when-sent"></a>发送时

客户端使用 set 信息请求更改的串行设备上打开的文件当前的文件结束位置。

### <a name="input-parameters"></a>输入的参数
**Parameters.SetFile.FileInformationClass**成员设置为**FileEndOfFileInformation**或**FileAllocationInformation**。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

如果请求成功，**信息**成员设置为零。

**状态**成员设置为以下状态的值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端取消了请求。 如果设备出错且序列配置为取消请求，如果设备错误时，序列也将取消请求。|
|STATUS_DELETE_PENDING|删除设备正在序列。|
|STATUS_INVALID_PARAMETER|不支持指定的文件尾信息。|
|STATUS_PENDING|串行排入队列供以后处理的请求。|

### <a name="operation"></a>操作

序列支持类型的请求**FileEndOfFileInformation**并**FileAllocationInformation**。 但是，序列不实际设置文件的信息。 文件结尾位置始终设置为零。

## <a name="irpmjsystemcontrol"></a>IRP_MJ_SYSTEM_CONTROL

[IRP_MJ_SYSTEM_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)请求支持 WMI 请求。

### <a name="when-sent"></a>发送时

WMI 内核模式组件可以发送 IRP_MJ_SYSTEM_CONTROL 请求序列将注册为串行设备的 WMI 提供程序之后的任何时间。 通常 WMI Irp 会在用户模式下的数据使用者已请求 WMI 数据。

### <a name="input-parameters"></a>输入的参数

特定请求

### <a name="output-parameters"></a>输出参数

特定请求

### <a name="io-status-block"></a>I/O 状态块

WMI 请求序列将状态字段设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_BUFFER_TOO_SMALL|大小 （字节） 的输出缓冲区小于所请求的信息所需大小。|
|STATUS_INSUFFICIENT_RESOURCES|没有足够的系统资源来节省的串行端口名称。|
|STATUS_INVALID_DEVICE_REQUEST|请求无效。|
|STATUS_WMI_GUID_NOT_FOUND|不支持 WMI GUID。|

### <a name="operation"></a>操作

使用串行[WmiSystemControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI 系统控制请求。 序列将注册以下类型的 WMI 库回调例程，其中**WmiSystemControl**调用来处理 WMI 请求发送到设备：

* [DpWmiQueryReginfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)
* [DpWmiQueryDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)
* [DpWmiSetDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_datablock_callback)
* [DpWmiSetDataItem](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)

序列不支持任何其他系统控制请求。 对于非 WMI 请求，序列将跳过当前的堆栈位置，并将发送关闭设备堆栈请求。

下表中所述 WMI GUID 串行寄存器。

串行 WMI GUID 关联数据结构 

| SERIAL_PORT_WMI_NAME_GUID | USHORT 跟 WCSTR |
| ------------------------- | -------------------------- |
| SERIAL_PORT_WMI_COMM_GUID | SERIAL_WMI_COMM_DATA |
| SERIAL_PORT_WMI_HW_GUID | SERIAL_WMI_HW_DATA |
| SERIAL_PORT_WMI_PERF_GUID | SERIAL_WMI_PERF_DATA |
| SERIAL_PORT_WMI_PROPERTIES_GUID | WMI_SERIAL_PORT_PROPERTIES |

串行设备的 WMI 名称是项值的值**PortName**设备插注册表项下。

## <a name="irpmjwrite"></a>IRP_MJ_WRITE

[IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)请求将数据从客户端传输到串行设备。

### <a name="when-sent"></a>发送时

客户端使用的写入请求时它将数据写入串行设备。

### <a name="input-parameters"></a>输入的参数

**Parameters.Write.Length**成员设置为的字节数，将从客户端分配写入缓冲区复制到串行设备。

**AssociatedIrp.SystemBuffer**成员指向客户端分配写入缓冲区从串行复制数据到串行设备。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

*信息*成员设置为实际复制到串行设备客户端的写入缓冲区的字节数。

*状态*成员设置为以下值之一：

|状态值|描述|
|----|----|
|STATUS_SUCCESS|请求已成功完成。|
|STATUS_CANCELLED|客户端取消了请求。 如果设备出错且序列配置为取消请求，如果设备错误时，序列也将取消请求。|
|STATUS_DELETE_PENDING|删除设备正在序列。|
|STATUS_PENDING|串行排入队列供以后处理的请求。|
|STATUS_TIMEOUT|超出了允许的写入请求的总时间。|

### <a name="operation"></a>操作

客户端可以使用的超时事件终止写入请求。 但是，请注意，当打开串行设备时，在设备上设置的超时事件是未定义。 内核模式下客户端可以使用[IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)若要将超时参数设置为零 （无超时使用事件） 和一个[IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)请求设置超时值参数。 有关详细信息大约读取和写入超时，请参阅[设置读取和写入串行设备超时](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))。

## <a name="related-topics"></a>相关主题

[Plug and Play 次要 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)

[处理 Power Irp 规则](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)

[串行控制器驱动程序设计指南](https://docs.microsoft.com/en-us/windows-hardware/drivers/serports/)
