---
title: 支持生物识别 IOCTL 调用序列
description: 支持生物识别 IOCTL 调用序列
ms.assetid: e6555895-8936-4f5d-8f2b-05b5283edbee
keywords:
- 生物识别驱动程序 WDK，支持 Ioctl
- 支持 Ioctl WDK 生物识别
- Ioctl WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91d6ac6f024310295e152932c3ed497e2efe2ed2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364677"
---
# <a name="supporting-biometric-ioctl-calling-sequence"></a>支持生物识别 IOCTL 调用序列


WBDI 是 Windows 标准基于 IOCTL 的接口。 在编写 WBDI 驱动程序时，必须支持一系列必需 Ioctl。 此外，可支持可选 Ioctl。 您可以查找中的必需和可选 Ioctl 的完整列表[生物识别 Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

供应商提供 WBDI 驱动程序应准备好按以下顺序 Windows 生物识别服务 (WBS) 从接收 IOCTL 请求。 你可以查看的处理程序的示例中的 Device.cpp 中这些 Ioctl [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)。

1.  Windows 生物识别服务或传感器适配器初始化生物识别设备并验证它准备好用于。 服务或适配器发送[ **IOCTL\_生物识别\_获取\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_attributes)请求。

    驱动程序收到一个指向[ **WINBIO\_传感器\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_sensor_attributes)结构。 在此 IOCTL 的处理程序，该驱动程序应填充此结构的相关成员并完成请求，通过调用[ **IWDFIoRequest::Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)。

2.  接下来，驱动程序收到[ **IOCTL\_生物识别\_获取\_传感器\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_sensor_status)。 该驱动程序的相关成员中应填充[ **WINBIO\_诊断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)结构并完成该请求。

3.  如果驱动程序指示有必要在校准**SensorStatus**的成员[ **WINBIO\_诊断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)从返回的结构IOCTL\_生物识别\_获取\_传感器\_状态请求，接下来，驱动程序收到[ **IOCTL\_生物识别\_校准** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_calibrate)请求。 此 IOCTL，该驱动程序必须提供一个处理程序。 校准设备之后, 该回调应返回[ **WINBIO\_校准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_calibration_info)结构。

4.  该驱动程序现在会收到[ **IOCTL\_生物识别\_捕获\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data)请求。 因为只有一个捕获可以处于挂起状态在任何时候，此请求的处理程序应首先确认没有请求处于挂起状态。 如果申请处于挂起状态，完成该请求与 WINBIO\_E\_数据\_集合\_IN\_进度。

    WinBio 服务或应用程序可以通过调用 Win32 取消例程，如请求取消未完成捕获请求的任何时候[ **CancelIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelio)， [ **CancelIoEx**](https://docs.microsoft.com/windows/desktop/FileIO/cancelioex-func)，或[ **CancelSynchronousIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelsynchronousio-func)。 在这种情况下，WBDI 驱动程序还必须支持取消。

    该驱动程序通过调用来处理取消[ **IWDFIoRequest::MarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-markcancelable)注册[IRequestCallbackCancel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-irequestcallbackcancel)接口。

    然后，该处理程序程序设备的捕获模式，并从回调返回。 请求应保持挂起状态直到被取消或驱动程序检测到捕获的已完成。 此 I/O 请求完成后，设备可以返回到空闲状态。 客户端可能会进行初始调用到 IOCTL\_生物识别\_捕获\_数据以确定实际捕获的正确的缓冲区大小。

5.  处理程序[ **IOCTL\_生物识别\_重置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_reset)应以物理方式将设备重置到已知的或空闲状态。 此请求的处理程序还必须取消任何挂起的数据收集 I/O 并填写[ **WINBIO\_空白\_负载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ns-winbio_ioctl-_winbio_blank_payload)结构。 然后，该处理程序完成请求。 客户端不需要调用之间调用 IOCTL 重置\_生物识别\_捕获\_数据。

 

 





