---
title: 在 WDF 中调试电源参考漏孔
description: 当 Windows 驱动程序框架 (WDF) 驱动程序调用 WdfDeviceStopIdle 时，框架将递增设备的 power 引用计数。
ms.assetid: 25F4EEBB-4733-498C-8704-8E015F81FE06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d66337d9180fb9d3233a49b684409dc64e14c50e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377494"
---
# <a name="debugging-power-reference-leaks-in-wdf"></a>在 WDF 中调试电源参考漏孔


当 Windows 驱动程序框架 (WDF) 驱动程序调用[ **WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)，framework 递增设备的 power 引用计数。 每次成功调用**WdfDeviceStopIdle**必须通过调用匹配[ **WdfDeviceResumeIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)以减少 power 引用计数。

从内核模式驱动程序框架 (KMDF) 1.15 和用户模式驱动程序框架 (UMDF) 2.15，您可以通过监视电源引用使用情况[ **！ wdfkd.wdfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)和[ **！ wdfkd.wdftagtracker** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)调试器扩展。 因此您需要与 WdfVerifier 应用程序或通过手动编辑驱动程序的服务密钥，则会将其打开，出于性能原因，默认情况下禁用此功能。

## <a name="wdfverifier"></a>WdfVerifier


打开您的驱动程序和右键单击的设置列表**TrackPower**设置。 选择适合你方案的选项。

**提示**  避免捕获性能关键代码路径中的堆栈跟踪。

 

![设置跟踪 power wdfverifier 中的引用](images/wdfverifier--track-power-references-on.png)

## <a name="editing-the-registry"></a>编辑注册表


您还可以启用验证工具支持和 power 引用跟踪通过编辑您的驱动程序的服务密钥。

KMDF 驱动程序：

**HKLM\\系统\\ControlSet001\\Services\\&lt;驱动程序服务名称&gt;\\参数\\Wdf**

UMDF 驱动程序：

**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;驱动程序服务名称&gt;\\参数\\Wdf**

```cpp
(REG_DWORD) VerifierOn = 0x1
(REG_DWORD) TrackPower = 0x0 (disabled)
                       = 0x1 (capture tick count, file name, line number)
                       = 0x2 (capture tick count, file name, line number, and stack traces)
```

## <a name="driver-code"></a>驱动程序代码


驱动程序调用[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)并[ **WdfDeviceResumeIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)来管理设备的工作电源状态，如下所示：

```cpp
//
// Take power reference
//
status = WdfDeviceStopIdle(device, FALSE);
if (NT_SUCCESS(status)) {
    //
    // Release power reference
    //
    WdfDeviceResumeIdle(device);
}
```

## <a name="debugging-with-wdfkd"></a>使用 WdfKd 进行调试


若要显示执行该设备，以及一个显示引用历史记录的标记跟踪器的 power 引用，请使用[ **！ wdfkd.wdfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)与 verbose 标志：

```cpp
kd> !wdfkd.wdfdevice 0x6d939790 ff
Power references: 0 !wdftagtracker 0x9ea030a8
```

调用[ **！ wdfkd.wdftagtracker** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)显示设备的 power 引用历史记录：

```cpp
kd> !wdftagtracker 0x9ea030a8
Reference and Release History:
# (showing most recent first; refcount is approximate in multi-threaded scenarios)

## 3 entries, history depth is 25

(--) 0 ref: Tag '....' at Time 0x1331e ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag '....' at Time 0x1331e ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

## <a name="specifying-a-tag"></a>指定一个标记


（可选） 指定标记名称，便于识别特定电源的引用。 若要执行此操作，请使用[ **WdfDeviceStopIdleWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevicestopidlewithtag)并[ **WdfDeviceResumeIdleWithTag**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdeviceresumeidlewithtag):

```cpp
status = WdfDeviceStopIdleWithTag(device, FALSE, (PVOID)'oyeH');
if (NT_SUCCESS(status)) {
    WdfDeviceResumeIdleWithTag(device, (PVOID)'oyeH');
}
```

对应[ **！ wdftagtracker** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)示例输出：

```cpp
(--) 0 ref: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

 

 





