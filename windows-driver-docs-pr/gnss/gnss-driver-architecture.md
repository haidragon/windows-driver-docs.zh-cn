---
title: GNSS 驱动程序体系结构
description: 概述了 GNSS UMDF 2.0 驱动程序体系结构，I/O 注意事项，并讨论了几种类型的跟踪和修补程序的会话。
ms.assetid: 11B54F92-DC84-4D74-9BBE-C85047AD2167
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: a27cd96060652aa2d9ae6d662525e3ae0f60b4fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385180"
---
# <a name="gnss-driver-architecture"></a>GNSS 驱动程序体系结构


概述了 GNSS UMDF 2.0 驱动程序体系结构，I/O 注意事项，并讨论了几种类型的跟踪和修补程序的会话。

## <a name="architecure-overview"></a>体系结构概述


以下高级别组件块图显示了 GNSS UMDF 2.0 驱动程序如何与 Windows 10 平台相集成。

![显示用户模式 gnss 体系结构关系图](images/gnss-architecture-4.png)

此处介绍了在关系图中的组件：

-   **LBS 应用程序：** 使用 Windows 10 平台的位置功能的用户应用程序

-   **测试应用程序：** 用于测试 GNSS 功能的应用程序。

-   **GNSS API:** **IGnssAdapter** COM （组件对象模型） 接口的公开 GNSS 设备连接到的位置服务，以及关于测试应用程序的内部组件的功能。 此 API 的确切形状是本文档的讨论范围内。 Windows 组件使用 GNSS 设备通过对编程**IGnssAdapter** COM 接口。 GNSS API 集是为唯一位置平台组件 （例如，位置服务和位置测试应用程序） 的专用 API，对其他第一方或第三方应用程序不可用。

-   **GNSS 适配器：** 这是一个独立 COM 对象实现**IGnssAdapter** COM 接口。 测试应用程序和位置服务的内部组件实例化此对象并使用通过在 GNSS 设备**IGnssAdapter**接口。 位置服务的 GNSS 定位引擎组件实现公开的 COM 类**IGnssAdapter**接口。 位置服务公开的工厂机制来测试和其他用于实例化 GNSS 适配器内的位置服务的 COM 类的单一实例 COM 对象的进程外应用程序。 进程外应用程序使用对 GNSS 驱动程序进行编程的 COM 接口指针。

    > [!NOTE]
    > COM 处理代理的进程外应用程序的接口指针，以便应用程序将视为**IGnssAdapter**接口指针视为进程内 COM 对象，但调用实际上由单一实例 GNSS位置服务中的适配器对象。

    定位引擎 GNSS 使用提供的位置服务的特定于位置的功能的内部 GNSS 适配器对象。 GNSS 适配器打开的文件句柄 GNSS 驱动程序使用**CreateFile** API，然后将包装到适当的 GNSS 本机 Api 调用**DeviceIoControl**调用中，会保留与 GNSS 状态机驱动程序对象和维护从上层的各种传入请求的状态。 此组件直接与基础 GNSS 设备堆栈通过本文档中定义的公共 GNSS IOCTL 接口进行交互。 GNSS 设备以逻辑方式视为独占资源，因此单独 GNSS 适配器控制到 GNSS 设备的所有访问。

    > [!NOTE]
    > 某些白盒驱动程序测试应用程序还可以使用 GNSS 驱动程序 IOCTL 接口直接在非生产环境中的，而不是使用 GNSS 适配器通过 GNSS 私有 Api。 但是，这些测试应用程序必须实现其自己的状态机和处理，以模拟 GNSS 适配器的特定功能。



-   **GNSS 驱动程序：** IHV 提供驱动程序使用 UMDF 2.0 实现。 GNSS 驱动程序支持 GNSS **DeviceIoControl** Api 通过与实际 GNSS 硬件进行连接。 GNSS 驱动程序还可用作转存进程/集成商 SUPL 函数。

-   **GNSS 设备/引擎：** 这是封装 GNSS 设备的 SoC 和硬件部分的概念组件。 IHV 可以选择实现大部分 GNSS 功能中此组件，从而使 GNSS 驱动程序层非常精简 （实质上是与 GNSS 设备进行连接的适配器）。

## <a name="support-for-gnss-devices-and-drivers-that-follow-the-legacy-windows-model"></a>GNSS 设备和驱动程序，请按旧的 Windows 模式的支持


Windows 10 中的位置平台支持的旧的传感器 v1.0 类驱动程序通过集成 GNSS 设备 (请参阅[编写的位置传感器驱动程序](writing-a-location-sensor-driver.md)) 或通过新集成 GNSS DDI 所述对[GNSS 驱动程序引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver)。

因此，应将与 Windows 7、 Windows 8 和 Windows 8.1 中已存在的传感器 v1.0 类扩展模型集成的 Windows 设备与 GNSS 设备继续在 Windows 10 中工作而无需任何更改。 强烈建议为这些驱动程序 （和任何新驱动程序） 发布到 Windows 更新来改进我们的用户的升级过程。

此外将为两组不同的 GNSS 设备在硬件实验室 Kit (HLK) 发出，使用 Windows 10 的测试：

-   一个新的测试来验证的新模型的驱动程序集。

-   要验证的旧模型的驱动程序的测试的另一组。 这些将是相同的可在 Windows 8.1 中 WHCK 测试集。

新的收集器组件中 HLK 标识这两组测试需要运行在系统中，如果有的话。

![显示 gnss 2.0 的驱动程序和适配器通信的示意图](images/gnss-architecture-5.png)

## <a name="coexistence-of-gnss-devices"></a>GNSS 设备的并存


在检测到系统中的多个 GNSS 设备的极少数情况下，位置平台将仅使用一台设备，主要是为了降低整体系统中电源消耗。 考虑了以下假设：

-   使用新 DDI 设备很可能是更高版本，且因此更有可能具有更好的功率消耗、 支持多个星座互动和更好地支持获得帮助。 因此如果检测到使用旧的驱动程序模型的设备和设备使用了新的驱动程序模型，后者将为所选的一个。

-   如果存在一个内部 GNSS 设备时，用户将外部 GNSS 设备，，则很可能用户想要使用此外部设备。

位置平台，根据这些设想的行为将如下所示：

-   两个 coexistent 旧驱动程序的情况：若要避免该行为将与 Windows 8.1，在这两个哪些 GNSS 设备都使用，同时，另一个的响应中的相同的后兼容性问题会传送到应用程序堆栈。

-   在设备中的一个旧驱动程序和外部插入一个新的驱动程序的情况：使用外部插入的 GNSS 设备。

-   在设备中的一个新的驱动程序和外部插入一个新的驱动程序的情况：使用外部插入的 GNSS 设备。

如果所选的 GNSS 设备支持地理围栏或其他卸载的操作，然后卸载会执行时使用该设备。 功能或在多个 GNSS 设备之间的会话，将不会拆分 GNSS 适配器。

