---
title: 使用 WMI 库注册块
description: 使用 WMI 库注册块
ms.assetid: 1f4b773d-ca24-47f5-87e8-84c98dad9267
keywords:
- WMI WDK 内核，向 WMI 注册
- 注册 WMI 数据提供程序
- 数据提供程序 WDK WMI
- 驱动程序注册 WDK WMI
- 事件阻止 WDK WMI
- 块 WDK WMI
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- 注册块
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71293d493677b459c48d7e7027301e0b66d2af43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358173"
---
# <a name="using-the-wmi-library-to-register-blocks"></a>使用 WMI 库注册块





驱动程序可以使用 WMI 库来处理[ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)并[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求如果它正在注册的块，请勿使用动态实例名称，或使用基于 PDO 或驱动程序定义的基本名称字符串的静态实例名称。 在此情况下，该驱动程序：

1.  调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)用一个指针指向驱动程序的设备对象，指向[ **WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)结构，以及指向 IRP 的

    **WMILIB\_上下文**结构表示要注册的块的数目 (**GuidCount**) 和点到一系列[ **WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmiguidreginfo)结构 (**GuidList**)，用于指定 GUID 的实例，并适用于相应的块的注册标志数。 它还定义入口点的驱动程序的必需和可选*DpWmiXxx*回调例程。

2.  当 WMI 调用驱动程序的[ *DpWmiQueryReginfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程，该驱动程序指定驱动程序的注册表路径、 其 MOF 资源名称、 适用于所有其块和信息的注册标志WMI 使用的驱动程序的数据块，它可以是名称实例指向物理设备对象的指针传递给驱动程序的[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程或基于字符串静态实例名称。

驱动程序必须进行初始化的入口点及其*DpWmiXxx*中的回调例程**WMILIB\_上下文**结构之前，调用**WmiSystemControl**，可以推迟的初始化，但**GuidCount**并**GuidList**中**WMILIB\_上下文**结构，直到 WMI 调用驱动程序*DpWmiQueryReginfo*例程。

 

 




