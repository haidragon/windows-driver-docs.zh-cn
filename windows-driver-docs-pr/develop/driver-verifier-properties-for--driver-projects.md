---
ms.assetid: 960368D6-5E24-46B6-83DA-0525065E5FFB
title: 驱动程序包项目的驱动程序验证程序属性
description: 驱动程序验证程序是一款运行时验证工具，用于提高驱动程序测试的有效性。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb1f628118afd80607076e94d3d8ba15915b95de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370742"
---
# <a name="driver-verifier-properties-for-driver-package-projects"></a>驱动程序包项目的驱动程序验证程序属性

[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)是一款运行时验证工具，用于提高驱动程序测试的有效性。 当你部署用于测试的驱动程序时，可以启用驱动程序验证程序并将其配置为在所有测试计算机上运行。

当你启用远程测试计算机上的驱动程序验证程序时，应始终设置与测试计算机的内核模式调试连接。 有关配置目标计算机和设置调试电缆的信息，请参阅[在 Visual Studio 中设置内核模式调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-kernel-mode-debugging-in-visual-studio)。

## <a name="span-idsetting_driver_verifier_properties_for_driver_package_projectsspanspan-idsetting_driver_verifier_properties_for_driver_package_projectsspanspan-idsetting_driver_verifier_properties_for_driver_package_projectsspansetting-driver-verifier-properties-for-driver-package-projects"></a><span id="Setting_Driver_Verifier_properties_for_driver_package_projects"></span><span id="setting_driver_verifier_properties_for_driver_package_projects"></span><span id="SETTING_DRIVER_VERIFIER_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>设置驱动程序包项目的驱动程序验证程序属性


1.  打开驱动程序包的属性页。 在“解决方案资源管理器”中，右键单击驱动程序包项目，并选择“属性”  。
2.  在驱动程序包的属性页中，单击“配置属性”  ，单击“驱动程序安装”  ，然后单击“驱动程序验证程序”  。
3.  选择“启用驱动程序验证”  选项。 选中此选项时，你可以选择要在测试计算机上验证的驱动程序并且还可以选择要使用的[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)选项。

## <a name="span-idproject_configuration_and_platformspanspan-idproject_configuration_and_platformspanspan-idproject_configuration_and_platformspanproject-configuration-and-platform"></a><span id="Project_Configuration_and_Platform"></span><span id="project_configuration_and_platform"></span><span id="PROJECT_CONFIGURATION_AND_PLATFORM"></span>项目配置和平台


配置列表和平台列表可让你为不同项目配置和平台组合应用不同的部署设置。 例如，你可以使用一组调试版本的部署选项将驱动程序部署到一台测试计算机，使用发布版本的部署选项将驱动程序部署到另一台测试计算机。

## <a name="span-idenable_driver_verifierspanspan-idenable_driver_verifierspanspan-idenable_driver_verifierspanenable-driver-verifier"></a><span id="Enable_Driver_Verifier"></span><span id="enable_driver_verifier"></span><span id="ENABLE_DRIVER_VERIFIER"></span>启用驱动程序验证程序


你可以在测试计算机上为计算机上的所有驱动程序、仅为驱动程序项目或为指定的驱动程序列表启用驱动程序验证程序。 例如，你可能想要在堆栈上为特定设备的一组驱动程序启用驱动程序验证程序。

## <a name="span-idverify_driversspanspan-idverify_driversspanspan-idverify_driversspanverify-drivers"></a><span id="Verify_Drivers"></span><span id="verify_drivers"></span><span id="VERIFY_DRIVERS"></span>验证驱动程序


指定要在测试计算机上进行验证的驱动程序。

<span id="All_Drivers"></span><span id="all_drivers"></span><span id="ALL_DRIVERS"></span>**所有驱动程序**  
指定驱动程序验证程序验证远程测试计算机上已安装的所有驱动程序。