## <a name="gnss-interface-overview"></a>GNSS 接口概述

GNSS 适配器和 GNSS 驱动程序之间的交互属于以下类别：

### <a name="capability-information-exchange"></a>功能信息交换

若要在 Windows 平台上支持可扩展性和 GNSS 堆栈的适应性，GNSS 适配器和 GNSS 驱动程序建立达成共识的基础 GNSS 堆栈，以及提供的支持的各种定义完善的功能Windows 平台。 功能方面也定义由 Microsoft 作为此 GNSS 接口定义的一部分，并将随 GNSS 空间中的多个创新会继续，市场中出现一组不同的芯片集/驱动程序。 GNSS 适配器时的初始化，或者根据需要在查询基础 GNSS 驱动程序/设备的各种功能，并相应地优化与 GNSS 驱动程序的交互。

完成 GNSS 适配器和 GNSS 驱动程序之间的功能的信息交换使用的控制代码[ **IOCTL\_GNSS\_发送\_平台\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_send_platform_capability)并[ **IOCTL\_GNSS\_获取\_设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_get_device_capability)。

### <a name="gnss-driver-command-and-configuration"></a>GNSS 的驱动程序命令和配置

GNSS 适配器可以执行一次性配置或 GNSS 驱动程序的定期重新配置。 同样 GNSS 适配器可能会执行某些特定于 GNSS 的命令通过驱动程序。 通过定义驱动程序和较高的级别的操作系统 (HLOS) 之间的一个命令执行协议来完成此操作。 具体取决于特定的命令类型，所需的操作可能立即或在系统重新启动后，才会生效。 GNSS 设备功能信息与类似，GNSS 命令也明确定义由 Microsoft 作为此 GNSS 接口定义的一部分，将继续不断发展，未来创新和因卡而异的 GNSS 设备驱动程序。

设备命令执行和配置都是使用控件的代码[ **IOCTL\_GNSS\_发送\_DRIVERCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_send_drivercommand)。

### <a name="position-information"></a>位置信息

这是基础 GNSS 设备的主要功能。 中的最基本形式 GNSS 适配器从 GNSS 驱动程序请求设备的当前位置。 此职位请求的变体包括 （但不限于） 以下定位会话类型：

-   设备 （单个单次触发修复） 的当前位置

-   连续定期流的修补程序 （基于时间的跟踪）

-   持续的基于移动阈值 （基于距离的跟踪） 的修补程序流

唯一的必填位置会话所需的每个 GNSS 硬件和 GNSS 驱动程序类型是一个镜头修复会话类型。 可以根据需要支持本机 （SOC 中、 GNSS 设备中并不在 GNSS 驱动程序或应用程序处理器中运行的服务的实现）、 基于时间的跟踪会话和距离基于跟踪会话。 这两种类型的本机跟踪会话的主要优势的潜在能源节约保持应用程序处理器 (AP) 处于休眠状态的更长的时间做更多 SOC 中处理和仅报告时所需的更改。 因为可以带来更高版本的节能和应用程序更广泛地使用，因此，支持本机距离基于跟踪的更多重大比本机基于时间的跟踪会话。

GNSS 驱动程序中检索位置信息的 act 都是通过修复，有状态的唯一会话中，包含以下操作：

1.  **启动修复会话：** GNSS 适配器启动启动修复会话 （由于 LBS 应用程序请求）。 GNSS 适配器设置的特定要求和首选项关联的请求和 intimates GNSS 驱动程序以启动引擎通过发出控制代码获取解决方法[ **IOCTL\_GNSS\_开始\_FIXSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_start_fixsession)。

2.  **获取设备位置 （修补程序数据）：** GNSS 适配器修复会话启动后，发出控制代码[ **IOCTL\_GNSS\_获取\_FIXDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_get_fixdata)开始等待来自驱动程序会提供修补程序。 当新的位置信息从引擎可用时，对此挂起 get 修复请求作出响应 GNSS 驱动程序。

    > [!NOTE]
    > 如果修复会话类型为 LKG 修补程序 （而非当前的修补程序），位置信息来自驱动程序的缓存。

    GNSS 适配器可确保始终可供 GNSS 驱动程序将修复数据可用时返回的异步 I/O 请求。 根据此修复程序，如果需要更多修补程序数据、 GNSS 适配器发出另一个 I/O 请求 （使用相同 IOCTL），此序列将继续，直到没有更多数据均可或修复会话将停止的性质。

3.  **修改修复会话：** 如果 GNSS 驱动程序不支持多路复用的相同类型的修复会话 GNSS 适配器可能发放[ **IOCTL\_GNSS\_修改\_FIXSESSION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_modify_fixsession)为这还会在其级别多路复用纠正会话类型。

4.  **停止修复会话：** GNSS 适配器发出停止修复会话属于特定修补程序会话任何进一步的位置信息是需要或预期的时。

### <a name="native-geofencing-support"></a>本机地理围栏的支持

GNSS DDI 支持卸载方案使用一系列 Ioctl 本规范中定义的地域隔离区。 为驱动程序，以指示这种支持定义了特殊功能标志，如果 GNSS 本机堆栈支持地理围栏，才必须设置此标志 （即它实现了地理围栏 GNSS 芯片中而不是在应用程序处理器）。 如果该驱动程序本身不支持地域隔离区，不应设置标志。 HLOS 已支持并非最佳的应用程序处理器 (AP)-基于地域隔离区跟踪引擎;尽管此解决方案不是为电源优化本机解决方案可以是因为，它是也经过测试且经过优化，因此它不应该用在 AP 中实现的等效解决方案。

> [!NOTE]
> 地域隔离区由 HLOS 跟踪需要应用程序处理器定期唤醒以检测地域隔离区违规，从而界定不受破坏的情况下，即使排出电源。 因此，此实现被视为可并非最佳。

HLOS 还使用跟踪作为故障转移机制无法跟踪由于低信号条件或其他暂时性错误，跟踪解决方案的本机地域隔离区从收到的错误通知的地域隔离区基础驱动程序时的基于亚太的地理围栏。
仅当地域隔离区跟踪是完全卸载到 SoC 和应用程序处理器仅用于处理与地域隔离区相关的事件被唤醒时，本机地理围栏支持是有益。 如果硬件不支持本机地域隔离区跟踪，GNSS 驱动程序必须不尝试在驱动程序层上实现。

GNSS 引擎还必须公开有案可稽的 IHV 特定优化参数，以便查找电源使用情况和用户体验之间的最佳平衡。 此外应支持的地域隔离区数超过**最小\_地域隔离区\_必需**标头文件中定义的值。 请注意，**最小\_地域隔离区\_必需**定义每个应用程序，为一个应用程序并不知道的其他应用程序或移动运营商使用地域隔离区数。

卸载支持地理围栏的过程包括以下要求：

