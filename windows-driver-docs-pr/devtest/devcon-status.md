---
title: DevCon Status
description: 显示计算机上的设备驱动程序的状态 （正在运行、 已停止或已禁用）。 在本地和远程计算机上有效。
ms.assetid: 97da6df4-ad93-440a-9136-13f2b79cbe9c
keywords:
- DevCon 状态驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Status
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c2a852f740770cdee6239907455a16aef54e54a
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492510"
---
# <a name="devcon-status"></a>DevCon Status


显示计算机上的设备驱动程序的状态 （正在运行、 已停止或已禁用）。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] status {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconstatustoolsspanspan-idddkdevconstatustoolsspanparameters"></a><span id="ddk_devcon_status_tools"></span><span id="DDK_DEVCON_STATUS_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。



<span id="______________"></span> **\\** *   
表示在计算机上的所有设备。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定全部或部分硬件 ID、 兼容 ID 或设备的设备实例 ID。 在指定多个 Id 时，键入一个空格之间每个 id。 包含一个 & 字符的 Id ( **&** ) 必须括在引号中。

以下特殊字符修改 ID 参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>匹配任何字符或任何字符。 使用通配符字符 (</em>) 创建 ID 模式，例如，<em>磁盘</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>例如，指示设备实例 ID <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>（单引号）</p></td>
<td align="left"><p>按原义的字符串匹配 （严格按其显示）。 使用单引号以指示星号是 ID 名称的一部分，不是通配符，例如，字符串前加上 <strong>'*PNP0600</strong>，其中 *PNP0600 （包括星号） 是硬件 id。</p></td>
</tr>
</tbody>
</table>  



<span id="________class______"></span><span id="________CLASS______"></span> **=** _class_   
指定设备的设备安装程序类。 等号 ( **=** ) 标识作为类名称的字符串。

此外可以指定硬件 Id、 兼容 Id、 设备实例 Id 或类名称后面的 ID 模式。 键入每个 ID 或模式之间有空格。 DevCon 匹配指定的 Id 的类中查找设备。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**状态**)。 否则，将忽略 DevCon **/m**参数并显示本地计算机上的设备驱动程序的状态，且不返回语法错误。

如果 DevCon 无法确定的设备，例如当设备无法再连接到计算机，状态 DevCon 会忽略描述从状态显示状态的行。

下面的示例显示成功状态命令。 描述设备状态的文本以粗体显示。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
    Driver is running.
1 matching device(s) found.
```

与此相反，下面的示例演示如何 DevCon 显示找不到设备的状态。 状态说明是从显示中消失。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
1 matching device(s) found.
```

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon /m:\\Server01 status *
devcon status pci*
devcon status "PCI\VEN_115D&DEV_0003&SUBSYS_0181115D"
devcon status =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 17:在本地计算机上显示的所有设备的状态](devcon-examples.md#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[18 的示例：显示设备通过设备实例 ID 的状态](devcon-examples.md#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[示例 19:在远程计算机上显示相关设备的状态](devcon-examples.md#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)









