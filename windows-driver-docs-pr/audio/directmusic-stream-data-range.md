---
title: DirectMusic 流数据范围
description: DirectMusic 流数据范围
ms.assetid: e3423901-330e-4a86-a921-6678e1c45a97
keywords:
- DirectMusic WDK 音频，流数据范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd272c8def92c524e50a637000930829df34d34a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359032"
---
# <a name="directmusic-stream-data-range"></a>DirectMusic 流数据范围


## <span id="directmusic_stream_data_range"></span><span id="DIRECTMUSIC_STREAM_DATA_RANGE"></span>


此示例使用[ **KSDATARANGE\_音乐**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_music)结构来描述 DirectMusic 流的数据范围。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_MUSIC);
 DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
 DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DIRECTMUSIC);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
  Technology            = STATICGUIDOF(KSMUSIC_TECHNOLOGY_WAVETABLE);
  Channels              = 0;
  Notes                 = 0;
  ChannelMask           = 0xFFFF;
```

 

 