-   HLOS 应能够创建一个或多个地域隔离区通过 DDI 并且驱动程序将其发送到硬件，若要开始跟踪它们。

-   HLOS 应不能删除一个或详细信息之前创建通过 DDI 的地域隔离区和驱动程序将其发送到停止跟踪它们的硬件。

-   理想情况下，GNSS 硬件应了解跟踪的每个地域隔离区状态的初始地域隔离区，而且在此初始状态下使用它仅报告更改。 如果 GNSS 硬件不支持此功能，则它会向 HLOS 报告的初始状态，每次创建地域隔离区。

-   GNSS 硬件跟踪设备的当前位置 power 高效的方式并唤醒 AP，只要设备具有输入和/或退出跟踪地域隔离区。 GNSS 驱动程序将传递给 HLOS 的地域隔离区警报。

-   在低卫星信号和其他暂时性错误条件下，可能无法可靠地跟踪现有地域隔离区 GNSS 引擎。 GNSS 引擎应能够检测到跟踪中断并且 GNSS 驱动程序应传递跟踪到 HLOS 状态错误警报。 HLOS 切换到默认基于亚太的地域隔离区跟踪直到 GNSS 硬件能够恢复并重新跟踪地域隔离区。

-   实现将 IHV 特定而异 GNSS 引擎需要提供的通知，以指示不能跟踪的地域隔离区的具体条件。 以下是实现的一些准则：

    -   如果 GNSS 引擎能够检测到的用户不动并确保有没有地域隔离区边界 25 以米为单位的高信任度或较少，则不需要发送跟踪错误 GNSS 引擎。

    -   如果 GNSS 引擎，能够检测到的用户不移动，但有 25 以米为单位是地域隔离区边界的高信任度或较少 GNSS 引擎将需要在一分钟内发送跟踪错误。

    -   如果 GNSS 引擎具有已检测的用户将移动，并且没有 GNSS 引擎需要发送跟踪错误，一分钟内或更少小于或等于 100 米的地域隔离区边界。

    -   如果无法确定用户是否移动，并没有 100 米的地域隔离区边界或更少，GNSS 引擎，GNSS 引擎将需要一分钟内或更少发送跟踪错误。

    -   如果正在检测用户将移动 GNSS 引擎，GNSS 引擎需要将发送跟踪错误的时间成正比的移动和距离的估计速度到最接近的地域隔离区。 一条建议是将错误消息中的发送\[(Distance-to-closest-fence-boundary(m) / 预计速度 (m/s))-15 秒\]。 GNSS 引擎可能会使用移动检测指标来确定应在其中发送跟踪错误的时间。

    -   如果无法确定用户正在 GNSS 引擎，GNSS 引擎需要将发送跟踪错误的时间成正比的移动和距离的高速度到最接近的地域隔离区。 一条建议是将错误消息中的发送\[Distance-to-closest-fence-boundary(m) / 343(m/s)\]。

-   GNSS 引擎报告地域隔离区跟踪状态错误期间，应该没有地域隔离区发送到 HLOS 的违规事件。

-   HLOS 可以重置的地域隔离区删除以前创建的所有地域隔离区通过单个命令的跟踪。

-   移动的起源于地域隔离区不会在重新启动或驱动程序重启后保留 GNSS 硬件或驱动程序中。 HLOS 处理持久性代表最终用户应用程序，并创建/删除操作所需的地域隔离区。

GNSS 适配器和以本机方式支持卸载在地域隔离区跟踪失败的情况下的地理围栏的 GNSS 引擎之间的交互方面 GNSS 适配器将按如下所示执行操作：

-   它将使用 AP 基于跟踪后 GNSS 驱动程序将返回失败以跟踪。

-   它将继续推送这些表中当前未跟踪在 OS 级别到驱动程序也因此同步地域隔离区 （添加/删除） 的任何更新。这将帮助 GNSS 引擎知道哪些地域隔离区当前未跟踪由操作系统，并且它可以使可跟踪/无法跟踪确定基于新数据。

-   它会将推送地域隔离区状态更改后 GNSS 驱动程序发回成功的功能，跟踪由 AP 基于跟踪器。

### <a name="driver-notifications-for-assistance-and-helper-data"></a>帮助和帮助程序数据的驱动程序通知

有时，GNSS 驱动程序可能需要从 GNSS 适配器协助帮助程序或数据操作。 这包括各种形式的 AGNSS 数据 （时间注入，ephemeris，初始粗略的位置）、 用户同意的情况下弹出窗口，以支持网络发起的用户平面定位，依次类推。

-   无法通过 GNSS 驱动程序来获取 GNSS 协助数据，而无需使用 GNSS 适配器。 但是建议使用 GNSS 适配器和利用定位服务有几个原因 Microsoft 获取帮助数据：

    -   Microsoft 当前位置堆栈将负责建立数据连接和遵守漫游的任何约束，数据首选项，网络安静模式下集成等。

    -   定位服务 Microsoft 可以定期获取特定于通过服务器到服务器后端连接 IHV 协助数据并将其提供到所有设备的需要保存 IHV 需要部署在世界各地的前端协助服务的满足可用性、 可伸缩性和响应能力的要求。

-   用户授予许可后，为应用程序所拥有的操作系统的收件箱的隐私。 因此任何 UI，以通知有关网络启动的位置请求用户或任何 UI，以请求同意的情况下用户响应到网络中发起位置请求，将由 Microsoft 拥有。 GNSS 驱动程序会通知收到 GNSS 适配器网络启动位置请求时，如果需要它将等待来自用户继续操作之前的默认时间到满足请求的响应。

GNSS 适配器主动寻求 GNSS 驱动程序中的此类请求，从而始终将一个或多个待 Irp 执行 GNSS 驱动程序不能启动请求以在其自己的上层，因为可以完成这种类型的操作，以便 GNSS 灾难恢复iver 可以重新打开此类挂起的请求响应。 接收的请求协助/帮助程序日期时，GNSS 适配器提取数据 （或执行特定操作代表 GNSS 驱动程序），并随后注入到 GNSS 驱动程序通过另一个所需的信息**DeviceIoControl**调用。

从驱动程序的通知处理通过常见的事件模型。 例如，对于 GNSS 协助 GNSS 适配器使用控制代码[ **IOCTL\_GNSS\_侦听\_AGNSS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_agnss) GNSS 驱动程序从接收 AGNSS 请求。 GNSS 适配器随后提取 AGNSS 协助数据和问题[ **IOCTL\_GNSS\_插入\_AGNSS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_inject_agnss)若要将数据推送到 GNSS 驱动程序。

该通知机制还用于接收与地域隔离区相关的警报数据和状态更新。 适配器使用的控制代码[ **IOCTL\_GNSS\_侦听\_地域隔离区\_警报**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_geofence_alert)用于接收单个地域隔离区警报和[ **IOCTL\_GNSS\_侦听\_地域隔离区\_TRACKINGSTATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_geofences_trackingstatus)用于跟踪的地域隔离区的总体状态中接收的更改。

