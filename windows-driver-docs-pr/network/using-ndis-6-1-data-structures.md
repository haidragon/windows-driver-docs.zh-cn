---
title: 使用 NDIS 6.1 数据结构
description: 使用 NDIS 6.1 数据结构
ms.assetid: 425cd2dc-99b0-4bed-8f7b-c291769c420a
keywords:
- 数据结构 WDK 网络
- NDIS WDK 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81058681da218df199f292adad775bf25d6e7dc5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360728"
---
# <a name="using-ndis-61-data-structures"></a>使用 NDIS 6.1 数据结构





NDIS 可以支持多个版本的相同的数据结构。 使用 NDIS 6.1 驱动程序更新 Windows Server 2008 中，Windows Vista Service Pack 1 (SP1) 中的结构或这两种操作系统必须报告正确**修订**成员和**大小**中的成员值[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)结构，它是在**标头**结构，如果有，成员时驱动程序初始化 NDIS 6.1 数据结构。

**请注意**  若要确定正确的版本和大小信息，请参阅每个结构，其中包含的参考页**标头**成员。 结构中包含的参考页**标头**成员的已更新和 NDIS 6.1 包括 NDIS 6.1 驱动程序的新信息。 如果不会更新到结构的 NDIS 6.1，NDIS 6.0 驱动程序提供的信息也适用于 NDIS 6.1 驱动程序。

 

 

 





