---
title: BDA 筛选器类别 GUID
description: BDA 筛选器类别 GUID
ms.assetid: fbd4bf91-8309-423a-97ea-7e4f90cd3b68
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7f9d1e033ac03dc8b6e124a5568efbe18ed20a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386690"
---
# <a name="bda-filter-category-guids"></a>BDA 筛选器类别 GUID


## <span id="ddk_bda_filter_category_guids_ks"></span><span id="DDK_BDA_FILTER_CATEGORY_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA 筛选器类别的 Guid 来指定 BDA 筛选器来创建的类型。 BDA 微型驱动程序这些 Guid 按指派到的数组**类别**的成员[ **KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)结构点。 *Bdamedia.h*标头文件定义了这些 Guid。

下面的筛选器类别 BDA 中提供了 Guid:

<span id="KSCATEGORY_BDA_RECEIVER_COMPONENT"></span><span id="kscategory_bda_receiver_component"></span>KSCATEGORY\_BDA\_接收方\_组件  
BDA 微型驱动程序将分配此 GUID 来指定创建 BDA 接收方筛选器。

<span id="KSCATEGORY_BDA_NETWORK_TUNER"></span><span id="kscategory_bda_network_tuner"></span>KSCATEGORY\_BDA\_网络\_调谐器  
BDA 微型驱动程序将分配此 GUID 来指定创建 BDA 网络调谐器筛选器。

<span id="KSCATEGORY_BDA_NETWORK_EPG"></span><span id="kscategory_bda_network_epg"></span>KSCATEGORY\_BDA\_NETWORK\_EPG  
BDA 微型驱动程序将分配此 GUID 来指定创建 BDA 电子版收视指南 (EPG) 筛选器。

<span id="KSCATEGORY_BDA_IP_SINK"></span><span id="kscategory_bda_ip_sink"></span>KSCATEGORY\_BDA\_IP\_接收器  
BDA 微型驱动程序将分配此 GUID 来指定创建 BDA IP 接收器筛选器。

<span id="KSCATEGORY_BDA_NETWORK_PROVIDER"></span><span id="kscategory_bda_network_provider"></span>KSCATEGORY\_BDA\_NETWORK\_PROVIDER  
BDA 微型驱动程序将分配此 GUID 来指定创建 BDA 网络提供程序筛选器。

<span id="KSCATEGORY_BDA_TRANSPORT_INFORMATION"></span><span id="kscategory_bda_transport_information"></span>KSCATEGORY\_BDA\_传输\_信息  
BDA 微型驱动程序将分配此 GUID 来指定创建 BDA 传输的信息筛选器 (TIF)。

 

 





