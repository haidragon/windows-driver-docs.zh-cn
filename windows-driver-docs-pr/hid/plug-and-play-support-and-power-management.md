---
title: 即插即用支持 I2C
description: 本部分介绍设备的支持通过 I²C HID 插的支持。
ms.assetid: 2D51B1B7-345E-4311-81D6-8A14CE2B44FE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8ab4e5227671e191e68336422157605adfaa75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545465"
---
# <a name="plug-and-play-support-for-i2c"></a>即插即用支持 I2C


本部分介绍通过 I²C 传输支持 HID 设备的即插支持。

### <a name="driver-loading"></a>驱动程序加载

Windows 将加载根据硬件标识符和 INF 之间兼容的标识符匹配的 HID I²C 类驱动程序。 通过高级配置和电源接口 (ACPI) 生成标识符。 为在 ACPI I²C 设备节点生成的硬件标识符。 所有 HID I²C 兼容的设备必须公开兼容性标识符，除了唯一的硬件标识符。

ACPI 5.0 规范包括的 HID 类设备的支持。 HID I²C 的 ACPI 定义如下所示。

|                           |                                             |             |                                                 |                                                                                      |
|---------------------------|---------------------------------------------|-------------|-------------------------------------------------|--------------------------------------------------------------------------------------|
| 字段                     | 值                                       | ACPI 对象 | 格式                                          | 备注                                                                             |
| 兼容 ID             | PNP0C50                                     | \_CID       | ACPI0C50 或 PNP0C50 的格式字符串     | CompatibleID                                                                         |
| 硬件 ID               | 特定于供应商                             | \_HID       | VVVVdddd （例如 NVDA0001） 格式的字符串 | VendorID + DeviceID                                                                  |
| 子系统                 | 特定于供应商                             | \_SUB       | VVVVssss （例如 INTL1234） 格式的字符串 | SubVendorID + SubSystemID                                                            |
| 硬件版本         | 特定于供应商                             | \_HRV       | 0xRRRR （2 个字节修订版本）                         | RevisionID                                                                           |
| 当前资源设置 | 特定于供应商                             | \_CRS       | 字节流                                     | 必须包括 I2CSerialBus 和 GPIO\_I2C 控制器 INT 和 GPIO 中断响应 |
| 设备特定的方法    | GUID {3CDFF6F7-4267-4555-AD05-B30A3D8938DE} | \_DSM       | 应用包                                         | 定义包含 HID 描述符地址的结构。                        |

 

每个 HID I²C 设备必须提供以下必填字段：

-   兼容 ID
-   硬件 ID
-   硬件版本
-   当前资源设置
-   设备特定的方法

请参阅高级配置和电源接口 (ACPI) 5.0 规范的其他信息。

下面提供了示例的硬件 Id 和兼容 Id 为随机的 HID I²C 设备。 这些详细信息基于本身所报告的一个顶级集合的类"特定于供应商"HID 示例设备。

高级配置和电源接口 (ACPI) 生成的以下的硬件 Id 和兼容 Id，若要加载的 HID I²C 传输驱动程序：

|                                      |                        |
|--------------------------------------|------------------------|
| 硬件标识符                 | 兼容的标识符 |
| ACPI\\Vid\_xxxx&Pid\_yyyy&Rev\_zzzz; | ACPI\\PNP0C50          |
| ACPI\\Vid\_xxxxPid\_yyyy;            |                        |
| ACPI\\xxxxyyyy;                      |                        |

 

在上一示例中，硬件 ID 使用生成从提取的值\_HID ACPI 方法的示例设备。 使用从提取的值生成兼容 ID \_CID ACPI 方法的示例设备。 HID I2C 通过兼容 ID 必须始终为 PNP0C50，对于 1.0 版。

**请注意**  如果提供 INF，应仅在上表的左侧列中使用的硬件标识符。 （不使用兼容的标识符右侧列中。）

 

HIDClass.sys 组件生成的隐藏客户端设备节点的硬件 ID 是按如下所示：

|                                                      |                       |
|------------------------------------------------------|-----------------------|
| 硬件标识符                                  | 兼容的标识符 |
| HID\\VEN\_MSFT&DEV\_0010&REV\_0002&Col01;            | 不适用                   |
| -HID\\VEN\_MSFT&DEV\_0010&Col01 HID\\MSFT0010&Col01; | 不适用                   |
| -HID\\\*MSFT0010Col01                                | 不适用                   |
| -HID\_DEVICE\_UP:FF00\_U:0001;                       | 不适用                   |
| -HID\_DEVICE                                         | 不适用                   |

 

硬件 ID 由 HIDClass.sys 生成，是完全相同的所有传输。 此标识符基于从 HIDI2C.sys （提取自 ACPI） 传递给 HIDClass.sys 的值。

### <a name="device-enumeration-sequence"></a>设备将枚举序列

一次 HID I²C 设备驱动程序 (HIDI2C。加载 Sys)，它开始通过 I²C 总线与设备进行通信。 该驱动程序执行的第一个操作是设备枚举序列。

以下列表提供了将枚举序列。 请注意，此列表的顺序可能在将来更改的 Windows 版本。

1.  为从系统 BIOS HID I²C 设备检索 ACPI ASL 代码。
2.  从设备中检索 HID 描述符。
    -   编写 HID 描述符地址
    -   读取 HID 描述符

3.  发出一组\_到设备的电源。
    -   编写组\_电源命令

4.  发出重置 （主机启动的重置） 到设备。
    -   编写重置命令
    -   设备断言 GPIO 中断
    -   读取输入寄存器的值 (0x00 0x00)

5.  从设备中检索报表描述符。
    -   编写报表描述符地址
    -   阅读报告描述符

如果主机无法成功完成任何与设备的步骤 1-5，HIDI²C 驱动程序可能加载错误值为*代码 10*。 没有内置到其中任何命令，重试逻辑。

**请注意**  步骤 4 和 5 并行优化 I²C 上的时间才能这样做。 由于报告描述符 （a） 静态和 （b） 相当长，Windows 8 可能发出请求，5，4 上等待来自设备的响应时。

 

### <a href="" id="supported-hid-i2c-commands"></a>受支持的 HID I²C 命令

HIDI2C。SYS 驱动程序支持以下命令

|                 |                                                |                                                                                                                                                                                                       |
|-----------------|------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 命令         | 如何使用它                                  | 使用时                                                                                                                                                                                        |
| Reset           | Windows 支持主机启动的重置。     | Windows 将发出此命令在以下方案-设备初始化期间的禁用/启用-卸载/重新安装                                                                         |
| 获取/设置\_报表 | Windows 支持 Get/Set\_报表命令。 | Windows 将在以下方案中的过程发出以下命令，当 HID 客户端驱动程序发出 get/set 功能报表请求-当 HID 客户端驱动程序发出的同步输入/输出报表 |
| 设置\_电源      | Windows 支持一组\_电源命令        | 系统将转换为低能耗 S3 / 连接待机状态-当系统处于关闭状态时，Windows 将在以下方案中的过程发出此命令。                               |

 

 

 



