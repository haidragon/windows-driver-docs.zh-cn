---
title: 请求显示自定义 UI
description: 请求显示自定义 UI
ms.assetid: 4b7366d9-e55a-4b24-b75f-a5f133b80ca7
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，请求显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e33af721872cd1e56c3a53a57808ee3bff5895b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373230"
---
# <a name="requesting-the-display-of-a-custom-ui"></a>请求显示自定义 UI




 

本机 802.11 IHV 扩展 DLL 可以请求通过本机 802.11 IHV UI 扩展 DLL 的自定义用户界面 (UI) 的显示。 例如，IHV 扩展 DLL 无法请求到显示的自定义 UI:

-   无线 LAN (WLAN) 关联操作期间，在各个阶段通知最终用户。

-   在将 WLAN 适配器具有为 WLAN 网络解除关联时，请通知最终用户。

-   通知最终用户使用 WLAN 网络进行身份验证的结果。

若要启动自定义 UI 或显示的通知，本机 802.11 IHV 扩展 DLL 调用[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request) ，并将传递一个指向[ **DOT11EXT\_IHV\_UI\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构通过*pIhvUIRequest*此函数的参数。

通过[ **DOT11EXT\_IHV\_UI\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构，本机 802.11 IHV 扩展 DLL 指定自定义 UI 的以下数据：

-   用户会话标识符 (ID)，用于标识特定的用户上下文。

-   全局唯一 ID (GUID)，用于标识特定的用户界面请求。

-   类 ID (CLSID) 的**IWizardExtension**在本机 802.11 IHV UI 扩展 DLL 中实现的 COM 接口。 CLSID 用于请求特定的自定义 UI 支持的 DLL。

    有关详细信息**IWizardExtension** COM 接口，请参阅[IWizardExtension COM 接口](https://go.microsoft.com/fwlink/p/?linkid=56607)。

-   包含将由独立硬件供应商 (IHV) 定义并由指定处理的专有格式的数据的缓冲区**IWizardExtension** COM 接口。 例如，缓冲区可能包含自定义用户界面中显示的默认值。

具体取决于 WLAN 连接状态的用户会话 ID 的自定义 UI 请求将显示为以下值之一：

-   如果适配器已连接到 WLAN 网络，则请求将显示为独立的可单击气球状通知通过启动 UI。 有关此过程的详细信息，请参阅[显示气球状通知](displaying-custom-ui-pages-within-a-balloon-notification.md)。

-   如果适配器是在连接到 WLAN 网络的过程中，请求将显示为一组标准的网络连接 UI 中的向导页。 有关此过程的详细信息，请参阅[网络连接向导中显示自定义 UI 页面](displaying-custom-ui-pages-within-the-network-connection-wizard.md)。

 

 





