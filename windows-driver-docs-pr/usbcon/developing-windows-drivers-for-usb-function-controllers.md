---
Description: 开发的 USB 函数控制器的 Windows 驱动程序的概述
title: 开发的 USB 函数控制器的 Windows 驱动程序的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f58909f940a6f69a77ec98301db9330f426f947
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716993"
---
# <a name="overview-of-developing-windows-drivers-for-usb-function-controllers"></a>开发的 USB 函数控制器的 Windows 驱动程序的概述


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>用途</strong></p>
<p>本部分介绍用于开发与 Microsoft 提供的 USB 函数控制器扩展 (UFX) 进行通信的通用串行总线 (USB) 函数控制器驱动程序的 Windows 操作系统系统中的支持。</p>
<p><strong>开发工具和 Microsoft 提供的二进制文件</strong></p>
<p>Windows Driver Kit (WDK) 包含所需的驱动程序开发，例如标头、 库、 工具和示例的资源。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p>
<p>若要编写函数控制器驱动程序，需要：</p>
<ul>
<li>作为 FDO 加载 UFX (Ufx01000.sys)。 此驱动程序包含在 Windows 中。</li>
<li>链接到存根 （stub） 库 (Ufx01000.lib)。 存根 （stub） 库是在 WDK 中。 库将转换函数控制器驱动程序所做的调用，并将其传递到 UFX。</li>
<li>包括 Ufxclient.h WDK 中提供。</li>
</ul>
<p>若要从用户模式下发送请求，需要：</p>
<ul>
<li>GenericUSBFn.sys 作为 USB 函数类驱动程序加载。 此驱动程序包含在 Windows 中。</li>
<li>包括 Genericusbfnioctl.h WDK 中提供。</li>
</ul>
<p>若要从 USB 类驱动程序发送请求，需要：</p>
<ul>
<li>作为 FDO 加载 UFX (Ufx01000.sys)。 此驱动程序包含在 Windows 中。</li>
<li>包括 Usbfnioctl.h WDK 中提供。</li>
</ul>
若要编写处理通过专有充电器充电的筛选器驱动程序，需要：
<ul>
<li>UfxChipidea.sys 或 Ufxsynopsys.sys 作为 UFX 到客户端驱动程序加载。</li>
<li>包括 Ufxproprietarycharger.h WDK 中提供。</li>
</ul></td>
<td><p><strong>UFX 的体系结构</strong></p>
<p>熟悉 Microsoft 提供的 USB 驱动程序堆栈：</p>
<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows 中的 USB 设备端驱动程序</a>
<p><strong>熟悉 UFX 对象和句柄</strong></p>
<p>UFX 扩展了 WDF 对象功能来定义其自己特定于 USB 的 UCX 对象。 WDF 对象的更多详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">Framework 对象简介</a>。</p>
<p>对于队列请求，UFX 使用特定于 USB 的对象。 有关详细信息<a href="ufx-objects-and-handles-used-by-a-usb-function-controller.md" data-raw-source="[UFX objects and handles used by a USB function client driver](ufx-objects-and-handles-used-by-a-usb-function-controller.md)">UFX 对象并处理 USB 函数客户端驱动程序使用的</a>。</p>
<p><strong>编写函数控制器客户端驱动程序</strong></p>
<p>了解行为的 UFX，它与客户端驱动程序，以及客户端驱动程序的功能交互的方式应实现。</p>
<p><a href="function-client-driver.md" data-raw-source="[Tasks for a function controller client driver](function-client-driver.md)">函数的控制器客户端驱动程序任务</a></p>
<p><strong>编程参考节</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#function-class-driver-reference" data-raw-source="[USB function class driver to UFX programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#function-class-driver-reference)">USB 到 UFX 编程参考的函数类驱动程序</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usb-function-controller-client-driver-reference" data-raw-source="[USB function controller client driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usb-function-controller-client-driver-reference)">USB 函数控制器客户端驱动程序编程参考</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#filter-driver-for-supporting-usb-chargers" data-raw-source="[USB filter driver for supporting proprietary chargers](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#filter-driver-for-supporting-usb-chargers)">支持专有充电器 USB 筛选器驱动程序</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



