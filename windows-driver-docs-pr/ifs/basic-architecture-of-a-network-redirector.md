---
title: 网络重定向程序的基本体系结构
description: 网络重定向程序的基本体系结构
ms.assetid: 60a7c79d-b89f-4c8b-9619-bd48c9e1efac
keywords:
- 网络重定向程序 WDK，体系结构
- 重定向程序驱动程序 WDK，体系结构
- TDI 驱动程序 WDK 文件系统
- 传输驱动程序接口 WDK 的文件系统
- WDK 的 Dll 文件系统
- SYS WDK 的文件系统
- 内核模式文件系统驱动程序 WDK 文件系统
- 用户模式 Dll WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3c6883755b24f351c7bf66970e90e85896ed423
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375717"
---
# <a name="basic-architecture-of-a-network-redirector"></a>网络重定向程序的基本体系结构


## <span id="ddk_basic_architecture_of_a_network_redirector_if"></span><span id="DDK_BASIC_ARCHITECTURE_OF_A_NETWORK_REDIRECTOR_IF"></span>


以下基本的软件组件所需的网络重定向程序的一部分：

-   内核模式文件系统设备驱动程序 (SYS)，提供重定向程序功能的网络。

-   用户模式动态链接库 (DLL)，提供用于非文件操作的客户端用户的应用程序对网络提供程序接口的访问和使用内核模式文件系统驱动程序提供网络重定向程序功能实现通信。

内核模式文件系统驱动程序组件的网络重定向程序与对象管理器、 缓存管理器、 内存管理器、 I/O 系统和其他内核系统交互，以便将远程文件访问集成到操作系统。 该驱动程序接收来自客户端应用程序通过 I/O 管理器进行远程文件访问请求，并将所需的信息通过网络发送到远程文件服务器。 该驱动程序还接收来自远程文件服务器的响应，并将信息传递回客户端应用程序通过 I/O 管理器。 网络重定向程序驱动程序还必须实现用于远程访问的网络协议或提供对另一个内核驱动程序、 用户模式应用程序或服务实现此网络协议或通信机制的调用。 要实现此网络通信的最常见方法是使用传输驱动程序接口 (TDI) 来调用现有的网络协议堆栈 (例如 TCP/IP)。 在网络驱动程序接口规范 (NDIS) 中使用的网络接口卡的底部层然后通信的网络协议堆栈。 还有可能特定于应用程序的接口可用于此通信机制。

用户模式 DLL 接收来自客户端不是文件的操作的网络提供程序接口通过特殊的请求。 这些请求可用于确定网络提供商，枚举远程网络资源，在登录到远程网络，更改网络密码装载远程网络共享或资源，使用远程服务器连接的功能和断开与远程共享文件夹的连接。 用户模式 DLL 实现用于访问远程文件系统的 WNet 用户模式 Api 的等效项。 此 DLL 然后与内核模式网络重定向程序驱动程序通过特殊 IOCTL 调用，以满足这些客户端请求进行通信。 例如，此 DLL 调用枚举 （浏览网上邻居） 的网络资源时，Windows 资源管理器中或连接到远程文件共享和资源 （打印机） 时。 此 DLL 也称为从 NET 命令行工具来查看远程资源 (**net 视图** \\ \\ *computername*) 和连接或断开连接到远程文件共享 (**net 使用**)。 也可以使用公开的 WNet Api 的多个提供程序路由器 (MPR) 的自定义应用程序调用此 DLL。

网络重定向程序还可能需要几个其他组件：

-   服务应用程序可能需要使其作为用户模式 DLL 和内核模式驱动程序之间的媒介，如果需要安全地存储在用户模式 DLL 中的全局数据的任何表。 用户模式 DLL 在客户端应用程序的进程空间中实例化，因为没有方法来保护需要在所有客户端应用程序是全局的任何内部数据表。 很可能具有连接到用户模式网络提供程序 DLL 时是私有的每个客户端应用程序的每个客户端数据，但不是全局数据。 服务应用程序 （.exe 文件） 可以使用用户模式 DLL 和内核驱动程序之间的媒介作为全局数据的表的存储位置。 例如，Microsoft 网络使用内置到 svchost.exe 工作站服务来存储全局表的"net use"连接和充当到内核模式驱动程序的中间方。 对于 Microsoft 网络、 用户模式 DLL、 ntlanman.dll、 工作站服务在 svchost.exe 的调用，然后调用内核模式驱动程序，mrxsmb.sys，提供重定向程序功能的网络。

-   安装并正确注册系统，其中必须包括创建任何必要的注册表项中的网络重定向程序组件的系统。 此外应卸载网络重定向程序，如果不再需要该软件的方法。 可以使用 Microsoft 系统安装程序 (MSI) 或 Windows INF 脚本文件来执行此安装它。 此外可以使用自定义安装程序被完成此安装和设置。

-   自定义内核模式 TDI 驱动程序需要如果网络重定向程序使用一种网络协议不包含安装操作系统 （Xerox 网络服务，例如） 中。 新 TDI 驱动程序将需要安装实现用于通信的网络协议。 内核模式网络重定向程序驱动程序连接到自定义 TDI 驱动程序的上边缘。 自定义 TDI 驱动程序将依次在其下边缘与的 NDIS 驱动程序进行通信。

    请注意，如果网络重定向程序使用 TCP/IP 协议，自定义 TDI 驱动程序不需要。 网络重定向程序将在这种情况下连接到 TCP/IP 协议 TDI 驱动程序的上边缘。

-   管理工具偶尔需要提供的访问权限的用户模式到内核模式驱动程序特殊的配置、 诊断和管理。 此外可以使用此工具来启用或禁用跟踪和解决问题的日志记录。 该工具会使用各种自定义专用 Ioctl 通信与内核驱动程序。 此工具还可能提供访问到服务控制管理器 (SCM) 来管理全局数据的存储位置安全地为用户模式网络提供程序 DLL 中介服务。

**请注意**   TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)相反。

 

 

 




