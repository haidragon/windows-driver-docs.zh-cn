---
title: WDTF 对象日志记录
description: WDTF 对象日志记录
ms.assetid: A99E62D1-31A2-46B5-841B-F3969854E39A
keywords:
- 日志记录 WDK WDTF
- 跟踪 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edaf8fa5df87d1586039cbbefed956e2769fa9ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369482"
---
# <a name="wdtf-object-logging"></a>WDTF 对象日志记录





WDTF 对象*日志记录*是 WDTF，可以将 WDTF 对象会自动向公用日志文件写入日志消息中的功能。 对象日志记录文件的名称称为 TestTextLog.log。 WDTF 对象日志记录有两个主要优点。 它简化了使用 WDTF 对象方法来记录在高级别方法调用，该方法的参数和方法的结果编写的测试脚本。 WDTF 对象日志记录还可诊断性提高通过提供一致的机制，用于编写常见日志消息。

默认情况下禁用 WDTF 对象日志记录。 通过调用启用对象日志记录[ **IWDTFConfig2::EnableObjectLogging** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfconfig2-enableobjectlogging)方法。 启用日志记录后，可以暂时禁用或重新启用它的特定操作或操作的集合通过调用方法[ **IWDTFAction2::EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfaction2-enableobjectlogging)， [**IWDTFAction2::DisableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfaction2-disableobjectlogging)， [ **IWDTFActions2::EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，和[ **IWDTFActions2::DisableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

WDTF 写入日志文件的日志消息具有通用模式。

```cpp
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
```

下面的示例演示对的调用的日志记录输出**DeviceDepot.Query("Volume::")** 示例系统启用日志记录时。

```cpp
[ Output ]

WDTF_TARGETS    : INFO  :  - Query("Volume::")
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: HL-DT-ST RW/DVD MU10N ATA Device
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
```

如果启用日志记录对象，则默认情况下被启用对象错误日志记录。 否则，错误日志记录默认为禁用状态。 如对象日志记录，你可以启用/禁用错误日志记录通过调用方法[ **IWDTFConfig2::EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfconfig2-enableobjecterrorlogging)， [ **IWDTFConfig2::DisableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfconfig2-disableobjecterrorlogging)， [ **IWDTFAction2::EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfaction2-enableobjecterrorlogging)， [ **IWDTFAction2::DisableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtfaction2-disableobjecterrorlogging)， [ **IWDTFActions2::EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，以及[ **IWDTFActions2::DisableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

WDTF 写入错误日志记录的日志文件的日志消息具有以下模式。 查找的关键字"错误"要跳转到日志中的第一个错误。

``` syntax
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
<OBJECT_NAME> : ERROR : Status: <ErrorString>
```

您仍然可以将无法写入到日志文件的自定义消息，通过调用[ **IWDTFLog2::OutputInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtflog2-outputinfo)或[ **IWDTFLog2::OutputError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtflog2-outputerror)方法。

有关可用的对象的列表，请参阅[WDTF 对象名称标记](wdtf-object-name-tags.md)。

## <a name="related-topics"></a>相关主题
[WDTF 对象名称标记](wdtf-object-name-tags.md)  
[启用和查看 WDTF 跟踪](viewing-wdtf-traces.md)  