### <a name="gnss-driver-logging"></a>GNSS 驱动程序日志记录

出于诊断目的，GNSS 驱动程序应记录错误和使用规定的日志记录机制 (WPP) 如下所述的 Microsoft 或 ETW 其他诊断信息。 建议的驱动程序用于 WPP 进行日志记录目的而不是 etw 的更多信息，虽然支持这两种机制。 WPP 所建议的原因是工具，可帮助调试驱动程序的可用性。

驱动程序必须不记录任何信息，用户可读或为其他比通过此规定日志记录技术。 有关详细信息，请参阅[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)。

使用 WPP 软件跟踪日志记录消息将类似于使用 Windows 事件日志记录服务。 该驱动程序日志文件中记录消息 ID 和未格式化的二进制数据。 随后，后处理器将日志文件中的信息转换为可读的形式。 但是，WPP 软件跟踪支持更多的能力和灵活性大于所支持的事件日志记录服务的消息格式。 例如，WPP 软件跟踪提供 IP 地址、 Guid、 system Id、 时间戳和其他有用的数据类型的内置的支持。 此外，用户可以添加到其应用程序相关的自定义数据类型。

### <a name="mobile-operator-protocol-support"></a>移动运营商协议支持

IHV 提供 GNSS 堆栈 （GNSS 驱动程序、 GNSS 设备/引擎） 是支持各种移动运营商定位协议 （SUPL、 UPL、 CP，等）。 如果不做意味着设备不会接受传递从移动运营商，并将极大地限制可以在其中 commercialized 设备。

> [!NOTE]
> 对这些协议和移动运营商要求的符合性的支持是强制性的某些移动运营商提供设备要求。 移动运营商协议的支持可能不是必需的大多数非 phone 平台，特别是如果平台不包括移动宽带 (MBB) 支持。

所有实现部分都抽象化 IHV 堆栈中和 Microsoft HLOS 组件是不可知的：
-   协议 （例如，协议的工作原理、 协议消息和等等的解释） 特定的实现详细信息。

-   实现堆栈的形状 (例如，实现可以位于 GNSS 设备/引擎或 GNSS 驱动程序，或如果需要一个单独的 HLOS 服务)。

-   实现协议的自有 IHV GNSS 堆栈内的各个组件之间的交互。 例如，如果 GNSS 驱动程序用于响应特定的 SUPL 协议消息，则可通过采用要求的 Wi-fi 扫描结果则用户模式下扩展将注入到通过专用 IOCTL 调用，该驱动程序的 Wi-fi 扫描结果或使这部分 UMDF 2.0 驱动器r，或处理数据在较低级别交互。 Microsoft GNSS HLOS 组件是不在意 IHV GNSS 堆栈组件之间的这种交互。

总之，IHV 或 OEM 需要提供 SUPL 客户端 （和可能 UPL 客户端系统是否要在中国寄送） 并将其集成使用/GNSS 驱动程序中。 GNSS DDI 中将完成与 SUPL 客户端的位置平台的所有交互操作。

为了促进移动运营商协议的实现，减少使用平台特定技术的软件开发的负担，GNSS 适配器提供了到 IHV GNSS 堆栈的特定功能。 GNSS 驱动程序被视为中介从 HLOS 组件接收此类功能，仅与 GNSS 驱动程序和不能与任何其他部分 IHV GNSS 堆栈 GNSS 适配器交互，例如。 GNSS 驱动程序 Ioctl 定义的语法和语义 GNSS 驱动程序和 GNSS 适配器之间的这种功能。 GNSS 驱动程序是负责将路由到特定 IHV 组件实现移动运营商协议。 广泛地说，GNSS 适配器提供了到 GNSS 驱动程序的以下功能：

1.  **配置：** 移动运营商预配设备并更改配置使用 OMA 协议标准所规定的配置机制。 例如，SUPL 标准要求 SUPL 配置以进行基于 UICC 和/或执行使用 SUPL OMA 配置配置文件信息获取通过 OMA DM 或 OMA CP。

    > [!NOTE]
    > 直到 Windows 10 手机出于配置目的 （OMA DM 和 OMA CP） 中提供某些功能不可用在其他平台中。 从 Windows 10 开始所有平台可支持 SUPL 配置通过 SUPL 配置服务提供商 (CSP)，新 as far as GNSS DDI 使用。 通过 CSP 注入预配可以来自图像本身 （通过 provxml 或 multivariant） 或从移动运营商通过 OMA DM 或 OMA CP。

    Windows 10 定义专有技术，设备管理配置服务提供商 (CSP)，用于解释和提取的配置数据。 Microsoft 提供，使用 OMA 配置并将配置推送到通过 GNSS 适配器 GNSS 驱动程序的 CSP。

    > [!NOTE]
    > 或者，IHV 还可以编写用户模式组件便可以使用移动运营商配置规范使用特定于手机的设备管理技术 (Csp)。 但是，这将为其他 IHV 负担，并且不建议这样做。

    在系统中，在双 SIM 设备的情况下包括支持只有一个 SUPL 配置。 Microsoft 提供的功能来重新配置 SUPL 基于 UICC 和 UICC 更改。 除此之外，如果设备漫游 HLOS 重新配置 SUPL 客户端在独立模式下工作。 本文档定义了用于将各种移动操作协议此类配置数据推送 Ioctl (SUPL 1.0 和 2.0，v2UPL，等等)。

2.  **用户同意 UI:** 若要满足的隐私要求，某些网络启动定位请求需要用户同意。 Ihv 不能为平台组件编写 UI。 因此 GNSS 适配器处理用于代表 GNSS 驱动程序的用户同意的用户界面。 在定义 GNSS 驱动程序通知 Ioctl，以请求 UI 弹出窗口中和 GNSS 适配器来传达用户对此类请求的响应 Ioctl [GNSS 驱动程序 Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver)。

为了实现 IHV 堆栈将需要一个完全正常运行 SUPL 客户端使用的接口或/通过 OS 平台中提供的常规功能。 以下是功能的 Ihv 可以利用以实现其 SUPL 客户端的 Windows 10 中提供的列表：

> [!NOTE]
>  无此功能是位置平台或 GNSS DDI 的一部分，但将包括此处获取问题的以帮助 GNSS 驱动程序开发人员理解什么可以利用从操作系统来实现 SUPL 功能。

![SUPL GNSS 驱动程序的客户端交互](images/gnss-architecture-6.png)

-   **SMS 路由器：** SMS 路由器允许 SUPL 客户端订阅执行 SUPL NI 请求的 WAP 推送的 SIP 推送消息。

