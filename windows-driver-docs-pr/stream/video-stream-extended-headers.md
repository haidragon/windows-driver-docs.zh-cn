---
title: 视频流扩展标头
description: 视频流扩展标头
ms.assetid: 6540026c-a41a-49e2-a41f-fe64106408f5
keywords:
- 视频捕获 WDK AVStream，扩展标头
- 捕获视频 WDK AVStream，扩展标头
- 扩展标头 WDK 视频捕获
- 标头 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caef9db00227c56620ad61dce4cc991fb11afa01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385368"
---
# <a name="video-stream-extended-headers"></a>视频流扩展标头


视频捕获微型驱动程序在其输出流中使用扩展标头提供的流和当前的框架内容的辅助信息。 例如，图像流标头提供有关当前的帧数、 丢弃的帧和字段极性标志数的信息。 为每个帧已完成，微型驱动程序填充有关捕获的帧的辅助信息的扩展标头中。

Stream 类视频捕获微型驱动程序指示其能够通过设置提供 pin 此附加信息**StreamHeaderMediaSpecific**的成员[ **HW\_流\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_object)结构**sizeof**两个以下结构之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>结构名称</th>
<th>用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info" data-raw-source="[&lt;strong&gt;KS_FRAME_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)"><strong>KS_FRAME_INFO</strong></a></p></td>
<td><p>帧数、 丢弃帧、 字段极性标志和 DirectDraw 图面上的句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_vbi_frame_info" data-raw-source="[&lt;strong&gt;KS_VBI_FRAME_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_vbi_frame_info)"><strong>KS_VBI_FRAME_INFO</strong></a></p></td>
<td><p>VBI 格式通道更改信息，标准的视频。</p></td>
</tr>
</tbody>
</table>

 

如果 Stream 类微型驱动程序不提供此附加信息，则应设置**StreamHeaderMediaSpecific**为零。

有关何时中指定一个值的详细信息**StreamHeaderMediaSpecific**，请参阅[Stream 类别](stream-categories.md)。

 

 




