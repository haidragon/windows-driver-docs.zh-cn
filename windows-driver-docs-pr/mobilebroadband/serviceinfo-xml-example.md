---
title: ServiceInfo XML 示例
description: ServiceInfo XML 示例
ms.assetid: b2114044-ca4b-4c1e-ab2e-73f4f56142b5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80211e10f4a905c80c6d23dadd7412fc305e32f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524129"
---
# <a name="serviceinfo-xml-example"></a>ServiceInfo XML 示例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

下面的 XML 文档使用[ServiceInfo XML 架构](serviceinfo-xml-schema.md)指定 Contoso 无线服务属性：

``` syntax
<DeviceInfo xmls="http://schemas.microsoft.com/windows/2010/05/DeviceMetadata/ServiceInfo">
    <ServiceCategoryList>
        <ServiceCategory>Network.MobileBroadband </ServiceCategory>
    </ServiceCategoryList>
    <ServiceName> </ServiceName>
    <ServiceDescription1>Fabrikam Wireless 3G network</ServiceDescription1>
    <ServiceDescription2></ServiceDescription2>
    <ServiceNumber>D4A5C6D5-8135-4A0D-9B9D-016F5D7D9F45  </ServiceNumber>
    <ServiceProvider>Contoso Wireless</ServiceProvider>
    <ServiceIcon>Contoso.ico</ServiceIcon>
    <ServiceSpecificExtension namespace="http://schemas.microsoft.com/windows/2010/12/DeviceMetadata/MobileBroadbandInfo">MobileBroadbandInfo.xml</ServiceSpecificExtension>
</ServiceInfo>
```

 

 





