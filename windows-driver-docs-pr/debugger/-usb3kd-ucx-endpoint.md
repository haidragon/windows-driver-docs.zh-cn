---
title: usb3kd.ucx_endpoint
description: Usb3kd.ucx_endpoint 命令在 USB 3.0 树中的 USB 设备上显示有关终结点的信息。 显示基于 UcxVersion.sys 保留的数据。
ms.assetid: 37667665-ACA1-48D3-B79E-5B9BBD689034
keywords:
- usb3kd.ucx_endpoint Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_endpoint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6ac241bdc8e19e08be992c6bf79f78d782a02050
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359780"
---
# <a name="usb3kducxendpoint"></a>！ usb3kd.ucx\_终结点


[ **！ Usb3kd.ucx\_终结点**](-usb3kd-device-info.md)命令中的 USB 设备上显示有关终结点信息[USB 3.0 树](usb-3-extensions.md#usb-3-tree)。 显示基于 USB 主控制器扩展驱动程序所维护的数据结构 (Ucx*版本*.sys)。

```dbgcmd
!usb3kd.ucx_endpoint UcxEndpointPrivContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UcxEndpointPrivContext______"></span><span id="_______ucxendpointprivcontext______"></span><span id="_______UCXENDPOINTPRIVCONTEXT______"></span> *UcxEndpointPrivContext*   
地址\_UCXENDPOINT\_PRIVCONTEXT 结构，它表示在终结点。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

USB 主控制器扩展驱动程序 (Ucx*版本*.sys) 提供的 USB 3.0 集线器驱动程序和 USB 3.0 主机之间的抽象层，控制器驱动程序。 扩展驱动程序具有其自己的主机控制器、 设备和终结点的表示形式。 输出 **！ ucx\_终结点**命令基于由扩展驱动程序维护的数据结构。 有关 USB 主控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

<a name="examples"></a>示例
--------

若要获取 UCX 终结点专用上下文的地址，请查看的输出[ **！ ucx\_控制器\_列表**](-usb3kd-ucx-controller-list.md)命令。 在以下示例中，第二个设备上的第一个终结点的专用上下文的地址是 0xfffffa8003694860。

```dbgcmd
3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
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

现在可以将传递到 UCX 终结点专用上下文的地址 **！ ucx\_终结点**命令。

```dbgcmd
3: kd> !ucx_endpoint 0xfffffa8003694860

## Dumping Ucx USB Endpoint Information fffffa8003694860
-----------------------------------------------------
dt ucx01000!_UCXENDPOINT_PRIVCONTEXT 0xfffffa8003694860
[Blk Out], UcxEndpointStateEnabled, MaxTransferSize: 4194304
Endpoint Address: 0x02
Endpoint Queue: !wdfqueue 0x57ffc969888

UcxEndpoint State History: <Event> NewState 
    [ 3] <UcxEndpointEventOperationSuccess> UcxEndpointStateEnabled
    [ 2] <UcxEndpointEventYes> UcxEndpointStateCompletingPendingOperation1
    [ 1] <UcxEndpointEventEnableComplete> UcxEndpointStateIsAbleToStart2
    [ 0] <SmEngineEventStart> UcxEndpointStateCreated

UcxEndpoint Event History:
    [ 1] UcxEndpointEventEnableComplete
    [ 0] SmEngineEventStart

EventCallbacks:
    EvtEndpointPurge: (0xfffff880044ba6e8) USBXHCI!Endpoint_UcxEvtEndpointPurge
    EvtEndpointAbort: (0xfffff880044ba94c) USBXHCI!Endpoint_UcxEvtEndpointAbort
    EvtEndpointReset: (0xfffff880044bb854) USBXHCI!Endpoint_UcxEvtEndpointReset
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[ **!usb3kd.ucx\_controller\_list**](-usb3kd-ucx-controller-list.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






