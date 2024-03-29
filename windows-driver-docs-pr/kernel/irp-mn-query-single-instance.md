---
title: IRP_MN_QUERY_SINGLE_INSTANCE
description: 支持 WMI 的所有驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 104b6b3e-aa5d-437f-8236-02e4abb1ba46
keywords:
- IRP_MN_QUERY_SINGLE_INSTANCE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 18c8d4b5ba79292961eeb716218f258378457c18
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370851"
---
# <a name="irpmnquerysingleinstance"></a>IRP\_MN\_查询\_单个\_实例


支持 WMI 的所有驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)处理**IRP\_MN\_查询\_单一\_实例**请求 WMI 又会调用该驱动程序[ *DpWmiQueryDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将此 IRP 发送到给定的数据块的单个实例的查询。

WMI 发送**IRP\_MN\_查询\_单个\_实例**在发送前[ **IRP\_MN\_EXECUTE\_方法**](irp-mn-execute-method.md)。 如果驱动程序支持**IRP\_MN\_EXECUTE\_方法**，它必须具有**IRP\_MN\_查询\_单一\_实例**正在执行的方法在同一个数据块的处理程序。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**指向标识查询的数据块的 GUID。

**Parameters.WMI.BufferSize**指示在非分页缓冲区的最大大小**Parameters.WMI.Buffer**，它指向[ **WNODE\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)结构，它标识查询的实例。

## <a name="output-parameters"></a>输出参数


如果该驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 会填写[ **WNODE\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)具有提供的驱动程序的数据结构[ *DpWmiQueryDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)例程。

否则，该驱动程序会填写**WNODE\_单个\_实例**结构，在**Parameters.WMI.Buffer** ，如下所示：

-   更新**WnodeHeader.BufferSize**与大小 （字节） 输出**WNODE\_单个\_实例**结构，包括实例数据。 此值应包括实例名称 （填充，以便该实例数据将开始在四字边界上） 的长度，即使静态注册正在查询的类实例名称和驱动程序编写器未显式提供名称时维护服务此 IRP。

-   集**SizeDataBlock**到大小 （字节） 的实例数据。 如果静态实例名称正在使用，此值应不包括实例名称的大小。

-   将实例数据写入**Parameters.WMI.Buffer**开始**DataBlockOffset**。 该驱动程序不得更改的输入的值**DataBlockOffset**。

如果在缓冲区**Parameters.WMI.Buffer**太小，无法接收的所有数据中的所需的大小，以驱动程序填充[ **WNODE\_过\_小**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_too_small)结构，在**Parameters.WMI.Buffer**。 如果缓冲区小于**sizeof**(**WNODE\_过\_小**)，该驱动程序将 IRP 失败并返回状态\_缓冲区\_过\_小。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_缓冲区\_过\_小

状态\_WMI\_GUID\_不\_找到

状态\_WMI\_实例\_不\_找到

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**中输入的值**WnodeHeader.BufferSize**。 此值包括静态实例名称的长度。

<a name="operation"></a>操作
---------

驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)， **WmiSystemControl**调用的驱动程序[ *DpWmiQueryDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)例程。

如果驱动程序处理**IRP\_MN\_查询\_单个\_实例**请求本身，才应该这样做**Parameters.WMI.ProviderId**指向与该驱动程序对其调用中传递的指针相同的设备对象[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须将请求转发到设备堆栈中的下一个较低驱动程序。

之前处理请求，该驱动程序必须确定是否**Parameters.WMI.DataPath**指向该驱动程序支持的 GUID。 如果不是，该驱动程序必须失败 IRP，并返回状态\_WMI\_GUID\_不\_找到。

该驱动程序负责验证所有输入的值。 具体而言，如果处理 IRP 请求本身，则该驱动程序，就必须执行以下操作：

-   对于静态名称，请验证**InstanceIndex**的成员[ **WNODE\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)结构位于范围内支持的数据块的驱动程序的实例索引。

-   有关动态名称，验证实例名称字符串标识驱动程序支持的数据块实例。

-   确认**Parameters.WMI.BufferSize**指定足够大，以接收该驱动程序将返回的所有数据的缓冲区。

如果该驱动程序支持的数据块，它会检查输入[ **WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)在**Parameters.WMI.Buffer**实例名称，按如下所示：

-   如果 WNODE\_标志\_静态\_实例\_中设置的名称**WnodeHeader.Flags**，则驱动程序使用**InstanceIndex**作为中的索引为该块的静态实例名称的驱动程序的列表。 WMI 从注册块时，驱动程序提供的注册数据中获取索引。

-   如果 WNODE\_标志\_静态\_实例\_名称是明确**WnodeHeader.Flags**，则驱动程序使用的偏移量**OffsetInstanceName**到输入中找到的实例名称字符串**WNODE\_单个\_实例**。 **OffsetInstanceName**的偏移量，以字节为单位，从结构开始处到 USHORT，这是实例名称字符串长度以字节为单位 （不是字符），包括终止 null （如果存在） 后跟实例名称字符串Unicode。

如果该驱动程序找不到指定的实例，它必须失败 IRP，并返回状态\_WMI\_实例\_不\_找到。 对于使用动态实例名称的实例，此状态指示驱动程序不支持该实例。 因此，WMI 可以继续查询其他数据提供程序，并返回相应的错误数据使用者，如果另一个提供程序的实例，但由于某种原因无法处理该请求。

如果驱动程序找到实例，并且可以处理该请求，它填充**WNODE\_单个\_实例**结构，在**Parameters.WMI.Buffer**使用的实例数据。

如果该实例有效，但该驱动程序无法处理请求，它可以返回任何相应的错误状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




