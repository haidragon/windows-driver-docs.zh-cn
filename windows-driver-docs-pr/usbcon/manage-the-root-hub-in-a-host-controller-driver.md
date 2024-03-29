---
Description: UCX 执行根中心管理。
title: USB 主控制器驱动程序的根集线器回调函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66c499f43cd6e7dc45541943d11bf8d89867969d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364819"
---
# <a name="root-hub-callback-functions-of-a-usb-host-controller-driver"></a>USB 主控制器驱动程序的根集线器回调函数


UCX 执行根中心管理。 它模拟和管理虚拟控件和中断终结点。 UCX 主机控制器驱动程序创建根集线器对象时创建这些虚拟终结点。

USB 集线器驱动程序中使用正则中心设备进行交互的相同方式与根中心进行交互。 但是，主机控制器驱动程序无需处理请求直接发送到根中心控件和中断终结点。 UCX 处理这些请求。 UCX 调用回调函数，以便它可以返回有关主控制器的端口的当前状态的相关信息由主机控制器驱动程序实现。 当这些回调函数完成时，基础 UCX 请求都已完成并返回到中心驱动程序。

在接收到根集线器中断传输，UCX 设置为挂起的请求。 其中一个根集线器端口上检测到更改时，主机控制器驱动程序调用[ **UcxRootHubPortChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nf-ucxroothub-ucxroothubportchanged)。 UCX 然后调用驱动程序的[ *EVT\_UCX\_ROOTHUB\_中断\_TX* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx)回调和驱动程序指示已更改的端口. 在此期间，UCX 完成回中心驱动程序的挂起请求。 中心驱动程序将控件传输发送到根中心，以获取终止状态更改的端口的端口状态。 UCX 设置为该控件转移请求挂起，并调用在驱动程序[ *EVT\_UCX\_ROOTHUB\_控制\_URB* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb)回调函数。 在实现中返回的当前状态的根集线器端口，包括设备连接的指示。 UCX 完成控制传输请求到中心驱动程序，并且设备枚举将继续。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)  