-   **若要请求此类连接，应为 SUPL 和 Api 使用连接管理器能够配置哪种连接：** 移动运营商可能需要在专用连接，或只需在不同于默认的 Internet 连接的连接上有 SUPL 流量。 若要执行此操作，**连接管理器**提供：

    -   为了 SUPL 通信都应使用的配置服务提供程序的 OEM 或移动运营商可以使用配置的连接。

    -   用于查询 SUPL 连接的连接参数 SUPL 客户端的 API。

    -   一个 API，用于建立 SUPL 连接，与上一步中获取的参数。

-   **移动电话网络连接配置：** 若要配置不同的移动电话网络连接，例如 SUPL 连接的参数的参数没有 OEM 或移动运营商可以使用配置服务提供程序。 然后可以在关联此连接**连接管理器**SUPL 目的。

-   **请求在 SUPL 连接处于正在进行时保持连接处于活动状态：** SUPL 客户端可能需要连接时在这些系统是在备用启动与 HSLP 的连接。 这可能是因为 GNSS 设备需要配置为使用基于 Microsoft 的定位，或者因为移动运营商发送了 NI 请求获取帮助的信息。 如果出现这种情况 SUPL 客户端将需要与 HSLP 建立连接，并确保连接处于活动状态，直到完成 SUPL 会话。

-   **与移动宽带 (MBB) 模块之间的交互：** 在 Windows 10 中，没有 Api 可通过 HLOS 检索移动电话网络测量，知道何时已放置的紧急的调用，等等。 需要通过直接与 MBB 集成来完成与 MBB 进行任何交互 (通过 AT 命令或其他专有方法)。

### <a name="manufacturing-testing"></a>生产测试

Oem 需要有办法在制造时进行验证，而且还在客户支持 GNSS 硬件和 GNSS 堆栈 （GNSS 驱动程序和 GNSS 设备/引擎） 正常工作的点。 IHV 可以提供专有机制使 Oem 可以进行此测试，也可以选择实现接口中 DDI 启用 OEM 来启动生产测试并获取结果。

位置 framework 会被绕过进行生产测试时测试的一大工作重点是在硬件验证或驱动程序验证。 一般情况下，设备将在一个特殊的"安全操作系统模式"加载组件和服务的最小集的位置。 在此模式下，OEM 可以启动一组将触发测试用例的测试应用程序。 出于效率和在制造过程的速度，它是强烈要求具有不同的组件中的测试的并发支持。

测试某一生产的界面包括两种类型的测试：

1.  **运营商批测试：** 此测试是验证外部连接/天线测试。 在此测试 GNSS 引擎必须搜索 CW 信号，并提供响应中的 SNRs （信号到干扰比率） 或干扰定量供应运营商度量值。 理想情况下测试应提供 10 Hz 时返回的响应。

2.  **自我测试：** 此测试是验证 GNSS 引擎的基本功能。 自我测试应能够检测到的一些基本问题中引擎 （有故障的硬件，而无需任何外部信号注入 GNSS 硬件中的连接错误。 此验证的目标是执行此成本低廉的测试，并进行了更详尽且成本高昂的测试设备进入前将其用作生产订单行中中的入口。 在此测试 GNSS 引擎和驱动程序应执行自我验证 pin 连接操作，返回状态代码指示所有内容是确定，或出现故障。 失败的错误代码必须指示检测到错误。 由 IHV 设置错误代码。

## <a name="io-considerations"></a>I/O 注意事项


GNSS 功能不会不映射到传统的文件读取和写入请求发送到设备驱动程序，因为**ReadFile**并**WriteFile**函数将不用于 GNSS 驱动程序 Api。 所有将也使用实现 GNSS 功能定义 GNSS 特定于设备 I/O 控制 (**DeviceIoControl**) 请求，也称为 Ioctl。

所有 Ioctl 将都使用方法\_缓冲作为输入和输出数据的数据传输机制。 由于 GNSS 相关数据的大小是相对较小，因此额外的缓冲副本不应影响系统性能。

GNSS 驱动程序将使用打开**文件\_标志\_OVERLAPPED**选项**CreateFile**函数。 因此所有 Ioctl 都是隐式异步的。 但是，大部分 GNSS Ioctl 是 （例如，以异步方式返回预期的驱动程序和结果中的某个活动 IOCTL 触发器） 在语义上是异步的尽管某些 Ioctl 是在语义上有无逻辑意义上同步异步操作或活动所涉及的这种 Ioctl。 以下几个 Ioctl 的同步行为将通过只需发出后锁定 GNSS 适配器线程**DeviceIoControl** I/O 操作完成之前调用。 因此，它是 GNSS 驱动程序始终作为处理所有 Ioctl 的一部分完成 IRP 的责任。 GNSS 适配器应只需遵循的约定的同步调用和发生错误时可能会或可能不会重新尝试这些命令。 IHV 驱动程序需要确保它返回错误前结合了驱动程序端上的所有逻辑。

对于请求和响应操作，GNSS 适配器将始终保留挂起的 I/O 操作，以便当 GNSS 驱动程序具有要作为对以前调用的操作的响应发送数据时，可以通过挂起 IRP 发送响应。

## <a name="single-shot-session"></a>单个单次触发的会话


向驱动程序一次单次触发修复启动修复请求包括准确性和响应时间值。 GNSS 引擎可使用这些值来了解应用程序请求的意向并做出明智的决策。 驱动程序收到请求后它应开始返回引擎生成的任何中间修补程序。 中间的修补程序是在计算其满足准确性要求，或者是最终的修补程序时由引擎生成的修补程序。 这些中间的修补程序的频率不强制实施，是该引擎的实现细节。 GNSS 适配器需要的修补程序会每隔几秒，并且它们不能是最后一个中间修复。

一旦 GNSS 引擎确定它不能获取当前的信号条件它应返回最终的修补程序，应停止执行任何进一步的计算下一个更好地修复。 最终的修补程序符合准确性要求，或指示引擎不能提高当前条件下提供的准确性。

GNSS 适配器发出的单个快照会话中是两种情况下停止修补程序：

-   它会从驱动程序获取最终的修补程序。

-   已达到请求的响应时间。 此处的最后一个中间修复将发送到应用程序。

下图说明了两个单个单次触发的会话：

![显示中间的关系图修补程序的两个会话](images/gnss-architecture-7.png)

**会话 1:** 该驱动程序提供的准确性和响应时间参数。 启动修复命令之后, 该驱动程序开始发送中间的修补程序。 一段时间后不确定它无法返回一个更准确的修复，以便指示为最终状态的最后一个修复。 响应时间限制已到达之前，将发生这种情况。 适配器发送到应用程序的最终解决方法，并发出停止修复命令。

**会话 2:** 相同，如上面的会话 1 中所示，但在此情况下，该引擎保留将提供更好的修补程序，以满足要求，准确性和保留发送中间修复之间。 达到会话响应时间限制时，适配器发出停止修复这应关闭此会话中的驱动程序。 收到的最后一个中间修复已发送到应用程序。

