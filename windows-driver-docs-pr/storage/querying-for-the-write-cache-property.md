---
title: 查询写缓存属性
description: 查询写缓存属性
ms.assetid: 80b7c366-3b54-4dae-8ac7-63caaa1767f9
keywords:
- 存储驱动程序 WDK，写入缓存
- 编写缓存 WDK 存储
- 将写回到 WDK 存储
- 编写通过 WDK 存储
- 同步缓存支持 WDK 存储
- 电池备份 WDK 存储
- 缓存 WDK 存储
- 在查询写入缓存
- 写通式请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a5052b603544e1374d7329aede8b78052dcee27
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383149"
---
# <a name="querying-for-the-write-cache-property"></a>查询写缓存属性


存储设备通常将数据写入到非易失性的媒体，如磁盘盘片之前缓冲写入缓存中的数据。 此类型的缓冲区可以提高设备性能，但它还会降低数据的完整性。 如果写入缓存没有备用电池，电源故障可能导致丢失缓存数据。

数据丢失的问题的一种补救措施是刷新写入缓存 （使用 SCSI 设备上的 SCSI 同步缓存命令）。 但是，刷新写入缓存是代价高昂的操作，并且如果经常执行此操作，它会大大降低性能。 无需刷新写入缓存，多个存储设备可允许*直写*请求。 直写请求绕过写缓存，并将数据发送到媒体直接。

例如，数据库应用程序可以使用直写请求以确保事务日志达到媒体和文件系统驱动程序可以使用直写请求，以确保该文件系统元数据到达媒体。

但是，并非所有具有写入缓存的存储设备支持直写请求或同步缓存中;并且，某些设备不需要绕过或刷新缓存的数据作为预防措施，因为它们具有防止在电源故障期间的数据损坏的电池备份系统。 应用程序和驱动程序必须具有有关设备的写入缓存的属性的信息，然后才能进行有效地使用它。

在 Windows Vista 中，可以使用[ **IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)请求与**StorageDeviceWriteCacheProperty**属性标识符以查询指定的设备的特征写入缓存的写缓存属性的存储类驱动程序。 写缓存属性包括有关缓存功能的设备的以下信息：

-   *写入缓存是否存在*。 写缓存属性指定设备是否具有写入缓存。

-   *写缓存类型*。 有两种主要类型的写入缓存：*写回*并*通过编写*。 使用回写式缓存，设备不会缓存将数据复制到非易失性媒体到绝对必要时。 此操作可以提高写入操作的性能。 使用写通式缓存，设备将数据写入到缓存和并行媒体。 这无法提高写入性能，但它使后续读取的操作速度更快。

    不要混淆写通式*缓存*使用写通式*请求*。 可以与任何类型的缓存，如果设备支持直写请求包括回写缓存，使用直写请求。 例如，假设目标是回写式缓存的 SCSI 设备。 如果设备支持直写请求，发起方可以绕过写缓存，通过写命令的命令描述符块 (CDB) 中设置强制单元访问 (FUA) 位。

-   *同步缓存支持*。 写缓存属性指示设备是否支持 SCSI 同步缓存命令或其他总线上的等效命令。

-   *备用电池*。 写缓存属性指示设备是否具有备用电池，可将保护在电源故障期间的缓存数据的完整性。

写缓存属性报告的信息的完整说明，请参阅[**存储\_编写\_缓存\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_write_cache_property)。

而无需写入缓存的属性机制 (即，使用 IOCTL\_存储\_查询\_属性请求并**StorageDeviceWriteCacheProperty**属性标识符)，应用程序和驱动程序必须查询设备的写入缓存特征，具有不同的序列的每个总线的命令。 例如，如果目标设备连接到 IEEE 1394 总线，而且使用减少块命令 （红细胞） 协议，发起方必须检索设备的模式来确定是否已启用写入缓存的数据的第 6 页。 但如果目标设备 SCSI 符合，发起方必须检索第 8 页的模式数据。 写入缓存的属性机制隐藏从发起方这些操作的详细信息，并提供不同的总线都是相同的存储设备的写入缓存的特征查询技术。

写入缓存的属性机制 （因为查询这些设备没有标准的方法） 不支持的 RAID 设备，或为闪存内存设备。

在 Windows 64 位版本上支持写入缓存属性。

 

 




