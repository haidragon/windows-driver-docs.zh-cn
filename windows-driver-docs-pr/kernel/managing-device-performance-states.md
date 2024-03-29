---
title: 管理设备性能状态
description: 管理设备性能状态
ms.assetid: 5a4cc09a-e86e-4e5a-98b2-0351b253b5b6
keywords:
- 电源管理 WDK 内核、 设备性能状态
- 设备性能状态 WDK 电源管理
- 性能状态 WDK 电源管理
- 自定义电源设置 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e07ac7c0b3548e09d8ef5a5c43fd23a12530e50a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365787"
---
# <a name="managing-device-performance-states"></a>管理设备性能状态


Windows Vista 功能的增强型的电源管理基础结构，它使驱动程序堆栈以更好地管理其设备的电源策略。 驱动程序可以注册以系统定义的电源设置更改时，或系统电源事件发生时收到通知。 设备电源策略所有者可以使用这些通知相应地调整其设备的电源使用情况。 此外，您可以创建提供访问特定于设备的能力和性能功能，可以是紧密集成到系统电源策略的自定义电源设置。 以下是两个主要的方法来将设备性能状态和能源节约行为与系统电源策略集成。

[创建自定义电源设置的设备](#creating-custom-power-settings-for-a-device)

[注册为 Notified 变为活动状态的电源方案、 电源方案个性或电源](#registering-to-be-notified-of-a-change-to-the-active-power-scheme)

### <a href="" id="creating-custom-power-settings-for-a-device"></a> 创建自定义电源设置的设备

可以定义可用于配置设备性能状态或节能行为的自定义电源设置。 有关自定义电源设置的信息是保存和管理的电源管理器。 在系统中的其他组件，如设备驱动程序、 服务或应用程序，可以注册以自定义电源设置的值更改时得到通知。 一般情况下，设备有电源消耗的牺牲性能的功能应具有相应的自定义电源设置。 创建自定义电源设置是最灵活的方法来将功率消耗与系统电源策略紧密集成，并提供以下其他好处：

-   自定义用户界面不需要进行自定义电源设置的用户可以访问。 所有电源设置，包括自定义电源设置向用户都显示上**高级设置**页**电源选项**控制面板。

-   用户和系统管理员可以轻松地编写脚本的自定义电源设置的配置通过使用 Powercfg.exe，电源管理命令行工具。

-   （可选） 的系统管理员可以创建的管理模板 (。ADM) 文件，它使组基于策略的新的电源设置的配置。

单个电源设置包含所有唯一地标识名称、 描述和提供的电源设置的值所需的信息。 每个电源设置 GUID、 设置名称、 说明，与交流和直流电源方案的默认设置定义。 自定义电源设置可以创建以静态方式对于设备，通过使用[ **INF AddPowerSetting 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addpowersetting-directive)，或动态注册，通过调用 Win32 电源管理功能的强大功能中包含使用 Microsoft Windows SDK 文档提供的管理参考。

驱动程序调用[ **PoRegisterPowerSettingCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregisterpowersettingcallback)注册电源管理器调用以通知对电源设置的更改的驱动程序的回调例程。 该设置更改时，电源管理器调用回调例程，并传递新的设置值。 驱动程序然后可以采取相应的电源设置的操作。 每个设置都由的电源设置 GUID 标识。 Wdm.h 中和 Ntpoapi.h 中定义的系统定义的电源设置 Guid。

例如，若要打开或关闭监视器电源处于打开状态时收到通知，驱动程序调用**PoRegisterPowerSettingCallback**，提供标识显示器的电源设置 GUID (GUID\_监视器\_电源\_ON) 和显示器电源设置的值更改时，电源管理器调用的回调例程的指针。

### <a href="" id="registering-to-be-notified-of-a-change-to-the-active-power-scheme"></a>注册为 Notified 变为活动状态的电源方案、 电源方案个性或电源

活动的电源方案的个性传达整体的节能的系统行为的用户的意图。 每个电源方案，包括自定义方案，具有各自的特点，指示总体方案的意图。 这样，其他自定义电源方案，同时仍提供的所有了解方案的意图权益创建。 Windows Vista 包括以下三个系统定义的电源使用方案和其相应的个性。

<a href="" id="maximum-power-savings"></a>**最大电源节省量**  
会降低性能，以最大程度减少电源消耗。

<a href="" id="automatic--balanced-"></a>**自动 （平衡）**  
可让系统在选择最佳的电源状态级别根据整体功率消耗。

<a href="" id="maximum-performance-------"></a>**最大性能**   
提供了最大性能，而不考虑功率消耗。

Power 源可以是交流电还是 DC 电源。

设备电源策略所有者可以使用有关活动的电源方案、 电源方案个性和电源的信息来调整设备的电源策略。 例如，设备电源策略所有者可能会主动关闭的设备如果电源方案个性更改为**最大电源节省量**。 但是，如果更改为电源方案个性**最大性能**，设备电源策略所有者可能会保持其设备的性能级别而不是减少能源消耗，并可能会使该设备提供支持在所有时间以确保最高级别的性能。

驱动程序可以注册到活动的电源方案、 电源方案个性或电源发生更改时收到通知。 驱动程序调用**PoRegisterPowerSettingCallback**注册的回调例程的电源管理器调用以通知此类更改的驱动程序，如下所示：

-   若要注册到活动的电源方案的更改的通知，提供表示的电源方案设置的 GUID (GUID\_ACTIVE\_POWERSCHEME)。 电源管理器将然后调用回调例程时活动的电源方案发生更改，即使新的电源方案的个性等同于以前的电源方案。

-   若要注册到电源方案个性更改的通知，提供表示的电源方案个性设置的 GUID (GUID\_POWERSCHEME\_个性)。 不同于以前的电源方案的个性活动的电源方案更改和新的电源方案的个性时，电源管理器将然后调用回调例程。

-   若要注册到电源更改的通知，提供表示的电源设置 GUID (GUID\_ACDC\_电源\_源)。 每当 power 源设置发生更改时，电源管理器将然后调用回调例程。

当活动的电源方案更改或电源方案个性更改，电源管理器调用回调例程，并将传递 GUID 表示的新的电源方案或电源方案个性。 驱动程序然后可以采取相应的更改的操作。

活动的电源方案设置和电源方案个性设置使用以下 Guid 来标识其各自的值：

-   GUID\_最大\_电源\_节省，对应于**最大电源节省量**电源方案和其相应的个性。

-   GUID\_最小\_电源\_节省，对应于**最大性能**电源方案和其相应的个性。

-   GUID\_典型\_电源\_节省，对应于**自动 （平衡）** 电源方案和其相应的个性。

当电源源更改时，电源管理器调用回调例程而交流电源，直流电源通过传递 GUID，表示电源源设置和电源源设置，指示计算机是否正在提供支持的值源或短期的直流电源。

 

 