若要实现一个镜头的支持时，请考虑的重要的设计方面之一是，如果基于距离的跟踪会话和基于时间的跟踪会话都不受支持，GNSS 引擎应继续跟踪后的 3 到 5 秒的附属项收到停止修复命令。 这是因为 GNSS 适配器需要实现模拟基于距离的跟踪会话和/或快照的基于时间的跟踪会话使用单个修复会话，并且如果 GNSS 引擎停止立即跟踪附属项，大多数 GNSS 设备都将有这使得不可能获取延迟实现满足需求的导航的模拟的跟踪会话，运行跟踪，或将应用程序映射。

GNSS 适配器可能会启动请求的单个快照的修补程序，系统在连接待机时，不只是当系统处于活动状态。 这可能是为满足需要的后台任务、 系统服务、 地域隔离区中的应用程序处理器或其他情况下的跟踪。 GNSS 驱动程序应能够将这些会话请求传递到 GNSS 设备并且可以满足请求或向 GNSS 适配器提供了错误。

下面的序列图说明了与获取独立 GNSS 修复相关的高级操作。 请注意这不包括协助数据的任何请求。

![gnss 体系结构的顺序关系图 ](images/gnss-architecture-8.png)

序列描述如下所示：

1.  GNSS 适配器打开 GNSS 驱动程序使用**CreateFile** API。 WDF/KMDF/UMDF 向 GNSS 驱动程序所需的可选回调。 返回的文件句柄用于所有后续操作。

2.  GNSS 适配器发出 IOCTL 通信对驱动程序的各种平台功能。 GNSS 驱动程序完成 I/O 操作。

3.  GNSS 适配器问题 IOCTL 用于获取设备功能。 GNSS 驱动程序返回的设备功能，并完成 I/O 操作。

4.  GNSS 适配器发出 Ioctl 为任何特定于驱动程序的配置或命令。 GNSS 驱动程序执行所需的操作，并完成 I/O 操作。

5.  GNSS 适配器问题[ **IOCTL\_GNSS\_启动\_FIXSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_start_fixsession)，以及指定的类型和其他方面的解决方法的参数。 在收到此 IOCTL，GNSS 驱动程序与基础设备开始接收修补程序进行交互，并随后完成 I/O 操作。

6.  GNSS 适配器问题[ **IOCTL\_GNSS\_获取\_FIXDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_get_fixdata)并等待 I/O 完成。 每当 GNSS 驱动程序具有中间的可用修补程序，它通过完成 I/O 操作返回的数据。

7.  直到 GNSS 驱动程序指示没有更多修补程序是预期 （最后一个修复收到） 重复步骤 6。

8.  GNSS 适配器问题[ **IOCTL\_GNSS\_停止\_FIXSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_stop_fixsession)。 GNSS 驱动程序执行与原始的修补程序请求关联的所需的清除操作。

9.  GNSS 适配器关闭驱动程序文件句柄使用**CloseHandle** API。

中详细描述了 GNSS Ioctl 和关联的数据结构[GNSS 驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/)。

## <a name="distance-based-tracking-session"></a>基于距离的跟踪会话


基于距离的跟踪会话的最终用户应用程序，因为从历史上看，它是.NET Api 中提供的唯一会话类型经常使用。 距离值 0 指示 GNSS 引擎应会提供修补程序在可能的最高费率。

GNSS 适配器仅在更高版本，则指示它能够将启动跟踪会话使用 GNSS 驱动程序，距离**SupportDistanceTracking**。

对跟踪会话的距离的驱动程序的启动修复，请求将包括所需的水平准确性和移动阈值，它是半正矢距离 GNSS 之前应涵盖系统以米为单位的驱动程序提供位置更新。 GNSS 引擎可以使用这些值来了解应用程序请求的意向并做出明智的决策，例如调整要检查的位置的频率。

启动修复请求收到由驱动程序后它应开始返回引擎生成的直到获取最后一个修复任何中间修补程序。 这将被视为该会话的第一个位置。 完成此操作后 GNSS 引擎应开始提供的修补程序，只要它检测到已大约提及的半正矢距离。

如果 GNSS 引擎决定，它不能跟踪过更长的位置 （例如，如果附属项不可见过更长） 的设备，它将返回错误到 GNSS 适配器，使位置平台可以故障回复到其他机制来提供对最终用户应用程序的位置更新。 GNSS 适配器应在以下时间内提供错误：

\[(Distance-remaining-since-last-known-position (m) / 预计速度 (m/s)) – 5 秒\]或 5 秒，两者中较大。

如果 GNSS 引擎提供给 GNSS 适配器错误但 GNSS 适配器未停止跟踪会话，GNSS 引擎应继续，如果签入电源优化的方式，它可以继续跟踪的位置。 IHV 可以使用优化以使此检测在低功耗。 用于优化的常见技术包括：

-   渐进后退

-   等待的成本较低的信号，表明设备移动以重新检查

-   低能耗检查附属信号

GNSS 引擎能够提供最终修复后的错误条件后，它应指示跟踪成功恢复到 GNSS 适配器发送该位置。

如果请求的跟踪会话已取消请求或新的应用程序正在请求距离的一个或多个应用程序基于跟踪会话，GNSS 适配器距离基于跟踪会话发出修改修复命令。 在此情况下 GNSS 适配器计算所必需进行多路复用不同的活动会话的新的聚合的会话参数，并使用这些参数更新 GNSS 驱动程序。

如果将 GNSS 适配器基于距离的跟踪会话发出停止修复命令：

-   跟踪会话移交到另一个系统中提供的定位引擎。

-   应用程序的请求跟踪会话已取消请求。

下图说明了两个距离基于跟踪会话：

![gnss 驱动程序的内部跟踪 ](images/gnss-architecture-9.png)

**会话 1:** GNSS 驱动程序提供准确性和移动阈值参数启动跟踪会话时。 开始修复命令后, 驱动程序开始发送中间的修补程序，直到它获得最终的修补程序或符合准确性要求此时 GNSS 适配器和 GNSS 引擎提供此类修补程序的修补程序将启动距离跟踪过程。 在会话处于活动状态，而 GNSS 适配器发送请求以修改会话参数有时 T1 和 T2。 每个修改参数后 GNSS 驱动程序会将修补程序更新发送到 GNSS 适配器，并且将恢复跟踪会话使用新参数，直到 GNSS 适配器发送停止修复命令的距离。

**会话 2:** 会话启动进程类似于会话 1 更高版本，但在给定时刻 GNSS 引擎是无法跟踪位置。 之后的时间是依赖于的距离和估计的速度移动，GNSS 驱动程序将发送一个错误。 GNSS 引擎继续检查在较低功率以及它会恢复时可以恢复，它指示这样 GNSS 适配器由发送新的修补程序。 根据需要 GNSS 适配器将发送停止修复命令之前，将使用新的修补程序更新会话。