<span id="Project_Output"></span><span id="project_output"></span><span id="PROJECT_OUTPUT"></span>**项目输出**  
指定驱动程序验证程序验证远程测试计算机上已安装的驱动程序项目。 这是默认选项。

<span id="Driver_List"></span><span id="driver_list"></span><span id="DRIVER_LIST"></span>**驱动程序列表**  
指定驱动程序验证程序在远程测试计算机上验证的驱动程序或驱动程序列表。 例如，你可以列出与特定设备关联的所有驱动程序。 用二进制文件名称指定驱动程序，如 Driver.sys。 使用分号分隔驱动程序列表。 不支持通配符值，例如 *n\*.sys*。

## <a name="span-iddriver_verifier_standard_flagsspanspan-iddriver_verifier_standard_flagsspanspan-iddriver_verifier_standard_flagsspandriver-verifier-standard-flags"></a><span id="Driver_Verifier_Standard_Flags"></span><span id="driver_verifier_standard_flags"></span><span id="DRIVER_VERIFIER_STANDARD_FLAGS"></span>驱动程序验证程序标准标志


你可以在测试计算机上配置以下驱动程序验证程序选项。

-   [DDI 合规性检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking) (Windows 8)

    当此选项处于活动状态时，驱动程序验证程序将应用一组设备驱动程序接口 (DDI) 规则，以检查驱动程序与操作系统的内核接口之间的交互是否正确。

