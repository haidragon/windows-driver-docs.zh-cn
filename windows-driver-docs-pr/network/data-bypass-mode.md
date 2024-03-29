---
title: 数据旁路模式
description: 数据旁路模式
ms.assetid: 98061803-22de-4fa2-8582-2d382f84dd75
keywords:
- 筛选器驱动程序 WDK 网络、 数据绕过模式
- NDIS 筛选器驱动程序 WDK，数据绕过模式
- 数据绕过模式 WDK 网络
- 绕过模式 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f15258293a0949b841fd9ec20251106d9297672
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364947"
---
# <a name="data-bypass-mode"></a>数据旁路模式





筛选器驱动程序*数据绕过模式*可改进的系统性能。 NDIS 不会调用*FilterXxx*会绕过的函数。 例如，如果发送和接收服务不需要的给定筛选器应用程序、 筛选器驱动程序可以跳过发送和接收函数。

筛选器驱动程序指定的默认入口点，可以跳过，在驱动程序初始化时，它调用的函数[ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)函数。 入口点是**NULL**默认情况下跳过的函数。 有关初始化的详细信息，请参阅[初始化筛选器驱动程序](initializing-a-filter-driver.md)。

若要更改在运行时绕过状态，该驱动程序必须指定的入口点[ *FilterSetModuleOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_set_module_options)在驱动程序初始化过程中的函数。 该驱动程序可以初始化[ **NDIS\_筛选器\_分部\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_partial_characteristics)结构，将传递到新的特征[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)的上下文中从函数*FilterSetModuleOptions*。

NDIS 调用*FilterSetModuleOptions*函数，如果有，重启操作开始处。 筛选器驱动程序可以将单独为每个筛选器模块的绕过模式设置。 有关详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

筛选器驱动程序可以绕过以下可选*FilterXxx*中指定的函数[ **NDIS\_筛选器\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_driver_characteristics)结构：

[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)

[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists_complete)

[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)

[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)

若要设置*FilterXxx*函数来绕过模式下，筛选器驱动程序指定**NULL**为该函数的入口点。 但是，如果驱动程序调用任何 NDIS 函数，都有一个关联*FilterXxx*函数，它必须为此，提供的入口点*FilterXxx*函数。 例如，如果驱动程序调用[ **NdisFIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)函数，它必须提供[ *FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)函数。

如果指定了筛选器驱动程序[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)函数，并发送请求进行排队，它还必须指定[ *FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)函数。

如果指定了筛选器驱动程序[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)或[ **FilterReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)函数，该驱动程序必须此外指定[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)函数。

若要在运行时更改其绕过模式设置，筛选器驱动程序可以调用[ **NdisFRestartFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfrestartfilter)函数。 **NdisFRestartFilter**计划暂停操作，后跟指定的筛选器模块的重新启动操作。 当调用 NDIS *FilterSetModuleOptions*，筛选器驱动程序可以通过调用来更改该筛选器模块的函数**NdisSetOptionalHandlers**并指定一组新的入口点。

**请注意**  暂停和重启可能导致某些网络数据包被删除的传输路径，或者接收的路径，或两者。 提供一种可靠的传输机制的网络协议可能会重试网络 I/O 操作对于丢失的数据包，但并不能保证可靠性其他协议不重试该操作。

 

筛选器驱动程序可以注册支持可选驱动程序服务的其他可选函数。 该驱动程序注册中的这些可选服务[ *FilterSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 有关这些可选服务的详细信息，请参阅[配置可选的筛选器驱动程序服务](configuring-optional-filter-driver-services.md)。

 

 