GNSS 适配器可能会保持处于活动状态，或甚至启动距离基于跟踪会话时系统不处于已连接待机状态，仅当系统处于活动状态。 这可能是为满足需要的后台任务、 系统服务、 地域隔离区中的应用程序处理器或其他情况下的跟踪。 GNSS 驱动程序应能够将这些会话请求传递到 GNSS 设备并且可以满足请求或向 GNSS 适配器提供了错误。

## <a name="time-based-tracking-session"></a>基于时间的跟踪会话


由应用程序需要频繁和常规位置更新来刷新用户界面 （例如，映射、 导航应用程序等），可以使用基于时间的跟踪会话。

GNSS 适配器将基于时间的跟踪会话使用 GNSS 驱动程序启动，仅在更高版本，则指示它能够**SupportContinuousTracking**。

对基于时间的跟踪会话的驱动程序的启动修复请求将包括所需的水平准确性和首选的时间间隔的 GNSS 驱动程序应提供位置更新。 GNSS 引擎可使用这些值来了解应用程序请求的意向并做出明智的决策，例如调整要检查的位置，开始获取几秒钟的时间间隔之前提供的附属项的频率定位更新，及时，依此类推。

启动修复请求收到由驱动程序后它应开始返回引擎生成的直到获取最后一个修复任何中间修补程序。 这将被视为该会话的第一个位置。 完成此操作后 GNSS 引擎应开始提供修补程序在会话参数所需的时间间隔。 如果 GNSS 引擎不能提供所需的应用程序的频率的位置，它应只需提供它可以最大速率的修补程序。

如果 GNSS 引擎决定，它不能跟踪过更长 （例如，如果附属项将不再可见） 设备的位置，它将返回错误到 GNSS 适配器，使位置平台可以故障回复到其他机制来提供位置最终用户应用程序的更新。

如果 GNSS 引擎提供给 GNSS 适配器错误但 GNSS 适配器未停止跟踪会话，GNSS 引擎应继续，如果签入电源优化的方式，它可以继续跟踪的位置。

IHV 可以使用优化使此检测在低功耗上, 一节中所述。 GNSS 引擎能够提供最终修复后的错误条件后，它应指示跟踪成功恢复到 GNSS 适配器发送该位置。

GNSS 适配器修改修复命令发出基于时间的跟踪会话，如果一个或多个应用程序的请求跟踪会话已取消请求或新的应用程序正在请求基于时间的跟踪会话。 在此情况下 GNSS 适配器计算所必需进行多路复用不同的活动会话的新的聚合的会话参数，并使用这些参数更新 GNSS 驱动程序。

如果将 GNSS 适配器基于时间的跟踪会话发出停止修复命令：

-   跟踪会话移交到另一个系统中提供的定位引擎。

-   应用程序的请求跟踪会话已取消请求。

下图说明了两个基于时间的跟踪会话。

![基于时间的跟踪关系图了解 gnss 驱动程序修补程序](images/gnss-architecture-10.png)

**会话 1:** GNSS 驱动程序提供准确性和首选时间间隔参数启动跟踪会话时。 该驱动程序应开始发送中间开始修复命令修复直到它获取最终的修补程序或符合在准确性要求的修补程序后什么时候，此类修补程序提供给 GNSS 适配器并 GNSS 引擎将启动基于时间的跟踪过程。 在会话处于活动状态，而 GNSS 适配器发送请求以修改会话参数有时 T1 和 T2。 参数 GNSS 每次修改后驱动程序会将修补程序更新发送到 GNSS 适配器，将继续基于时间的跟踪会话，使用新参数，直到 GNSS 适配器发送停止修复命令。

**会话 2:** 会话启动进程类似于在会话 1 中更高版本，但在给定时刻 GNSS 引擎停止能够跟踪位置。 GNSS 引擎无法提供 15 秒的会话参数所需的时间间隔内的修补程序时，GNSS 驱动程序将发送一个错误。 GNSS 引擎继续检查在较低功率以及它会恢复时可以恢复，它指示这样 GNSS 适配器由发送新的修补程序。 根据需要 GNSS 适配器将发送停止修复命令之前，将使用新的修补程序更新会话。

GNSS 适配器可能会保持处于活动状态，或甚至启动基于时间跟踪会话时系统不处于已连接待机状态，仅当系统处于活动状态。 这可能是为满足需要的后台任务、 系统服务、 地域隔离区中的应用程序处理器或其他情况下的跟踪。 GNSS 驱动程序应能够将这些会话请求传递到 GNSS 设备并且可以满足请求或向 GNSS 适配器提供了错误。

## <a name="handle-different-types-of-fix-session-simultaneously"></a>同时处理不同类型的修复会话


某些高级的 GNSS 引擎可能能够同时处理一个镜头会话，使用基于距离的和/或基于时间的跟踪会话。 理想情况下独立会话应不相互影响，但这可能不是始终有可能，专门在同时进行的单个快照和时间基于跟踪会话的情况下。 本部分提供一些指导原则的 IHV 实现，以防折中方案不需要进行以处理不同类型的同时会话。

在本部分中使用以下首字母缩写词：

-   **SS:** 单个单次触发的会话

-   **DBT:** 距离基于跟踪会话

-   **TBT**:时间基于跟踪会话

-   **TBF:** 修补程序之间的时间

