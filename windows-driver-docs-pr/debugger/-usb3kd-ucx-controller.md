---
title: usb3kd.ucx_controller
description: Usb3kd.ucx_controller 命令显示有关 USB 3.0 主控制器的信息。 显示基于由 UcxVersion.sys 维护的数据结构。
ms.assetid: A2768E47-C8D7-4A01-80AC-98FB5AAA17BD
keywords:
- usb3kd.ucx_controller Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f358e645c89bca3daa351e08105f070013be35a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359788"
---
# <a name="usb3kducxcontroller"></a>!usb3kd.ucx\_controller


[ **！ Usb3kd.ucx\_控制器**](-usb3kd-device-info.md)命令显示有关 USB 3.0 主控制器的信息。 显示基于 USB 主控制器扩展驱动程序所维护的数据结构 (Ucx*版本*.sys)。

```dbgcmd
!usb3kd.ucx_controller UcxControllerPrivContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UcxControllerPrivContext______"></span><span id="_______ucxcontrollerprivcontext______"></span><span id="_______UCXCONTROLLERPRIVCONTEXT______"></span> *UcxControllerPrivContext*   
地址\_UCXCONTROLLER\_PRIVCONTEXT 结构，它表示控制器。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

USB 主控制器扩展驱动程序 (Ucx*版本*.sys) 提供的 USB 3.0 集线器驱动程序和 USB 3.0 主机之间的抽象层，控制器驱动程序。 扩展驱动程序具有其自己的主机控制器、 设备和终结点的表示形式。 输出[ **！ ucx\_控制器**](-usb3kd-device-info.md)命令基于由扩展驱动程序维护的数据结构。 有关 USB 主控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

<a name="examples"></a>示例
--------

若要获取 UCX 控制器专用上下文的地址，请查看的输出[ **！ ucx\_控制器\_列表**](-usb3kd-ucx-controller-list.md)命令。 在以下示例中，专用上下文的地址是 0xfffffa80052da050。

```dbgcmd
3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        ...
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        ...
```

现在可以将传递到 UCX 控制器专用上下文的地址[ **！ ucx\_控制器**](-usb3kd-device-info.md)命令。

```dbgcmd
3: kd> !ucx_controller 0xfffffa80052da050

## Dumping Ucx Controller Information fffffa80052da050
---------------------------------------------------
dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT 0xfffffa80052da050
Parent Device: !wdfdevice 0x57ffac91fd8
Controller Queues:
    Default               : !wdfqueue 0x57ffacc5fd8
    Address'0'Ownership   : !wdfqueue 0x57ffad5ad88
    DeviceManagement      : !wdfqueue 0x57ffacd6fd8
    ... pend on Ctrl Reset: !wdfqueue 0x57ffad48fd8

Controller Reset State History: <Event> NewState 
    [ 2] <ControllerResetEventOperationSuccess> ControllerResetStateRHPdoInD0
    [ 1] <ControllerResetEventRHPdoEnteredD0> ControllerResetStateStopBlockingResetComplete1
    [ 0] <SmEngineEventStart> ControllerResetStateRhPdoInDx

Controller Reset Event History:
    [ 1] ControllerResetEventRHPdoEnteredD0
    [ 0] SmEngineEventStart

Root Hub PDO: !wdfdevice 0x57ffaf4daa8
Number of 2.0 Ports: 2
Number of 3.0 Ports: 2
RootHub Control !wdfqueue 0x57ffacb4798
RootHub Interrupt !wdfqueue 0x57ffad033f8, pending !wdfequest 0x57ffa5fe998

Device Tree:
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa80053405d0 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005a3f710 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005bbe4e0 [Blk Out], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa8005ac4810 [Blk In ], UcxEndpointStateStale
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003686820 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005be0550 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003695580 [Blk In ], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa80036a20c0 [Blk Out], UcxEndpointStateStale
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[ **!usb3kd.ucx\_controller\_list**](-usb3kd-ucx-controller-list.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






