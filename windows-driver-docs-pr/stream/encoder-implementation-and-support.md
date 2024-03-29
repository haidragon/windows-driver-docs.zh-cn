---
title: 编码器实现和支持
description: 编码器实现和支持
ms.assetid: 6ba97ff8-815b-490f-920b-6ede4f730e98
keywords:
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩数据流 WDK AVStream
- 编码的流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- 属性集 WDK 编码器
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- ENCAPIPARAM_PEAK_BITRATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98a0bd04cedcdc81ea44d501bef1d7868dfb08f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384120"
---
# <a name="encoder-implementation-and-support"></a>编码器实现和支持

在 Windows XP Service Pack 1，Microsoft 定义了三个内核的流式处理属性集和中的一个枚举*ksmedia.h*以支持仅视频编码器设备。 每个属性集包含单个属性。 换而言之，每个属性接收其自身属性集。 如果您的驱动程序发出*获取*的属性或*设置*-属性调用，然后指定属性集 GUID (如中所定义*ksmedia.h*) 中**设置**的成员[ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)结构，不进行任何**Id**成员时设置调用：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性集</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate" data-raw-source="[ENCAPIPARAM_BITRATE](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate)">ENCAPIPARAM_BITRATE</a></td>
<td><p>此属性设置为指定的编码比特率编码器设备支持的实现。 请参阅<a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">编码器的代码示例</a>的更多详细信息。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode" data-raw-source="[ENCAPIPARAM_BITRATE_MODE](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode)">ENCAPIPARAM_BITRATE_MODE</a></td>
<td><p>实现此属性设置为指定的设备支持的编码模式。 设置此属性的用法<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode" data-raw-source="[&lt;strong&gt;VIDEOENCODER_BITRATE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)"> <strong>VIDEOENCODER_BITRATE_MODE</strong> </a>枚举来指定支持的模式。 请参阅<a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">编码器的代码示例</a>的更多详细信息。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-peak-bitrate" data-raw-source="[ENCAPIPARAM_PEAK_BITRATE](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-peak-bitrate)">ENCAPIPARAM_PEAK_BITRATE</a></td>
<td><p>实现此属性设置为指定的设备的最大的编码比特率。</p></td>
</tr>
</tbody>
</table>

客户端访问这些属性通过派生**IVideoEncoder**从 COM 接口**IEncoderAPI** COM 接口 （Windows 软件开发工具包 (SDK) 文档中所述）。

微型驱动程序必须指定默认值为每个 ENCAPIPARAM\_*Xxx*属性。 本主题[编码器的代码示例](encoder-code-examples.md)演示如何指定默认属性值。 在开发和调试的编码器筛选器，当前的属性页可以触发的微型驱动程序支持 ENCAPIPARAM\_比特率属性集。

在 DirectX 9.0 中，六个其他属性集和一个事件集定义中*ksmedia.h*为广泛的编码器，包括仅限音频的编码器提供更好的支持。 与使用 ENCAPIPARAM\_*Xxx*属性，每个属性接收其自身属性集：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性集</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-video-encoder" data-raw-source="[CODECAPI_VIDEO_ENCODER](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-video-encoder)">CODECAPI_VIDEO_ENCODER</a></td>
<td><p>如果你的设备支持编码的视频流 （包括如电视音频辅助音频） 然后实现此属性集的支持。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-audio-encoder" data-raw-source="[CODECAPI_AUDIO_ENCODER](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-audio-encoder)">CODECAPI_AUDIO_ENCODER</a></td>
<td><p>如果你的设备是仅限音频的编码器，然后实现而不是 CODECAPI_VIDEO_ENCODER 设置此属性的支持。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-setalldefaults" data-raw-source="[CODECAPI_SETALLDEFAULTS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-setalldefaults)">CODECAPI_SETALLDEFAULTS</a></td>
<td><p>实现此属性设置重置编码器设备的所有内部设置，例如编码比特率和编码为其默认值的模式。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-allsettings" data-raw-source="[CODECAPI_ALLSETTINGS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-allsettings)">CODECAPI_ALLSETTINGS</a></td>
<td><p>实现此属性设置为通信编码器设备的当前设置。 设置此属性用于客户端之间的通信。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-supportsevents" data-raw-source="[CODECAPI_SUPPORTSEVENTS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-supportsevents)">CODECAPI_SUPPORTSEVENTS</a></td>
<td><p>如果设备支持事件从用户模式-例如，若要更改的编码模式，比特率或其他设置--则实现此属性集。 如果你实现此属性集，然后必须还实现对 CODECAPI_CHANGELISTS 事件支持。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-currentchangelist" data-raw-source="[CODECAPI_CURRENTCHANGELIST](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-currentchangelist)">CODECAPI_CURRENTCHANGELIST</a></td>
<td><p>实现此属性设置来确定哪些编码器参数已更改以前调用设置一个或多个编码器属性中。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件组</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-changelists" data-raw-source="[CODECAPI_CHANGELISTS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-changelists)">CODECAPI_CHANGELISTS</a></p></td>
<td><p>如果设备支持对通过 CODECAPI_SUPPORTSEVENTS 属性组的用户模式事件作出响应，则实现此事件集以返回已更改为客户端的结果的以前的编码器设置的列表<em>设置</em>-属性调用 CODECAPI_SETALLDEFAULTS 或 CODECAPI_ALLSETTINGS。</p></td>
</tr>
</tbody>
</table>

客户端访问这些属性流过**ICodecAPI** COM 接口 （Windows SDK 文档中所述）。 请参阅[编码器安装和注册](encoder-installation-and-registration.md)有关 COM 接口的详细信息，包括如何指定 KsProxy 应公开的接口。

微型驱动程序应实现支持 basic*获取*-属性查询。 本主题[编码器的代码示例](encoder-code-examples.md)演示如何支持*获取*-属性查询。

在开发一个编码器筛选器时，将编码功能移到单独的筛选器中，从视频捕获筛选器。 定义你自己专用的媒体，使图形生成器可以正确连接编码器，并捕获筛选器。 如果您的硬件能够支持的总线控制非编码的内容，则可能还公开公共媒介。 如果你实现公钥和私钥的媒体，然后专用媒介首先列出，因为它可以减少图形构建时间;若要生成筛选器关系图时，请查找正确的筛选器。

有关使用介质和筛选器的多个实例 （在单独的筛选器关系图） 的详细信息请参阅[介质和类别](mediums-and-categories.md)。