下表提供了某些情况下同时处理一个镜头和基于时间的跟踪会话：

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>案例</th>
<th>SS 活动？</th>
<th>TBT 活动？</th>
<th>案例详细信息</th>
<th>可接受的时间间隔的修补程序</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>案例 1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS 会话正在进行时 TBT 定期会话的开始使用剩余超时&gt;= 间隔</p></td>
<td><p>TBT 间隔相同</p></td>
<td><p>SS 会话行为：</p>
<ul>
<li><p>在超时之前发送中间和最后一个修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul>
<p>TBT 会话行为：</p>
<ul>
<li><p>发送中间和最后一个修补程序。</p></li>
<li><p>接收到大约根据时间间隔的修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>情况 2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS 会话正在进行时 TBT 定期会话的开始使用剩余超时&lt;间隔</p></td>
<td><p>间隔保持不变，则为 SS 超时，直到满足 SS 会话。</p>
<p>然后更新间隔以 TBT 间隔相同</p></td>
<td><p>SS 会话行为：</p>
<ul>
<li><p>在超时之前发送中间和最后一个修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul>
<p>TBT 会话行为：</p>
<ul>
<li><p>发送中间和最后一个修补程序</p></li>
<li><p>修补程序接收到大约根据时间间隔，但可能是更频繁，而提供 SS 会话。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>案例 3</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS 会话开始时正在进行的 TBT 定期会话启动具有超时设置&gt;= 间隔</p></td>
<td><p>TBT 间隔相同</p></td>
<td><p>SS 会话行为：</p>
<ul>
<li><p>在超时之前发送中间和最后一个修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul>
<p>TBT 会话行为：</p>
<ul>
<li><p>发送中间和最后一个修补程序</p></li>
<li><p>接收到大约根据时间间隔的修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>用例 4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS 会话开始时正在进行的 TBT 定期会话启动具有超时设置&lt;间隔</p></td>
<td><p>间隔更改为相同 SS 超时，直到满足 SS 会话。 然后可以更新间隔以 TBT 间隔相同。</p></td>
<td><p>SS 会话行为：</p>
<ul>
<li><p>在超时之前发送中间和最后一个修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul>
<p>TBT 会话行为：</p>
<ul>
<li><p>发送中间和最后一个修补程序。</p></li>
<li><p>修补程序接收到大约根据时间间隔，但可能是更频繁，而提供 SS 会话。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>用例 5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>使用修改的间隔启动 TBT 定期会话</p></td>
<td><p>使用调制解调器的会话将更新为新的时间间隔为 TBT 间隔相同。 如果需要调制解调器会话将重启。</p></td>
<td><p>SS 会话行为：</p>
<ul>
<li><p>不适用</p></li>
</ul>
<p>TBT 会话行为：</p>
<ul>
<li><p>发送中间和最后一个修补程序。</p></li>
<li><p>接收到大约根据时间间隔的修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>用例 6</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS 会话正在进行时正在进行的 TBT 定期会话接收的时间间隔，使用剩余超时值更改时所在&gt;= 间隔</p></td>
<td><p>TBT 间隔相同</p></td>
<td><p>SS 会话行为：</p>
<ul>
<li><p>在超时之前发送中间和最后一个修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul>
<p>TBT 会话行为：</p>
<ul>
<li><p>发送中间和最后一个修补程序</p></li>
<li><p>接收到大约根据时间间隔的修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>用例 7</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>SS 会话正在进行时正在进行的 TBT 定期会话接收的时间间隔，使用剩余超时值更改时所在&lt;间隔</p></td>
<td><p>间隔更改为满足 SS 会话前所剩余的超时值，SS 相同。 然后可以更新间隔以 TBT 间隔相同。</p></td>
<td><p>SS 会话行为：</p>
<ul>
<li><p>在超时之前发送中间和最后一个修补程序。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul>
<p>TBT 会话行为：</p>
<ul>
<li><p>发送中间和最后一个修补程序</p></li>
<li><p>修补程序接收到大约根据时间间隔，但可能是更频繁，而提供 SS 会话。</p></li>
<li><p>收到停止后立即关闭会话。</p></li>
</ul></td>
</tr>
</tbody>
</table>



如果同时有基于时间和距离基于跟踪会话，则可以设置 GNSS 引擎准确性跟踪要使用的两个最小值。 准确性有同时一个镜头和跟踪会话时所需的不同值的情况下下, 表还提供一些指导原则：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>案例</th>
<th>SS 准确性</th>
<th>DBT 或 TBT 准确性</th>
<th>总体 GNSS 引擎准确性</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>案例 1</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p>不适用</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p><strong>SS 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取高准确性结果。 中间的修补程序提供给 HLOS 可用。</p></td>
</tr>
<tr class="even">
<td><p>情况 2</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p>不适用</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p><strong>SS 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取中/低准确性结果。 如果满足要求的修补程序已可用，则这返回作为最终的修补程序。 否则，中间的修补程序提供给 HLOS 可用。</p></td>
</tr>
<tr class="odd">
<td><p>案例 3</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p>高</p></td>
<td><p>高</p></td>
<td><p><strong>SS 会话行为：</strong>考虑到高精度会话已存在 DBT 或 TBT 会话，SS 会话只需中间进一步向提供修补程序 HLOS 直到获取所需的最终精度或获得最终的修补程序。</p></td>
</tr>
<tr class="even">
<td><p>用例 4</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p>高</p></td>
<td><p>高</p></td>
<td><p><strong>SS 会话行为：</strong>考虑到高精度会话已存在 DBT 或 TBT 会话，SS 会话只需中间进一步向提供修补程序 HLOS 直到获取所需的最终精度或获得最终的修补程序。</p></td>
</tr>
<tr class="odd">
<td><p>用例 5</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p>中/低</p></td>
<td><p>中/低-&gt;高然后返回到中/低 SS 会话完成后</p></td>
<td><p><strong>SS 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取高准确性结果。 中间的修补程序提供给 HLOS 可用。</p>
<p><strong>DBT 或 TBT 会话行为：</strong>它是对此会话的确定以暂时接收高准确性结果。 但是，SS 会话提供服务后，此会话的准确性应返回到中/低。</p></td>
</tr>
<tr class="even">
<td><p>用例 6</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p>中/低</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p><strong>SS 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取中/低准确性结果。 如果满足要求的修补程序已可用，则这返回作为最终的修补程序。 否则，中间的修补程序提供给 HLOS 可用。</p></td>
</tr>
<tr class="odd">
<td><p>用例 7</p></td>
<td><p>不适用</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p><strong>DBT 或 TBT 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取高准确性结果。 中间的修补程序提供给 HLOS 可用。</p></td>
</tr>
<tr class="even">
<td><p>用例 8</p></td>
<td><p>不适用</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p><strong>DBT 或 TBT 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取中/低准确性结果。 如果满足要求的修补程序已可用，则这返回作为最终的修补程序。 否则，中间的修补程序提供给 HLOS 可用。</p></td>
</tr>
<tr class="odd">
<td><p>用例 9</p></td>
<td><p>高</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p>高</p></td>
<td><p><strong>DBT 或 TBT 会话行为：</strong>会话已获得高精度的修补程序或中间的修补程序，因此无需更改。</p></td>
</tr>
<tr class="even">
<td><p>用例 10</p></td>
<td><p>高</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p>高然后更改为中/低 SS 会话完成后</p></td>
<td><p><strong>DBT 或 TBT 会话行为：</strong>会话可以继续获取高精度的修补程序或中间的修补程序，直到 SS 会话已完成。 然后，它应更改到中/低准确性的修补程序。</p></td>
</tr>
<tr class="odd">
<td><p>用例 11</p></td>
<td><p>中/低</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p>中/低-&gt;高</p></td>
<td><p><strong>DBT 或 TBT 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取高准确性结果。 中间的修补程序提供给 HLOS 可用。</p></td>
</tr>
<tr class="even">
<td><p>用例 12</p></td>
<td><p>中/低</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p>高-&gt;中/低</p></td>
<td><p><strong>DBT 或 TBT 会话行为：</strong>GNSS 设备与会话进行刷新或重新启动以获取中/低准确性结果。 如果满足要求的修补程序已可用，则这返回作为最终的修补程序。 否则，中间的修补程序提供给 HLOS 可用。</p></td>
</tr>
</tbody>
</table>










