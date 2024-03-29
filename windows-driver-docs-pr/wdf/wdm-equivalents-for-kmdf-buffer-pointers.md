---
title: WDF 缓冲区指针的 WDM 等效项
description: WDF 缓冲区指针的 WDM 等效项
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87bc8cc393d9ad62d8e79d7ea6b056e5e6a6ae7
ms.sourcegitcommit: 41a1b058cdb6c10d3b5fe80e01f044e827687641
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69979402"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDF 缓冲区指针的 WDM 等效项


内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序使用以下方法来检索缓冲和直接 i/o 的 i/o 缓冲区。 除非另行指定, 否则这些方法同时适用于 KMDF 和 UMDF。

-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)
-   [**WdfRequestRetrieveOutputWdmMdl (仅限 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)
-   [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)
-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)
-   [**WdfRequestRetrieveInputWdmMdl (仅限 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
-   [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)

下表描述了用于\_缓冲的 irp mj\_读取、irp\_mj\_写入和 irp\_mj\_设备\_控制请求的检索方法返回的内容和直接 i/o。 对 i/o 的请求都需要特殊处理, 因为在请求用户模式进程的上下文中运行时, 驱动程序必须检索缓冲区。

## <a href="" id="read"></a>IRP\_MJ\_读取请求的缓冲区


若要检索读取请求的缓冲区, KMDF 驱动程序将调用**WdfRequestRetrieveOutput**_Xxx_方法之一。 其中每个方法返回的缓冲区会有所不同, 具体取决于驱动程序是执行缓冲还是直接 i/o。 下表描述了 WDM 术语中每个方法所返回的指针。

| Functions                                                                             | 缓冲 i/o                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp. SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (仅限 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | 生成**Irp-&gt;AssociatedIrp. SystemBuffer**的内存描述符列表 (MDL) 并返回 MDL。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取**Irp-&gt;AssociatedIrp. SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)。 |

 

## <a href="" id="write"></a>IRP\_MJ\_写入请求的缓冲区


若要检索写入请求的缓冲区, KMDF 驱动程序将调用**WdfRequestRetrieveInput**_Xxx_方法之一。 其中每个方法返回的缓冲区会有所不同, 具体取决于驱动程序是执行缓冲还是直接 i/o。 下表描述了 WDM 术语中每个方法所返回的指针。

| Functions                                                                           | 缓冲 i/o                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)             | **Irp-&gt;AssociatedIrp. SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (仅限 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) | 为**Irp-&gt;AssociatedIrp. SystemBuffer**生成 mdl 并返回 mdl。                                                                   | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)             | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取**Irp-&gt;AssociatedIrp. SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)。 |

 

## <a href="" id="device-control"></a>IRP\_MJ\_设备控制请求的缓冲区\_


若要检索设备 i/o 控制请求的缓冲区, KMDF 驱动程序需要调用**WdfRequestRetrieveInputXxx**或**WdfRequestRetrieveOutputXxx**方法。 其中每个方法返回的缓冲区会有所不同, 具体取决于驱动程序是执行[缓冲还是直接](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)i/o, 如下表所示:

| Functions                                                                             | 缓冲 i/o                                                                                                                                    | 直接 I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)               | **Irp-&gt;AssociatedIrp. SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (仅限 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)   | 为**Irp-&gt;AssociatedIrp. SystemBuffer**生成 mdl 并返回 mdl。                                                                   | 为**Irp-&gt;AssociatedIrp. SystemBuffer**生成 mdl 并返回 mdl。                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)               | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取**Irp-&gt;AssociatedIrp. SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)。 |
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp. SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (仅限 KMDF)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | 生成**Irp-&gt;AssociatedIrp. SystemBuffer**的内存描述符列表 (MDL) 并返回 MDL。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取**Irp-&gt;AssociatedIrp. SystemBuffer**。 | 返回 WDFMEMORY 对象。 对此对象调用[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)以获取[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;MdlAddress**)。 |

 

 

 





