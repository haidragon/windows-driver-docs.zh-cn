---
title: Sharks Cove 硬件开发板
description: Sharks Cove 是硬件开发板，可用于开发 Windows 硬件和驱动程序。
ms.assetid: D86546BB-B613-4CEE-9A76-3FD269137EE9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6d8f91d435020e2314a071c71f959df24c6e8e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385172"
---
# <a name="sharks-cove-hardware-development-board"></a>Sharks Cove 硬件开发板

> [!WARNING]
> Windows IoT Core 不再支持 Sharks Cove 硬件开发板。  如需目前支持的开发板的列表，请参阅 [SoCs and custom boards](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/socsandcustomboards)（SoC 和自定义板）。

Sharks Cove 是[硬件开发板](https://go.microsoft.com/fwlink/p?linkid=506967)，可用于开发 Windows 硬件和驱动程序。

可以通过 Intel Sharks Cove 板为使用各种接口（包括 GPIO、I2C、I2S、UART、SDIO 和 USB）的设备开发驱动程序。 还可以使用 Sharks Cove 板为相机和触摸屏开发驱动程序。

如需与 Sharks Cove 板相关的下载，请参阅 [Sharks Cove UEFI Firmware](https://go.microsoft.com/fwlink/p?linkid=403167)（Sharks Cove UEFI 固件）。

如需详细规范，请参阅 [Sharks Cove 技术规范](https://go.microsoft.com/fwlink/p?linkid=403169)。

## <a name="span-idbefore_you_startspanspan-idbefore_you_startspanspan-idbefore_you_startspanbefore-you-start"></a><span id="Before_you_start"></span><span id="before_you_start"></span><span id="BEFORE_YOU_START"></span>准备工作


此处提供的说明要求你运行 Windows 10、Windows 8.1 或 Windows 7。 如果运行的是 Windows 8，则这些说明不适用。

如果运行的是 Windows 7，则需要安装 [PowerShell 4.0](https://go.microsoft.com/fwlink/p?linkid=507377) 和 [Windows 8.1 更新的 Windows 评估和部署工具包 (ADK)](https://go.microsoft.com/fwlink/p/?linkid=239721)。 然后，在“开始”  菜单上，转到“所有程序”  &gt;“Windows 工具包”&gt;“Windows ADK”&gt;“部署和映像工具环境”。 以管理员身份打开此命令提示符窗口。 在输入这些说明中给出的命令时，请使用此命令提示符窗口。

## <a name="span-idstep_1__get_the_board_and_related_hardwarespanspan-idstep_1__get_the_board_and_related_hardwarespanspan-idstep_1__get_the_board_and_related_hardwarespanstep-1-get-the-board-and-related-hardware"></a><span id="Step_1__Get_the_board_and_related_hardware"></span><span id="step_1__get_the_board_and_related_hardware"></span><span id="STEP_1__GET_THE_BOARD_AND_RELATED_HARDWARE"></span>步骤 1：获取开发板和相关硬件


将需要此硬件：

-   附带电源线和适配器的 Sharks Cove 板。
-   USB 集线器
-   USB 键盘
-   USB 鼠标
-   USB 网络适配器
-   监视器和 HDMI 电缆（可能还需适配器）

可以从 [Mouser Electronics](https://go.microsoft.com/fwlink/p?linkid=403172) 获取 Sharks Cove 板。

## <a name="span-idstep_2__download_kits_and_toolsspanspan-idstep_2__download_kits_and_toolsspanspan-idstep_2__download_kits_and_toolsspanstep-2-download-kits-and-tools"></a><span id="Step_2__Download_kits_and_tools"></span><span id="step_2__download_kits_and_tools"></span><span id="STEP_2__DOWNLOAD_KITS_AND_TOOLS"></span>步骤 2：下载工具包和工具


一个驱动程序开发环境有两台计算机：主计算机  和目标计算机  。 目标计算机也称为“测试计算机”  。 在主机上的 Microsoft Visual Studio 中开发和构建驱动程序。 调试程序在主机上运行并且位于 Visual Studio 用户界面中。 当测试和调试驱动程序时，驱动程序在目标计算机上运行。 在此情况下，Sharks Cove 板是目标计算机。

若要开发 Sharks Cove 板的硬件和驱动程序，需要在主机上安装以下工具包和工具：

-   [Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=533470)
-   [Windows 驱动程序工具包 (WDK)、WDK Test Pack 和 Windows 调试工具](https://go.microsoft.com/fwlink/p/?LinkId=733614)

在主机上，首先下载 Visual Studio，然后下载 WDK，再下载 WDK Test Pack。 不需要单独为 Windows 下载调试工具，因为它已经包含在 WDK 中。

### <a name="span-iddocumentationspanspan-iddocumentationspanspan-iddocumentationspandocumentation"></a><span id="Documentation"></span><span id="documentation"></span><span id="DOCUMENTATION"></span>文档

请在[此处](https://go.microsoft.com/fwlink/p?linkid=317001)开始查看 WDK 的联机文档。

请在[此处](https://go.microsoft.com/fwlink/p?linkid=223405)开始查看 Windows 调试工具的联机文档。

Windows 调试工具的文档还作为安装目录中的 CHM 文件提供。 示例：C:\\Program Files (x86)\\Windows Kits\\8.1\\Debuggers\\x64\\debugger.chm。

## <a name="span-idstep_3__install_windows_on_the_sharks_cove_boardspanspan-idstep_3__install_windows_on_the_sharks_cove_boardspanspan-idstep_3__install_windows_on_the_sharks_cove_boardspanstep-3-install-windows-on-the-sharks-cove-board"></a><span id="Step_3__Install_Windows_on_the_Sharks_Cove_board"></span><span id="step_3__install_windows_on_the_sharks_cove_board"></span><span id="STEP_3__INSTALL_WINDOWS_ON_THE_SHARKS_COVE_BOARD"></span>步骤 3：在 Sharks Cove 板上安装 Windows


可以在 Sharks Cove 板上安装以下 Windows 版本之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Windows_Embedded_8.1_Industry_Pro_Evaluation"></span><span id="windows_embedded_8.1_industry_pro_evaluation"></span><span id="WINDOWS_EMBEDDED_8.1_INDUSTRY_PRO_EVALUATION"></span>Windows Embedded 8.1 Industry Pro 评估版</p></td>
<td align="left"><p>这是 180 天的免费试用版。 我们将其称为评估版。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Windows_Embedded_8.1_Industry_Pro_with_Update__x86__-_DVD"></span><span id="windows_embedded_8.1_industry_pro_with_update__x86__-_dvd"></span><span id="WINDOWS_EMBEDDED_8.1_INDUSTRY_PRO_WITH_UPDATE__X86__-_DVD"></span>Windows Embedded 8.1 Industry Pro with Update (x86) - DVD</p></td>
<td align="left"><p>这需要订阅。 我们将其称为完整版。</p></td>
</tr>
</tbody>
</table>



若要安装评估版，请阅读对许可协议进行的以下修正：

**面向硬件开发人员计划的评估软件许可条款修正**

如果使用此软件是为了支持硬件开发人员计划，则以下条款将适用：

-   你同意 Windows Embedded 8.1 Industry Pro 的 Microsoft 评估软件许可条款（简称“评估软件许可条款”）的全部条款，以下条款除外：
    -   经过部分修正的评估软件许可条款 的 1.b. 部分（演示权限），如：
        -   你可能会出于一些合理必要的演示目的，通过使用软件（“演示设备”）向潜在客户演示或交付由你开发的可用于演示的 Windows Embedded 8.1 Industry Pro 设备。 可以向客户演示和交付演示设备，他们无需履行保密义务。
    -   1\.b. 部分中与 上述已修正部分不直接冲突的所有条款都将适用。
-   **使用该软件即表示你接受这些条款。** 如果不接受并且不遵守这些条款，则不得使用该软件或其功能。

下载 [Windows Embedded 8.1 Industry (x86) Pro 评估版](https://go.microsoft.com/fwlink/p?linkid=403173)或 Windows Embedded 8.1 Industry Pro with Update (x86) - DVD。
查找下载的文件。 例如，

9600.17050.WINBLUE\_REFRESH...X86FRE\_EN-US\_DV9.ISO。

创建一个将作为 Sharks Cove 安装程序文件的根的文件夹（例如，C:\\SharksCoveWindows）。 我们将此文件夹称为 *Root*。 在 *Root* 中，创建以下子文件夹：

-   安装
-   SharksCoveBsp

双击 ISO 文件，并将以下文件复制到 *Root*\\Setup。

-   启动
-   Efi
-   源
-   支持
-   Autorun.inf
-   Bootmgr
-   Bootmgr.efi
-   Setup.exe

**注意**  如果运行的是 Windows 7，请右键单击 ISO 文件，然后选择“刻录磁盘映像”  。 将映像刻录到可录制 DVD。 然后，将文件从 DVD 复制到 *Root*\\Setup。



在[此处](https://go.microsoft.com/fwlink/p?linkid=506954)获取 Sharks Cove 板支持包 (BSP)。 将该包中的所有文件都复制到 *Root*\\SharksCoveBsp 中。

在[此处](https://go.microsoft.com/fwlink/p/?linkid=403174)获取 WDK 开发板加载项工具包。 打开“SourceCode”  选项卡。单击“下载”（不是“下载”选项卡），获取工具包脚本。  打开 Scripts 文件夹，然后将以下两项复制到 *Root* 中。

-   Create-DevboardImage.ps1
-   DevBoard 文件夹

**注意**  DevBoard 文件夹包含多个脚本和模块（DevboardImage.ps1、Devboard.psm1、enable-telnet.ps1，等等）。



以管理员身份打开命令提示符窗口，并输入 **Powershell**。 导航至 *Root*。 若要将 BSP 添加到 Windows 映像中，请输入以下命令之一：

如果使用的是 Windows 的评估版，则输入以下命令：

``` syntax
.\Create-DevboardImage -SourcePath Setup\sources\install.wim -Index 2 -BspManifest SharksCoveBsp\SharksCoveBsp.xml
```

如果使用的是 Windows 的完整版，则输入以下命令：

``` syntax
.\Create-DevboardImage -SourcePath Setup\sources\install.wim -Index 1 -BspManifest SharksCoveBsp\SharksCoveBsp.xml
```

**注意**  可能需要先设置执行策略，然后才能运行 **Create-DevboardImage** 脚本。 例如：



``` syntax
Set-ExecutionPolicy -ExecutionPolicy Unrestricted
```

将 BSP 添加到 Windows 映像中后，即可将这些文件夹和文件从 *Root*\\Setup 复制到 U 盘 (FAT32)。

-   启动
-   Efi
-   源
-   支持
-   Autorun.inf
-   Bootmgr
-   Bootmgr.efi
-   Setup.exe

设置 Sharks Cove 硬件，如下所示：

![开发板和连接件的图片](images/sharkscoveconnections03.png)

将该 U 盘插入连接到 Sharks Cove 板的集线器。 启动或重启 Sharks Cove 板时，请按住增大音量按钮。 增大音量按钮是开发板左侧的一组三个按钮中最顶端的按钮，如上图所示。 （如果开发板已启动，可以按住电源按钮几秒钟将其关闭。）当开发板启动时，将在屏幕上看到 EFI shell。

**注意**  可能需要导航到 EFI Shell。 转到  “引导管理器”&gt;“EFI Internal Shell”。



请记下 U 盘的名称（例如，**fs1**:）。

（在此处，我们将使用 **fs1**: 作为 U 盘的名称。）在 **Shell&gt;** 提示符下，输入以下命令：

**fs1:** 
**cd efi\\boot**
**dir** 验证 bootia32.efi 是否在目录中。 输入此命令：

**bootia32.efi** 按照屏幕上的 Windows 设置说明进行操作。

## <a name="span-idstep_4__provision_the_sharks_cove_board_for_driver_deployment_and_testingspanspan-idstep_4__provision_the_sharks_cove_board_for_driver_deployment_and_testingspanspan-idstep_4__provision_the_sharks_cove_board_for_driver_deployment_and_testingspanstep-4-provision-the-sharks-cove-board-for-driver-deployment-and-testing"></a><span id="Step_4__Provision_the_Sharks_Cove_board_for_driver_deployment_and_testing"></span><span id="step_4__provision_the_sharks_cove_board_for_driver_deployment_and_testing"></span><span id="STEP_4__PROVISION_THE_SHARKS_COVE_BOARD_FOR_DRIVER_DEPLOYMENT_AND_TESTING"></span>步骤 4：预配 Sharks Cove 板，以便进行驱动程序部署和测试


预配  是配置计算机以便进行自动驱动程序部署、测试和调试的过程。

设置硬件，如下所示。

![带有连接件的开发板预配图片](images/sharkscoveconnections02.png)

预配 Sharks Cove 板类似于预配任何其他计算机。 若要预配 Sharks Cove 板，请参阅以下主题中的说明：

-   [预配计算机以便进行驱动程序开发和测试 (WDK 8.1)](provision-a-target-computer-wdk-8-1.md)

另请参阅在线提供的以及在 debugger.chm 中提供的以下主题：

-   [Setting up Kernel-Mode Debugging using Serial over USB in Visual Studio](https://go.microsoft.com/fwlink/p?linkid=400460)（在 Visual Studio 中使用 Serial over USB 设置内核模式调试）

**注意**  在预配 Sharks Cove 板之前，需要禁用“安全启动”。 重启 Sharks Cove 板。 在开发板重启时，按住增大音量按钮。 转到  “设备管理器”&gt;“系统设置”&gt;“启动”。 将“UEFI 安全启动”  设置为“禁用”  。



## <a name="span-idstep_5__write_a_software_driver_for_the_sharks_cove_boardspanspan-idstep_5__write_a_software_driver_for_the_sharks_cove_boardspanspan-idstep_5__write_a_software_driver_for_the_sharks_cove_boardspanstep-5-write-a-software-driver-for-the-sharks-cove-board"></a><span id="Step_5__Write_a_software_driver_for_the_Sharks_Cove_board"></span><span id="step_5__write_a_software_driver_for_the_sharks_cove_board"></span><span id="STEP_5__WRITE_A_SOFTWARE_DRIVER_FOR_THE_SHARKS_COVE_BOARD"></span>步骤 5：编写 Sharks Cove 板的软件驱动程序


编写 Sharks Cove 板的设备驱动程序之前，最好先通过编写软件驱动程序自行熟悉驱动程序开发工具。 该过程类似于编写任何其他目标计算机的软件驱动程序。 开始时，请按照此处的实例练习进行操作：

-   [编写第一个驱动程序](writing-your-first-driver.md)

## <a name="span-idstep_6__alter_the_secondary_system_description_table__ssdt_spanspan-idstep_6__alter_the_secondary_system_description_table__ssdt_spanspan-idstep_6__alter_the_secondary_system_description_table__ssdt_spanstep-6-alter-the-secondary-system-description-table-ssdt"></a><span id="Step_6__Alter_the_Secondary_System_Description_Table__SSDT_"></span><span id="step_6__alter_the_secondary_system_description_table__ssdt_"></span><span id="STEP_6__ALTER_THE_SECONDARY_SYSTEM_DESCRIPTION_TABLE__SSDT_"></span>步骤 6：更改辅助系统描述表 (SSDT)


若要为连接到 Sharks Cove 板上的简单外设总线 (SPB) 的设备编写驱动程序，需更新 Sharks Cove 固件中的辅助系统描述表 (SSDT)。 相关示例是为通过 I2C 总线传输数据并通过通用 I/O (GPIO) 引脚生成中断的加速计编写驱动程序。 有关详细信息，请参阅 [Simple Peripheral Buses](https://go.microsoft.com/fwlink/p?linkid=399232)（简单外设总线）。

下面是更改 SSDT 的示例。 我们将为 [ADXL345](https://go.microsoft.com/fwlink/p?linkid=401463) 加速计添加一个表条目。

**注意**  有关 [SpbAccelerometer 示例驱动程序](https://go.microsoft.com/fwlink/p?linkid=506965)和 ADXL345 加速计的分步指南，请参阅 [SpbAccelerometer driver cookbook](https://docs.microsoft.com/windows-hardware/drivers/sensors/spbaccelerometer-driver-cookbook)（SpbAccelerometer 驱动程序指南）。



1.  将 x86 版本的 ASL.exe 复制到 Sharks Cove 板。 ASL.exe 包括在 WDK 中。

    示例：C:\\Program Files (x86)\\Windows Kits\\8.1\\Tools\\x86\\ACPIVerify\\ASL.exe

2.  以管理员身份打开命令提示符窗口。 通过输入以下命令反编译 SSDT：

    **asl /tab=ssdt**

    这将创建 Ssdt.asl 文件。

3.  打开 Ssdt.asl（例如，在记事本中打开）。

    ``` syntax
    DefinitionBlock("SSDT.AML", "SSDT", 0x01, "Intel_", "ADebTabl", 0x00001000)
    {
        Scope()
        {
            Name(DPTR, 0x3bf2d000)
            Name(EPTR, 0x3bf3d000)
            Name(CPTR, 0x3bf2d010)
            Mutex(MMUT, 0x0)
            Method(MDBG, 0x1, Serialized)
            {
                Store(Acquire(MMUT, 0x3e8), Local0)
                If(LEqual(Local0, Zero))
                {
                    OperationRegion(ABLK, SystemMemory, CPTR, 0x10)
                    Field(ABLK, ByteAcc, NoLock, Preserve)
                    {
                        AAAA, 128
                    }
                    Store(Arg0, AAAA)
                    Add(CPTR, 0x10, CPTR)
                    If(LNot(LLess(CPTR, EPTR)))
                    {
                        Add(DPTR, 0x10, CPTR)
                    }
                    Release(MMUT)
                }
                Return(Local0)
            }
        }

        // Insert a Scope(_SB_) and a Device entry here.

    }
    ```

4.  插入 Scope(\_SB\_) 条目。 在 Scope 条目内，插入你自己的 Device 条目。 例如，下面是 ADXL345 加速计的 scope(\_SB\_) 条目和 Device 条目。

    ``` syntax
    Scope(_SB_)
    {
        Device(SPBA)
        {
            Name(_HID, "SpbAccelerometer")
            Name(_UID, 1)



        Method(_CRS, 0x0, NotSerialized)
        {
            Name(RBUF, ResourceTemplate()
            {          
                I2CSerialBus(0x53, ControllerInitiated, 400000, AddressingMode7Bit, "\\_SB.I2C3", 0, ResourceConsumer) 
                GpioInt(Edge, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPO2") {0x17}
            })

            Return(RBUF)
        }


        Method(_DSM, 0x4, NotSerialized)
        {
            If(LEqual(Arg0, Buffer(0x10)
            {
                0x1e, 0x54, 0x81, 0x76, 0x27, 0x88, 0x39, 0x42, 0x8d, 0x9d, 0x36, 0xbe, 0x7f, 0xe1, 0x25, 0x42
            }))
            {
                If(LEqual(Arg2, Zero))
                {
                    Return(Buffer(One)
                    {
                        0x03
                    })
                }

                If(LEqual(Arg2, One))
                {
                    Return(Buffer(0x4)
                    {
                        0x00, 0x01, 0x02, 0x03
                    })
                }
            }
            Else
            {
                Return(Buffer(One)
                {
                    0x00
                })
            }
        } // Method(_DSM ...)

    } // Device(SPBA)

} // Scope(_SB_)
```

在此示例中，`ResourceTemplate()` 下的条目指定加速计需要两个硬件资源：特定 I2C 总线控制器 (I2C3) 的连接 ID 和 GPIO 中断。 中断使用名为 GPO2 的 GPIO 控制器上的引脚 0x17。


5.  将自己的 Device 条目添加到 Ssdt.asl 之后，通过输入以下命令编译 Ssdt.asl：

    **asl ssdt.asl**

    这会将编译的输出放置在名为 Ssdt.aml 的文件中。

6.  验证是否已为 Sharks Cove 板启用测试签名。

    **注意**  测试签名将在预配期间自动启用。




在 Sharks Cove 板上，以管理员身份打开命令提示符窗口。 输入此命令：

**bcdedit /enum {current}**

验证是否可以在输出中看到 `testsigning Yes`。

``` syntax
Windows Boot Loader
-------------------
identifier              {current}
...
testsigning             Yes
...
```

如果需要手动启用测试签名，请参照以下步骤：

1.  以管理员身份打开命令提示符窗口，并输入此命令：

    **bcdedit /set TESTSIGNING ON**

2.  重启 Sharks Cove 板。 在开发板重启时，按住增大音量按钮。 转到  “设备管理器”&gt;“系统设置”&gt;“启动”。 将“UEFI 安全启动”  设置为“禁用”  。
3.  保存更改并继续启动到 Windows。


7.  若要加载已更新的 SSDT，请以管理员身份打开命令提示符窗口，并输入此命令：

    **asl /loadtable ssdt.aml**

    重启 Sharks Cove 板。

## <a name="span-idstep_7__connect_your_device_to_the_sharks_cove_boardspanspan-idstep_7__connect_your_device_to_the_sharks_cove_boardspanspan-idstep_7__connect_your_device_to_the_sharks_cove_boardspanstep-7-connect-your-device-to-the-sharks-cove-board"></a><span id="Step_7__Connect_your_device_to_the_Sharks_Cove_board"></span><span id="step_7__connect_your_device_to_the_sharks_cove_board"></span><span id="STEP_7__CONNECT_YOUR_DEVICE_TO_THE_SHARKS_COVE_BOARD"></span>步骤 7：将设备连接到 Sharks Cove 板


在[此处](https://go.microsoft.com/fwlink/p?linkid=506966)获取 Sharks Cove 端头和引脚的规格。

使用该规格确定要用于你的设备的引脚。 例如，假设你想要将 ADXL345 加速计连接到 I2C 总线。 在该规格中，可以看到 J1C1 头具有所需的引脚。 下面是要在 J1C1 头上使用的一些（但不是全部）引脚。

| Pin | 引脚名称        | 备注                            | ACPI 对象      |
|-----|-----------------|-------------------------------------|------------------|
| 7   | GPIO\_S5\[23\]  | 加速计中断信号      | \_SB.GPO2 {0x17} |
| 13  | SIO\_I2C2\_DATA | I2C 控制器 2 的 I2C 数据线  | \_SB.I2C3        |
| 15  | SIO\_I2C2\_CLK  | I2C 控制器 2 的 I2C 时钟线 | \_SB.I2C3        |



请注意与 SSDT 中的 Device 条目的关系。

``` syntax
I2CSerialBus(... "\\_SB.I2C3", , )
GpioInt(... "\\_SB.GPO2") {0x17}
```

## <a name="span-idstep_8__write__build__and_deploy_a_driver_for_your_devicespanspan-idstep_8__write__build__and_deploy_a_driver_for_your_devicespanspan-idstep_8__write__build__and_deploy_a_driver_for_your_devicespanstep-8-write-build-and-deploy-a-driver-for-your-device"></a><span id="Step_8__Write__build__and_deploy_a_driver_for_your_device"></span><span id="step_8__write__build__and_deploy_a_driver_for_your_device"></span><span id="STEP_8__WRITE__BUILD__AND_DEPLOY_A_DRIVER_FOR_YOUR_DEVICE"></span>步骤 8：为设备编写、构建和部署驱动程序


为 Sharks Cove 板编写设备驱动程序类似于为任何其他计算机编写设备驱动程序。 在 Visual Studio 中，可以从驱动程序模板开始，也可以从驱动程序示例开始。

准备好测试 Sharks Cove 板上的驱动程序时，请执行以下步骤：

1.  在主机上的 Visual Studio 中，右键单击程序包项目，然后选择“属性”  。 转到  “驱动程序安装”&gt;“部署”。 选中“启用部署”  和“部署前删除以前的驱动程序版本”  。 对于“目标计算机名称”  ，请选择 Sharks Cove 板的名称。 选择“安装并验证”  。
2.  继续在属性页中转到  “驱动程序签名”&gt;“常规”。 对于“签名模式”  ，请选择“测试签名”  。 单击“确定”  。
3.  在驱动程序项目中，打开 INF 文件。 编辑硬件 ID，使其与在 SSDT 中创建的硬件 ID (\_HID) 匹配。 例如，假设将此 Device 条目置于 SSDT 中，

    ``` syntax
    Device(SPBA)
    {
       Name(_HID, "SpbAccelerometer")
       ...
    ```

    则 INF 文件中的硬件 ID 将为 ACPI\\SpbAccelerometer。

    ``` syntax
    [Standard.NT$ARCH$]
    %KMDFDriver1.DeviceDesc%=KMDFDriver1_Device, ACPI\SpbAccelerometer
    ```

4.  在 Visual Studio 的“调试”  菜单上，选择“开始调试”  。
5.  Microsoft Visual Studio 首先在“输出”  窗口中显示进度。 然后，它将打开“调试程序即时窗口”  并继续显示进度。

    等待至已在 Sharks Cove 板上部署、安装和加载驱动程序。 此操作可能需一到两分钟。

6.  如果调试程序未自动强行进入，请从“调试”  菜单中选择“全部中断”  。 主计算机上的调试程序将强行进入目标计算机（内核模式）或 Wudfhost.exe (UMDF) 的正确实例。 在“调试程序即时窗口”  中，会看到调试程序命令提示符。

7.  若要查看已加载的模块，请输入 **lm**。 验证驱动程序是否出现在已加载模块的列表中。

## <a name="span-idusing_windbg_to_debug_the_sharks_cove_boardspanspan-idusing_windbg_to_debug_the_sharks_cove_boardspanspan-idusing_windbg_to_debug_the_sharks_cove_boardspanusing-windbg-to-debug-the-sharks-cove-board"></a><span id="Using_WinDbg_to_debug_the_Sharks_Cove_board"></span><span id="using_windbg_to_debug_the_sharks_cove_board"></span><span id="USING_WINDBG_TO_DEBUG_THE_SHARKS_COVE_BOARD"></span>使用 WinDbg 调试 Sharks Cove 板


作为使用 Visual Studio 设置内核模式调试的替代方法，你还可以手动完成设置。 将在线提供或在 debugger.chm 中提供该主题。

-   [Setting up Kernel-Mode Debugging using Serial over USB Manually](https://go.microsoft.com/fwlink/p?linkid=400461)（使用 Serial over USB 手动设置内核模式调试）

作为使用 Visual Studio 进行调试的替代方法，你还可以使用 WinDbg。

无论使用的是 Visual Studio 还是 WinDbg，以下实例指南都有助于学习调试程序命令：

-   [Getting Started with WinDbg (User-Mode)](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windbg)（WinDbg 入门（用户模式））
-   [Getting Started with WinDbg (Kernel-Mode)](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windbg--kernel-mode-)（WinDbg 入门（内核模式））

## <a name="span-idsample_driver_codespanspan-idsample_driver_codespanspan-idsample_driver_codespansample-driver-code"></a><span id="Sample_driver_code"></span><span id="sample_driver_code"></span><span id="SAMPLE_DRIVER_CODE"></span>示例驱动程序代码


-   [SpbAccelerometer 示例驱动程序（UMDF 版本 1）](https://go.microsoft.com/fwlink/p?linkid=506965)

## <a name="span-idunderstanding_simple_peripheral_busesspanspan-idunderstanding_simple_peripheral_busesspanspan-idunderstanding_simple_peripheral_busesspanunderstanding-simple-peripheral-buses"></a><span id="Understanding_simple_peripheral_buses"></span><span id="understanding_simple_peripheral_buses"></span><span id="UNDERSTANDING_SIMPLE_PERIPHERAL_BUSES"></span>了解简单外设总线


若要了解 Windows 驱动程序如何与简单外设总线协同工作，请参阅 [Simple Peripheral Buses](https://go.microsoft.com/fwlink/p?linkid=399232)（简单外设总线）。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[SharksCove.org](https://go.microsoft.com/fwlink/p?linkid=403167)

[用于所有驱动程序开发人员的概念](https://go.microsoft.com/fwlink/p/?linkid=399233)

[开发、测试以及部署驱动程序](https://go.microsoft.com/fwlink/p/?linkid=399234)

[Windows 驱动程序框架](https://go.microsoft.com/fwlink/p/?linkid=399235)

[Windows 硬件开发人员中心](https://go.microsoft.com/fwlink/p/?linkid=8703)

[适用于 Windows 的 WDK 示例](https://go.microsoft.com/fwlink/p?linkid=394031)

[Windows 硬件和驱动程序开发人员社区](https://go.microsoft.com/fwlink/p?linkid=393983)

[技术支持](https://go.microsoft.com/fwlink/p/?linkid=8713)










