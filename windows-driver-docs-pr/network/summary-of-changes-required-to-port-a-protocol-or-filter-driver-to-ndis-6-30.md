---
title: 到端口协议或筛选器驱动程序到 NDIS 6.3 的更改
description: 若要更新的 NDIS 6.x 协议或筛选器驱动程序支持 NDIS 6.30，您必须修改以下各节中所述。
ms.assetid: 1C6CB2E1-C129-4F3B-AF7D-357580BEE7F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b447b26d16ec8f924e5c80d4aae555bd2933d0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377988"
---
# <a name="summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-630"></a>将协议或筛选器驱动程序移植到 NDIS 6.30 所要做出的更改摘要


若要更新的 NDIS 6.x 协议或筛选器驱动程序支持 NDIS 6.30，您必须修改以下各节中所述。

-   [构建环境](#build-environment)
-   [常规移植协议驱动程序](#general-porting-requirements-for-protocol-drivers)
-   [常规移植的筛选器驱动程序要求](#general-porting-requirements-for-filter-drivers)

## <a name="build-environment"></a>构建环境


-   替换为预处理器定义 NDIS60 或 NDIS61 或 NDIS620，如果存在，NDIS630。
-   更新的主版本号和次的 NDIS 版本编号在 NDIS\_*Xxx*\_驱动程序\_特征结构中所述[实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md).

## <a name="general-porting-requirements-for-protocol-drivers"></a>常规移植协议驱动程序


协议驱动程序应始终完成**NetEventSetPower**而无需等待数据包。 有关详细信息，请参阅：

-   [在 NDIS 6.30 电源管理增强功能](power-management-enhancements-in-ndis-6-30.md)
-   [处理即插即用事件和协议驱动程序中的电源管理事件](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)

有关 NDIS 6.30 功能的详细信息，请参阅[简介 NDIS 6.30](introduction-to-ndis-6-30.md)。

## <a name="general-porting-requirements-for-filter-drivers"></a>常规移植的筛选器驱动程序要求


筛选器驱动程序应始终完成**NetEventSetPower**而无需等待数据包。 有关详细信息，请参阅：

-   [在 NDIS 6.30 电源管理增强功能](power-management-enhancements-in-ndis-6-30.md)
-   [**NDIS\_微型端口\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)
-   [**NET\_PNP\_EVENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)
-   [OID\_PNP\_SET\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

有关 NDIS 6.30 功能的详细信息，请参阅[简介 NDIS 6.30](introduction-to-ndis-6-30.md)。

 

 