-   [死锁检测](https://docs.microsoft.com/windows-hardware/drivers/devtest/deadlock-detection)

    当此选项处于活动状态时，驱动程序验证程序将监控驱动程序对旋转锁、互斥体和快速互斥体的使用。 这将检测驱动程序代码是否可能会导致在某个时刻死锁。

-   [DMA 验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/dma-verification)

    当此选项处于活动状态时，驱动程序验证程序将监控驱动程序对直接内存访问 (DMA) 例程的使用。 这将检测 DMA 缓冲器、适配器和映射寄存器的使用是否不正确。

-   [强制 IRQL 检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-irql-checking)

    当此选项处于活动状态时，驱动程序验证程序将通过使可分页代码失效将极端内存压力置于驱动程序上。 如果驱动程序尝试访问错误 IRQL 处的分页内存或持有旋转锁，则驱动程序验证程序将会检测到此行为。

-   [I/O 验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/i-o-verification)

    当此选项处于活动状态时，驱动程序验证程序将通过特殊池分配驱动程序中断请求数据包 (IRP)，并监控驱动程序的 I/O 处理。 这将检测 I/O 例程的使用是否非法或不一致。 此外，驱动程序验证程序还将监控多个 I/O 管理程序例程的调用情况，并对即插即用 (PnP) IRP、电源 IRP 和 WMI IRP 执行压力测试。

-   [其他检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/miscellaneous-checks)

    当此选项处于活动状态时，驱动程序验证程序将查找驱动程序崩溃的常见原因，如空余内存的不当处理等。

-   [池跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/pool-tracking)

    当此选项处于活动状态时，驱动程序验证程序将检查驱动程序在未加载时是否已释放其全部内存分配。 这会揭示内存泄漏。

-   [安全检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/security-checks)

    当此选项处于活动状态时，驱动程序验证程序将查找导致出现安全漏洞的常见错误，如内核模式例程对用户模式地址的引用等。

-   [特殊池检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/special-pool)

    当此选项处于活动状态时，驱动程序验证程序将通过特殊池分配驱动程序的大部分内存请求。 将会监控此特殊池是否存在内存溢出、内存欠载和内存在释放后仍可访问的情况。

## <a name="span-iddriver_verifier_scenario_specific_settingsspanspan-iddriver_verifier_scenario_specific_settingsspanspan-iddriver_verifier_scenario_specific_settingsspandriver-verifier-scenario-specific-settings"></a><span id="Driver_Verifier_Scenario_Specific_Settings"></span><span id="driver_verifier_scenario_specific_settings"></span><span id="DRIVER_VERIFIER_SCENARIO_SPECIFIC_SETTINGS"></span>驱动程序验证程序场景特定设置


-   [资源不足模拟](https://docs.microsoft.com/windows-hardware/drivers/devtest/low-resources-simulation)

    当此选项处于活动状态时，驱动程序验证程序将会随机地让池分配请求和其他资源请求失败。 通过将这些分配故障注入到系统中，驱动程序验证程序可以测试驱动程序处理资源不足情况的能力。

-   [强制挂起 I/O 请求](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-pending-i-o-requests)

    当此选项处于活动状态时，驱动程序验证程序将检测驱动程序对 STATUS\_PENDING 返回值的响应，方法是为对 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) 的随机调用返回 STATUS\_PENDING。

-   [IRP 日志记录](https://docs.microsoft.com/windows-hardware/drivers/devtest/irp-logging)

    当此选项处于活动状态时，驱动程序验证程序将监控驱动程序对 IRP 的使用情况并创建一份 IRP 使用日志。

-   [面向堆栈的固定 MDL 检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-stack) (Windows 8)

    [面向堆栈的固定 MDL 检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-stack)选项用于监控驱动程序如何处理驱动程序堆栈中的固定 MDL 缓冲区。 驱动程序验证程序可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，必须在至少一个驱动程序上启用 I/O 验证。

-   [面向驱动程序的固定 MDL 检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-driver) (Windows 8)

    [面向驱动程序的固定 MDL 检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-driver)选项用于监控每个驱动程序是如何处理固定 MDL 缓冲区的。 此选项可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，你必须在至少一个驱动程序上启用 I/O 验证。

-   [Power 框架延迟模糊处理](https://docs.microsoft.com/windows-hardware/drivers/devtest/concurrency-stress-test) (Windows 8)

    当此选项处于活动状态时，驱动程序验证程序将随机化线程计划，以帮助消除驱动程序中的并发错误。

-   [基于堆栈的故障注入](https://docs.microsoft.com/windows-hardware/drivers/devtest/stack-based-failure-injection) (Windows 8)

    [基于堆栈的故障注入](https://docs.microsoft.com/windows-hardware/drivers/devtest/stack-based-failure-injection)选项用于将资源故障注入内核模式驱动程序中。 此选项结合使用了特殊驱动程序 KmAutoFail.sys 和[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)来侵入驱动程序错误处理路径。

    **注意**  不能将[基于堆栈的故障注入](https://docs.microsoft.com/windows-hardware/drivers/devtest/stack-based-failure-injection)和[资源不足模拟](https://docs.microsoft.com/windows-hardware/drivers/devtest/low-resources-simulation)组合使用。

     

## <a name="span-iddriver_verifier_options_that_require_i_o_verificationspanspan-iddriver_verifier_options_that_require_i_o_verificationspanspan-iddriver_verifier_options_that_require_i_o_verificationspandriver-verifier-options-that-require-io-verification"></a><span id="Driver_Verifier_options_that_require_I_O_Verification"></span><span id="driver_verifier_options_that_require_i_o_verification"></span><span id="DRIVER_VERIFIER_OPTIONS_THAT_REQUIRE_I_O_VERIFICATION"></span>需要 I/O 验证的驱动程序验证程序选项


有四个选项需要你先启用 [I/O 验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/i-o-verification)。 如果未启用 I/O 验证，则无法启用这些选项。

-   [强制挂起 I/O 请求](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-pending-i-o-requests)
-   [IRP 日志记录](https://docs.microsoft.com/windows-hardware/drivers/devtest/irp-logging)
-   [面向堆栈的固定 MDL 检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-stack)
-   [面向驱动程序的固定 MDL 检查](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-driver)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)
* [如何使用 Visual Studio 在运行时测试驱动程序](testing-a-driver-at-runtime.md)
* [在 Visual Studio 中设置内核模式调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-kernel-mode-debugging-in-visual-studio)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
 

 






