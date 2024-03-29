---
title: 初始化虚拟微型端口
description: 初始化虚拟微型端口
ms.assetid: 5f2e23a9-375b-4b0d-95d2-5a3af1acb3be
keywords:
- 初始化虚拟微型端口
- 虚拟微型端口 WDK 网络
- NDIS 中间层驱动程序 WDK，虚拟微型端口
- 中间驱动程序 WDK 网络、 虚拟微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2900e4c7b800b2d6f004ad60ad121b2b9f2eef8e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381301"
---
# <a name="initializing-a-virtual-miniport"></a>初始化虚拟微型端口





若要启动的虚拟微型端口初始化，中间驱动程序调用[ **NdisIMInitializeDeviceInstanceEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)函数。 中间驱动程序，通常可以从此调用其[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。 中间驱动程序调用后**NdisIMInitializeDeviceInstanceEx**和即插即用播放管理器请求以启动虚拟设备的 NDIS、 NDIS 调用驱动程序的[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

在调用*MiniportInitializeEx*的上下文中可以是**NdisIMInitializeDeviceInstanceEx**如果插管理器将启动虚拟设备之前**NdisIMInitializeDeviceInstanceEx**返回。 如果中间驱动程序提供了多个虚拟微型端口，该驱动程序必须调用**NdisIMInitializeDeviceInstanceEx**为可通过其每个虚拟微型端口。

NDIS 将传递到初始化参数*MiniportInitializeEx*中[ **NDIS\_微型端口\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_init_parameters)在结构*MiniportInitParameters* 。 **IMDeviceInstanceContext**结构中的成员指定指向虚拟设备的上下文区域的指针。 该驱动程序传递到此指针[ **NdisIMInitializeDeviceInstanceEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)在正常*DeviceContext*参数。

在中*MiniportInitializeEx*，中间驱动程序执行初始化虚拟微型端口所需的操作。 此初始化是类似于任何其他微型端口适配器初始化。

 

 





