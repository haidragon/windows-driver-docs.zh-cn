---
title: 打印功能的 Win32 API 支持
description: 打印功能的 Win32 API 支持
ms.assetid: 1b40cc3e-c6f6-460f-b514-4ef3a001f563
keywords:
- 打印功能 WDK，Win32 API 支持
- DrvDeviceCapabilities
- Win32 应用程序 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bc1c3fc6afccf301ab2e2709a88fcbd7573d84e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368972"
---
# <a name="win32-api-support-for-print-capabilities"></a>打印功能的 Win32 API 支持


Windows Vista 打印子系统提供了兼容性支持，允许 Windows Presentation Foundation (WPF) 应用程序使用基于 GDI 的打印驱动程序并使 Microsoft 基于 Win32 的应用程序可以使用 XPSDrv 打印驱动程序。 此兼容性提供通过软件填充程序的一个层。 填充程序是转换对数据执行操作，以便否则互操作不兼容的软件的软件模块。 下图显示了此实现用于打印功能的数据路径。

![说明打印功能的数据流关系图](images/ptpccomp.gif)

这两[XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md)和基于 GDI 的版本 3 打印驱动程序支持[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)函数。 在 Win32 应用程序调用**DrvDeviceCapabilities**或**GetDevCap**函数，将调用打印子系统**DrvDeviceCapabilities**收集设备从打印驱动程序的功能信息。

当 WPF 应用程序请求 PrintCapabilities 文档从打印驱动程序时，打印子系统将执行下列任一操作：

-   如果打印驱动程序支持[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))，打印子系统将通过使用查询 PrintCapabilities 文档的打印驱动程序[ **IPrintTicketProvider::GetPrintCapabilities** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554365(v=vs.85))方法。

-   如果打印驱动程序不支持**IPrintTicketProvider**接口，打印票证管理器将查询[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)打印函数驱动程序并使用返回的信息创建 PrintTicket 文档返回到应用程序。

详细了解如何**IPrintTicketProvider** Microsoft 打印驱动程序支持的接口，请参阅[打印机驱动程序和 Windows Vista 中的插件接口设计](printer-driver-and-plug-in-helper-interfaces.md)。

 

 




