---
title: 提取并设置控制数据的数据索引
description: 提取并设置控制数据的数据索引
ms.assetid: d26d169f-4116-4d81-94c7-63c92d22877d
keywords:
- HID 报告 WDK，设置控制数据
- 报告 WDK HID，设置控制数据
- HID 的报表 WDK，提取控件数据
- WDK HID，提取控件数据的报表
- HID 控制如何将数据提取
- 数据编制索引 WDK HID
- 索引 WDK HID 数据
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f98a484a5de3e3adf093dc6a81025b72556b23b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375719"
---
# <a name="extracting-and-setting-control-data-by-data-indices"></a>提取并设置控制数据的数据索引





若要使用[数据索引](data-indices.md)若要提取并设置控制数据在 HID 报表中，应用程序或驱动程序可以使用下面的 HID 支持例程：

[**HidP\_GetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getdata)

[**HidP\_SetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setdata)

这些例程是应用程序或驱动程序，提供"增值"服务特别有用。 例如，一个提供了 HIDClass 设备支持的所有控件的自定义界面。 Microsoft DirectInput 是一个示例。

通过调用这些例程，应用程序或驱动程序最有效地可获取和设置在报表中的所有值。 例如，若要获取所有数值数据，通过其[HID 用法](hid-usages.md)，它必须调用[ **HidP\_GetUsageValue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevalue)为每个用途。 但是，若要获取所有值的数据的数据索引，它仅有调用**HidP\_GetData**后。

应用程序或驱动程序使用的集合中指定的数据索引[按钮功能数组](button-capability-arrays.md)并[值功能数组](value-capability-arrays.md)来标识 HID 用法。

 

 




