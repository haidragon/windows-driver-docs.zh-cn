---
title: 框架对象摘要
description: 框架对象摘要
ms.assetid: 799284a5-91c0-47b0-8f20-75a5f8e2284d
keywords:
- 列出的 framework 对象 WDK KMDF
- framework 对象 WDK KMDF 摘要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f43075b3090469d023b942d1b9d36fd51d5935
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368085"
---
# <a name="summary-of-framework-objects"></a>框架对象摘要


下表列出了所有 framework 对象，并提供了有关每个对象的一些基本信息。 模式列指示是否可以使用该对象在 KMDF 和 UMDF 驱动程序或仅 KMDF。

回调和方法的框架都适用的列表，请参阅[WDF 回调摘要和方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)。

|名称|句柄|用途|默认父级|驱动程序可以重写默认父？|模式|参考|
|--- |--- |--- |--- |--- |--- |--- |
|子列表对象|WDFCHILDLIST|表示子设备连接到父设备的列表。|设备对象|否|KM|[WDF 子列表对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/)|
|集合对象|WDFCOLLECTION|表示对象集合。|驱动程序对象|是|KM/UM|[WDF 集合对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/)|
|常见的缓冲区对象|WDFCOMMONBUFFER|表示一个通用的缓冲区。|DMA 启用程序对象|否|KM|[WDF 常见缓冲区对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/)|
|设备对象|WDFDEVICE|表示一个设备。|驱动程序对象|否|KM/UM|[WDF 设备对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/)|
|DMA 启用程序对象|WDFDMAENABLER|使驱动程序即可使用框架的 DMA 功能。|设备对象|是|KM|[WDF DMA 对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/)|
|DMA 事务对象|WDFDMATRANSACTION|表示 DMA 事务。|DMA 启用程序对象|否|KM|[WDF DMA 对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/)|
|DPC 对象|WDFDPC|表示延迟的过程调用。|无|是|KM|[WDF DPC 对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/)|
|驱动程序对象|WDFDRIVER|表示一个驱动程序。|无|否|KM/UM|[WDF 驱动程序对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/)|
|文件对象|WDFFILEOBJECT|表示一个文件。|设备对象|否|KM/UM|[WDF 文件对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/)|
|常规对象|WDFOBJECT|表示常规对象。|驱动程序对象|是|KM/UM|[WDF 常规对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/)|
|中断对象|WDFINTERRUPT|表示硬件中断资源。|设备对象|是|KM/UM|[WDF 中断对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/)|
|I/O 目标对象|WDFIOTARGET|表示另一个驱动程序将 I/O 请求发送到的驱动程序。|设备对象|是|KM/UM|[WDF I/O 目标对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/)|
|后备链列表对象|WDFLOOKASIDE|表示后备链列表。|驱动程序对象|是|KM|[WDF 内存对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/)|
|内存对象|WDFMEMORY|表示一个内存缓冲区。|驱动程序对象|是|KM/UM|[WDF 内存对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/)|
|队列对象|WDFQUEUE|表示接收的 I/O 请求的 I/O 队列。|设备对象|是|KM/UM|[WDF 队列对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/)|
|注册表项对象|WDFKEY|表示注册表项。|驱动程序对象|是|KM/UM|[WDF 注册表项对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/)|
|请求对象|WDFREQUEST|表示 I/O 请求。|无，如果创建的框架。 驱动程序对象，如果创建的驱动程序。|是，如果创建的驱动程序。|KM/UM|[WDF 请求对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/)|
|资源列表对象|WDFCMRESLIST|表示资源的列表。|驱动程序对象|否|KM/UM|[WDF 资源对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)|
|资源范围列表对象|WDFIORESLIST|表示逻辑配置。|资源要求列表对象|否|KM|[WDF 资源对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)|
|资源要求列表对象|WDFIORESREQLIST|表示资源的要求列表。|驱动程序对象|否|KM|[WDF 资源对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)|
|旋转锁对象|WDFSPINLOCK|表示旋转锁。|驱动程序对象|是|KM/UM|[WDF 同步方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/)|
|字符串对象|WDFSTRING|表示一个 Unicode 字符串。|驱动程序对象|是|KM/UM|[WDF 字符串对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfstring/)|
|计时器对象|WDFTIMER|表示一个计时器。|无|是|KM/UM|[WDF 计时器对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/)|
|USB 设备对象|WDFUSBDEVICE|表示连接到 USB 的设备。|设备对象|否|KM/UM|[WDF USB 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)|
|USB 接口对象|WDFUSBINTERFACE|表示 USB 设备接口。|USB 设备对象|否|KM/UM|[WDF USB 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)|
|USB 管道对象|WDFUSBPIPE|表示一个 USB 设备管道。|USB 接口对象|否|KM/UM|[WDF USB 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)|
|等待锁对象|WDFWAITLOCK|表示等待锁。|驱动程序对象|是|KM/UM|[WDF 同步方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/)|
|WMI 实例对象|WDFWMIINSTANCE|表示一个 WMI 数据块的一个实例。|WMI 提供程序对象|否|KM|[WDF WMI 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/)|
|WMI 提供程序对象|WDFWMIPROVIDER|表示 WMI 数据块。|设备对象|否|KM|[WDF WMI 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/)|
|工作项对象|WDFWORKITEM|表示工作项。|无|是|KM/UM|[WDF 工作项对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/)|


 

 

 





