---
title: 处理 SRB_FUNCTION_WMI
description: 处理 SRB_FUNCTION_WMI
ms.assetid: df20b9dc-1b67-4044-8abe-3cf5714076b3
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_WMI
- WMI WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 463045b6073e923293fee74d3edc22093114789d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372331"
---
# <a name="handling-srbfunctionwmi"></a>处理 SRB\_函数\_WMI


## <span id="ddk_handling_srb_function_wmi_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_WMI_KG"></span>


如果支持 HBA [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) 端口驱动程序将 WMI 将请求发送到微型端口驱动程序。 HBA 指示它通过设置的 WmiDataProvider 字段支持 WMI [**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)结构**TRUE**在其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)例程。

微型端口驱动程序的编写器准备微型端口，以便处理 WMI 请求，如下所示：

-   如果微型端口公开自定义数据的块或事件块，它应在 MOF 文件中定义此类块并将其编译为二进制资源微型端口的二进制映像中。 有关详细信息，请参阅[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)。

-   实现必需和可选*HwScsiWmiXxx*回调例程，如中所述[SCSI 微型端口驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

-   处理 SRB\_函数\_WMI。

如果微型端口驱动程序可能会挂起 WMI 请求，其**DriverEntry**例程应请求的内存分配为 SRB 扩展以便微型端口驱动程序可以维护请求整个 SRB 处理过程的上下文。

微型端口驱动程序将处理其第一个 WMI 请求之前，必须分配 SCSI\_WMILIB\_上下文结构在其设备扩展并初始化与以下结构：

-   支持的微型端口驱动程序，包括标准块中的系统定义的数据和事件块的数目*wmicore.mof*以及微型端口驱动程序的自定义块，如果有的话。

-   指向数组 SCSIWMIGUIDREGINFO 结构，一个用于支持每个块的指针。

-   到微型端口驱动程序的入口点*HwScsiWmiXxx*回调例程。 微型端口驱动程序必须至少提供入口点[ **HwScsiWmiQueryReginfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)例程和一个[ **HwScsiWmiQueryDataBlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)例程。

微型端口驱动程序无需执行任何操作即可注册其数据和事件阻止设置端口 WmiDataProvider 字段以外\_配置\_信息结构**TRUE**和实现所需*HwScsiWmiQueryReginfo*例程。 端口驱动程序负责注册与 WMI 内核组件的微型端口驱动程序的块。

在收到在其中 SRB**函数**成员设置为 SRB\_函数\_WMI，微型端口驱动程序[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程 does以下内容：

-   分配 SCSIWMI\_请求\_上下文结构从 SRB 扩展，如果该请求可能会挂起，或如果该请求可能永远不会等待，最终的堆栈。

-   检查**Srb**- **&gt;WMIFlags**以确定请求是否为该适配器或逻辑单元。

-   调用[ **ScsiPortWmiDispatchFunction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)并指出了微型端口驱动程序的 SCSI\_WMILIB\_上下文、 其设备扩展，并请求上下文和以下从 SRB 参数：

    **Srb**- **&gt;WMISubFunction**

    **Srb**- **&gt;DataPath**

    **Srb**- **&gt;DataTransferLength**

    **Srb**- **&gt;DataBuffer**

-   调用[ **ScsiPortWmiPostProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)时驱动程序已完成处理请求。 如果该驱动程序不会挂起请求，然后**ScsiPortWmiPostProcess**很可能会在回调中调用。 如果驱动程序等待请求然后**ScsiPortWmiPostProcess**应在请求完成时调用。

-   集**Srb**- **&gt;DataTransferLength**并**Srb**- **&gt;SrbStatus**返回的值为[ **ScsiPortWmiGetReturnSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize)并[ **ScsiPortWmiGetReturnStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)，分别

-   调用[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)与**RequestComplete**并再次与**NextRequest**或 (**NextLuRequest**).

有关 WMI 的详细信息，请参阅[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)。

 

 




