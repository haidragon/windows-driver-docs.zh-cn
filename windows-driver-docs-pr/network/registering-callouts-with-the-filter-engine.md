---
title: 将标注注册到筛选器引擎
description: 将标注注册到筛选器引擎
ms.assetid: a5bade33-e3d1-4e1d-8503-51485097046e
keywords:
- Windows 筛选平台标注驱动程序 WDK，初始化
- 标注驱动程序 WDK Windows 筛选平台，初始化
- 初始化标注驱动程序 WDK Windows 筛选平台
- 注册标注 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f01e15ef409c71704bbbd9b5d37d07fae01828
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374761"
---
# <a name="registering-callouts-with-the-filter-engine"></a>将标注注册到筛选器引擎


标注驱动程序已创建了一个设备对象后，它可以向筛选器引擎中注册其标注。 标注驱动程序可以注册其标注筛选器引擎在任何时候，即使筛选器引擎当前未运行。 要使用筛选器引擎注册一个标注，标注驱动程序调用[ **FwpsCalloutRegister0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutregister0)函数。 例如：

```C++
// Prototypes for the callout's callout functions
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT0  *classifyOut
    );

NTSTATUS NTAPI
 NotifyFn(
 IN FWPS_CALLOUT_NOTIFY_TYPE notifyType,
    IN const GUID  *filterKey,
    IN const FWPS_FILTER0  *filter
    );

VOID NTAPI
 FlowDeleteFn(
    IN UINT16  layerId,
    IN UINT32  calloutId,
    IN UINT64  flowContext
    );

// Callout registration structure
const FWPS_CALLOUT0 Callout =
{
 { ... }, // GUID key identifying the callout
  0,       // Callout-specific flags (none set here)
 ClassifyFn,
 NotifyFn,
 FlowDeleteFn
};

// Variable for the run-time callout identifier
UINT32 CalloutId;

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  PDEVICE_OBJECT deviceObject;
  NTSTATUS status;

  ...

 status =
 FwpsCalloutRegister0(
 deviceObject,
      &Callout,
      &CalloutId
      );

  ...

 return status;
}
```

如果在调用[ **FwpsCalloutRegister0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutregister0)函数运行成功，最后一个参数指向的变量包含标注的运行时标识符。 此运行时标识符对应于指定的标注密钥的 GUID。

单个标注驱动程序可以实现多个标注。 如果标注驱动程序实现多个标注，则会调用[ **FwpsCalloutRegister0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpscalloutregister0)函数为每个标注，它支持使用筛选器引擎注册每个标注一次。

## <a name="related-topics"></a>相关主题


[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

 

 






