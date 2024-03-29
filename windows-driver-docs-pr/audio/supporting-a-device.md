---
title: 支持某个设备
description: 支持某个设备
ms.assetid: 5f60d3aa-6061-40f7-8108-d752534b88ed
keywords:
- 音频的微型端口驱动程序 WDK、 设备支持
- 微型端口驱动程序 WDK 音频设备支持
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频设备支持
- 端口驱动程序 WDK 音频，微型端口驱动程序
- 端口驱动程序 WDK 音频，端口类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1410d6abc90842112044136429ae642ed6462a74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354222"
---
# <a name="supporting-a-device"></a>支持某个设备


## <span id="supporting_a_device"></span><span id="SUPPORTING_A_DEVICE"></span>


PortCls 系统驱动程序 (*Portcls.sys*) 提供了几个内置端口驱动程序以支持的呈现和捕获批和 MIDI 流音频设备。

所有端口驱动程序将派生自基接口的接口都公开[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)。 **IPort**方法继承自基接口**IUnknown**。 **IPort**提供了以下其他方法：

[**IPort::GetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-getdeviceproperty)

从注册表检索的音频适配器插属性。
[**IPort::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-init)

初始化端口对象。
[**IPort::NewRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-newregistrykey)

创建新的注册表项或打开现有的密钥。
PortCls 实现以下端口驱动程序：

[WaveCyclic 端口驱动程序](wavecyclic-port-driver.md)

[WavePci 端口驱动程序](wavepci-port-driver.md)

[WaveRT 端口驱动程序](wavert-port-driver.md)

[拓扑端口驱动程序](topology-port-driver.md)

[MIDI 端口驱动程序](midi-port-driver.md)

[Dmu 端口驱动程序](dmus-port-driver.md)

 

 




