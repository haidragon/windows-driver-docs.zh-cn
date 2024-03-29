---
title: WinDbg 入门（用户模式）
description: WinDbg 是 Windows 调试工具中包含的内核模式和用户模式调试器。 在这里, 我们将提供练习, 帮助你开始使用 WinDbg 作为用户模式调试器。
ms.assetid: 8C2D2D0C-7E54-4711-A6FD-970E040F1C50
ms.date: 10/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9d140c4eddf12fce29b7eba6b1c7df3c70df03
ms.sourcegitcommit: b3167f0d423713bee9561fabbdb3d581aea449f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2019
ms.locfileid: "68616812"
---
# <a name="getting-started-with-windbg-user-mode"></a>WinDbg 入门（用户模式）

WinDbg 是 Windows 调试工具中包含的内核模式和用户模式调试器。 在这里, 我们将提供练习, 帮助你开始使用 WinDbg 作为用户模式调试器。

有关如何获取 Windows 调试工具的信息, 请参阅[适用于 windows 的调试工具 (WinDbg、KD、CDB、NTSD)](https://go.microsoft.com/fwlink/p?linkid=223405)。 

安装调试工具后, 找到64位 (x64) 和32位 (x86) 版本的工具的安装目录。 例如：

-   C:\\Program Files (x86)\\Windows 工具包\\8.1\\调试器\\x64
-   C:\\Program Files (x86)\\Windows 工具包\\8.1\\调试器\\x86

## <a name="span-idlaunchnotepadandattachwindbgspanspan-idlaunchnotepadandattachwindbgspanspan-idlaunchnotepadandattachwindbgspanlaunch-notepad-and-attach-windbg"></a><span id="Launch_Notepad_and_attach_WinDbg"></span><span id="launch_notepad_and_attach_windbg"></span><span id="LAUNCH_NOTEPAD_AND_ATTACH_WINDBG"></span>启动记事本并附加 WinDbg

1.  导航到您的安装目录, 然后打开 WinDbg。

2.  [此处](https://go.microsoft.com/fwlink/p?linkid=223405)还提供了调试器文档。

3.  在 "**文件**" 菜单上, 选择 "**打开可执行**文件"。 在 "打开可执行文件" 对话框中, 导航到包含 notepad.exe 的文件夹 (例如, C:\\Windows\\System32)。 对于 "**文件名**", 请输入 notepad.exe。 单击“打开” 。

    ![启动记事本后的 windbg 屏幕截图](images/windbggetstart01.png)

4.  在 "WinDbg" 窗口底部附近的命令行中, 输入以下命令:

    [。 sympath srv\*](https://go.microsoft.com/fwlink/p?linkid=399238)

    输出类似于以下内容:

    ```dbgcmd
    Symbol search path is: srv*
    Expanded Symbol search path is: cache*;SRV
    ```

    符号搜索路径指示 WinDbg 查找符号 (PDB) 文件的位置。 调试器需要符号文件来获取有关代码模块的信息 (函数名、变量名和 like)。

    输入此命令, 该命令会告诉 WinDbg 完成符号文件的初始查找和加载:

    [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)

5.  若要查看 Notepad.exe 模块的符号, 请输入以下命令:

    [x 记事本! *](https://go.microsoft.com/fwlink/p?linkid=399240)

    **注意如果看**不到任何输出, 请输入[ **。重新加载**](https://go.microsoft.com/fwlink/p?linkid=399239)。  

    若要查看 Notepad.exe 模块中包含 main 的符号, 请输入以下命令:

    [x 记事本!\*main\*](https://go.microsoft.com/fwlink/p?linkid=399240)
 
    输出类似于以下内容:

    ```dbgcmd
    000000d0`428ff7e8 00007ff6`3282122f notepad!WinMain
    ...
    ```

6.  在记事本中放置断点!WinMain, 请输入以下命令:

    [bu 记事本!WinMain](https://go.microsoft.com/fwlink/p?linkid=399390)

    若要验证是否已设置断点, 请输入以下命令:

    [bl](https://go.microsoft.com/fwlink/p?linkid=399391)

    输出类似于以下内容:

    ```dbgcmd
    0 e 00007ff6`32825f64     0001 (0001)  0:**** notepad!WinMain
    ```

7.  若要启动记事本运行, 请输入以下命令:

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

    记事本运行到**WinMain**函数之前, 然后将其中断到调试器。
    ```dbgcmd
    Breakpoint 0 hit
    notepad!WinMain:
    00007ff6`32825f64 488bc4          mov     rax,rsp
    ```

    若要查看记事本进程中加载的代码模块列表, 请输入以下命令:

    [lm](https://go.microsoft.com/fwlink/p?linkid=399237)

    输出类似于以下内容:

    ```dbgcmd
    0:000> lm
    start             end                 module name
    00007ff6`32820000 00007ff6`3285a000   notepad    (pdb symbols)          C:\...\notepad.pdb
    00007ffc`ab7e0000 00007ffc`ab85b000   WINSPOOL   (deferred)             
    00007ffc`aba10000 00007ffc`abc6a000   COMCTL32   (deferred)             
    00007ffc`adea0000 00007ffc`adf3f000   SHCORE     (deferred)             
    00007ffc`af490000 00007ffc`af59f000   KERNELBASE   (deferred)             
    00007ffc`af7d0000 00007ffc`af877000   msvcrt     (deferred)             
    00007ffc`af880000 00007ffc`b0c96000   SHELL32    (deferred)             
    00007ffc`b0e40000 00007ffc`b0ef7000   OLEAUT32   (deferred)             
    00007ffc`b0f00000 00007ffc`b0f57000   sechost    (deferred)             
    00007ffc`b0f60000 00007ffc`b1005000   ADVAPI32   (deferred)             
    00007ffc`b1010000 00007ffc`b1155000   GDI32      (deferred)             
    00007ffc`b1160000 00007ffc`b1296000   RPCRT4     (deferred)             
    00007ffc`b12a0000 00007ffc`b1411000   USER32     (deferred)             
    00007ffc`b1420000 00007ffc`b15f6000   combase    (deferred)             
    00007ffc`b16c0000 00007ffc`b17f9000   MSCTF      (deferred)             
    00007ffc`b1800000 00007ffc`b189a000   COMDLG32   (deferred)             
    00007ffc`b18a0000 00007ffc`b18f1000   SHLWAPI    (deferred)             
    00007ffc`b1b60000 00007ffc`b1cd8000   ole32      (deferred)             
    00007ffc`b1cf0000 00007ffc`b1e2a000   KERNEL32   (pdb symbols)          C:\...\kernel32.pdb
    00007ffc`b1eb0000 00007ffc`b1ee4000   IMM32      (deferred)             
    00007ffc`b1f50000 00007ffc`b20fa000   ntdll      (private pdb symbols)  C:\...\ntdll.pdb
    ```

    若要查看堆栈跟踪, 请输入以下命令:

    [温度](https://go.microsoft.com/fwlink/p?linkid=399389)

    输出类似于以下内容:

    ```dbgcmd
    0:000> k
    Child-SP          RetAddr           Call Site
    00000048`4e0cf6a8 00007ff6`3282122f notepad!WinMain
    00000048`4e0cf6b0 00007ffc`b1cf16ad notepad!WinMainCRTStartup+0x1a7
    00000048`4e0cf770 00007ffc`b1fc4629 KERNEL32!BaseThreadInitThunk+0xd
    00000048`4e0cf7a0 00000000`00000000 ntdll!RtlUserThreadStart+0x1d ...
    ```

8.  若要重新启动记事本, 请输入以下命令:

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

9.  若要中断记事本, 请从 "**调试**" 菜单中选择 "**中断**"。

10. 若要在**ZwWriteFile**上设置和验证断点, 请输入以下命令:

    [bu ntdll.dll!ZwWriteFile](https://go.microsoft.com/fwlink/p?linkid=399390)

    [bl](https://go.microsoft.com/fwlink/p?linkid=399391)

11. 输入[g](https://go.microsoft.com/fwlink/p?linkid=399388) , 再次开始运行记事本。 在记事本窗口中输入一些文本, 然后从 "**文件**" 菜单中选择 "**保存**"。 当涉及**ZwCreateFile**时, 正在运行的代码会中断。 输入[k](https://go.microsoft.com/fwlink/p?linkid=399389)以查看堆栈跟踪。

    ![windbg 中堆栈跟踪的屏幕截图](images/windbggetstart02.png)

    在 WinDbg 窗口中, 在命令行的左侧, 请注意处理器和线程号。 在此示例中, 当前处理器编号为 0, 当前线程号为11。 我们正在查看线程11的堆栈跟踪 (发生在处理器0上的运行)。

12. 若要查看记事本进程中的所有线程列表, 请输入以下命令 (波形符):

    [~](https://go.microsoft.com/fwlink/p?linkid=399392)

    输出类似于以下内容:

    ```dbgcmd
    0:011> ~
       0  Id: 10c8.128c Suspend: 1 Teb: 00007ff6`31cdd000 Unfrozen
       1  Id: 10c8.1a10 Suspend: 1 Teb: 00007ff6`31cdb000 Unfrozen
       2  Id: 10c8.1850 Suspend: 1 Teb: 00007ff6`31cd9000 Unfrozen
       3  Id: 10c8.1774 Suspend: 1 Teb: 00007ff6`31cd7000 Unfrozen
       4  Id: 10c8.1e80 Suspend: 1 Teb: 00007ff6`31cd5000 Unfrozen
       5  Id: 10c8.10ac Suspend: 1 Teb: 00007ff6`31cd3000 Unfrozen
       6  Id: 10c8.13a4 Suspend: 1 Teb: 00007ff6`31bae000 Unfrozen
       7  Id: 10c8.2b4 Suspend: 1 Teb: 00007ff6`31bac000 Unfrozen
       8  Id: 10c8.1df0 Suspend: 1 Teb: 00007ff6`31baa000 Unfrozen
       9  Id: 10c8.1664 Suspend: 1 Teb: 00007ff6`31ba8000 Unfrozen
      10  Id: 10c8.15e4 Suspend: 1 Teb: 00007ff6`31ba6000 Unfrozen
    . 11  Id: 10c8.8bc Suspend: 1 Teb: 00007ff6`31ba4000 Unfrozen
    ```

    在此示例中, 有12个索引为0到11的线程。

13. 若要查看线程0的堆栈跟踪, 请输入以下命令:

    [~ 0](https://go.microsoft.com/fwlink/p?linkid=399393)

    [温度](https://go.microsoft.com/fwlink/p?linkid=399389)

    输出类似于以下内容:

    ```dbgcmd
    0:011> ~0s
    USER32!SystemParametersInfoW:
    00007ffc`b12a4d20 48895c2408      mov     qword ptr [rsp+8], ...
    0:000> k
    Child-SP          RetAddr           Call Site
    00000033`d1e9da48 00007ffc`adfb227d USER32!SystemParametersInfoW
    (Inline Function) --------`-------- uxtheme!IsHighContrastMode+0x1d
    00000033`d1e9da50 00007ffc`adfb2f12 uxtheme!IsThemeActive+0x4d
    ...
    00000033`d1e9f810 00007ffc`b1cf16ad notepad!WinMainCRTStartup+0x1a7
    00000033`d1e9f8d0 00007ffc`b1fc4629 KERNEL32!BaseThreadInitThunk+0xd
    00000033`d1e9f900 00000000`00000000 ntdll!RtlUserThreadStart+0x1d
    ```

14. 若要退出调试并从记事本进程分离, 请输入以下命令:

    [qd](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idlaunchyourownapplicationandattachwindbgspanspan-idlaunchyourownapplicationandattachwindbgspanspan-idlaunchyourownapplicationandattachwindbgspanlaunch-your-own-application-and-attach-windbg"></a><span id="Launch_your_own_application_and_attach_WinDbg"></span><span id="launch_your_own_application_and_attach_windbg"></span><span id="LAUNCH_YOUR_OWN_APPLICATION_AND_ATTACH_WINDBG"></span>启动自己的应用程序并附加 WinDbg


假设你已编写并生成此小型控制台应用程序。

```dbgcmd
...
void MyFunction(long p1, long p2, long p3)
{
    long x = p1 + p2 + p3;
    long y = 0;
    y = x / p2;
}

void main ()
{
    long a = 2;
    long b = 0;
    MyFunction(a, b, 5);
}
```

对于本练习, 我们假定生成的应用程序 (myapp) 和符号文件 (myapp) 在 C:\\MyApp\\x64\\调试中。 我们还会假定应用程序源代码在 C:\\myapp\\myapp 中, 并且目标计算机编译了 MyApp。

1.  打开 WinDbg。

2.  在 "**文件**" 菜单上, 选择 "**打开可执行**文件"。 在 "打开可执行文件" 对话框中, 导航\\到\\C\\: MyApp x64 调试。 对于 "**文件名**", 请输入 myapp.exe。 单击“打开” 。
3.  输入以下命令:

    [.symfix](https://docs.microsoft.com/windows-hardware/drivers/debugger/-symfix--set-symbol-store-path-)

    [. sympath](https://docs.microsoft.com/windows-hardware/drivers/debugger/-sympath--set-symbol-path-)+ C:\\MyApp\\x64\\调试

    现在, WinDbg 知道在何处查找应用程序的符号和源代码。 在这种情况下, 不需要将源代码位置设置为[srcpath](https://docs.microsoft.com/windows-hardware/drivers/debugger/-srcpath---lsrcpath--set-source-path-) , 因为符号具有指向源文件的完全限定路径。

4.  输入以下命令:

    [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)

    [bu MyApp! main](https://go.microsoft.com/fwlink/p?linkid=399390)

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

    当应用程序进入**主**函数时, 应用程序会中断到调试器。

    WinDbg 显示你的源代码和命令窗口。

    ![windbg 中源代码的屏幕截图](images/windbggetstart03.png)

5.  在 "**调试**" 菜单上, 选择 "**单步执行**" (或按**F11**)。 继续单步执行, 直到你逐步进入**MyFunction**。 单步执行此行`y = x / p2`时, 应用程序将崩溃并中断调试器。 输出类似于以下内容:

    ```dbgcmd
    (1450.1424): Integer divide-by-zero - code c0000094 (first chance)
    First chance exceptions are reported before any exception handling.
    This exception may be expected and handled.
    MyApp!MyFunction+0x44:
    00007ff6`3be11064 f77c2428    idiv  eax,dword ptr [rsp+28h] ss:00000063`2036f808=00000000
    ```

6.  输入此命令：

    [! 分析-v](https://go.microsoft.com/fwlink/p?linkid=399396)

    WinDbg 显示问题的分析 (在本例中为 0)。

    ```dbgcmd
    FAULTING_IP: 
    MyApp!MyFunction+44 [c:\myapp\myapp\myapp.cpp @ 7]
    00007ff6`3be11064 f77c2428        idiv    eax,dword ptr [rsp+28h]

    EXCEPTION_RECORD:  ffffffffffffffff -- (.exr 0xffffffffffffffff)
    ExceptionAddress: 00007ff63be11064 (MyApp!MyFunction+0x0000000000000044)
       ExceptionCode: c0000094 (Integer divide-by-zero)
      ExceptionFlags: 00000000
    NumberParameters: 0
    ...
    STACK_TEXT:  
    00000063`2036f7e0 00007ff6`3be110b8 : ... : MyApp!MyFunction+0x44
    00000063`2036f800 00007ff6`3be1141d : ... : MyApp!main+0x38
    00000063`2036f840 00007ff6`3be1154e : ... : MyApp!__tmainCRTStartup+0x19d
    00000063`2036f8b0 00007ffc`b1cf16ad : ... : MyApp!mainCRTStartup+0xe
    00000063`2036f8e0 00007ffc`b1fc4629 : ... : KERNEL32!BaseThreadInitThunk+0xd
    00000063`2036f910 00000000`00000000 : ... : ntdll!RtlUserThreadStart+0x1d

    STACK_COMMAND: dt ntdll!LdrpLastDllInitializer BaseDllName ;dt ntdll!LdrpFailureData ;.cxr 0x0 ;kb

    FOLLOWUP_IP: 
    MyApp!MyFunction+44 [c:\myapp\myapp\myapp.cpp @ 7]
    00007ff6`3be11064 f77c2428        idiv    eax,dword ptr [rsp+28h]

    FAULTING_SOURCE_LINE:  c:\myapp\myapp\myapp.cpp

    FAULTING_SOURCE_FILE:  c:\myapp\myapp\myapp.cpp

    FAULTING_SOURCE_LINE_NUMBER:  7

    FAULTING_SOURCE_CODE:  
         3: void MyFunction(long p1, long p2, long p3)
         4: {
         5:     long x = p1 + p2 + p3;
         6:     long y = 0;
    >    7:  y = x / p2;
         8: }
         9: 
        10: void main ()
        11: {
        12:     long a = 2;
    ...
    ```

## <a name="span-idsummaryofcommandsspanspan-idsummaryofcommandsspanspan-idsummaryofcommandsspansummary-of-commands"></a><span id="Summary_of_commands"></span><span id="summary_of_commands"></span><span id="SUMMARY_OF_COMMANDS"></span>命令摘要


-   "**帮助**" 菜单上的 "**内容**" 命令
-   [. sympath (设置符号路径)](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [。重载 (重载模块)](https://go.microsoft.com/fwlink/p?linkid=399239)
-   [x (检查符号)](https://go.microsoft.com/fwlink/p?linkid=399240)
-   [g (走)](https://go.microsoft.com/fwlink/p?linkid=399388)
-   "**调试**" 菜单上的 "**中断**" 命令
-   [lm (列出加载的模块)](https://go.microsoft.com/fwlink/p?linkid=399237)
-   [k (显示 Stack Backtrace)](https://go.microsoft.com/fwlink/p?linkid=399389)
-   [bu (设置断点)](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [bl (断点列表)](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [~ (线程状态)](https://go.microsoft.com/fwlink/p?linkid=399392)
-   [~ s (设置当前线程)](https://go.microsoft.com/fwlink/p?linkid=399393)
-   [. sympath + (设置符号路径) 追加到现有符号路径](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [srcpath (设置源路径)](https://go.microsoft.com/fwlink/p?linkid=399395)
-   "**调试**" 菜单上的 "**单步**执行" 命令 (**F11**)
-   [! 分析-v](https://go.microsoft.com/fwlink/p?linkid=399396)
-   [qd (退出并分离)](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Getting Started with WinDbg (Kernel-Mode)](getting-started-with-windbg--kernel-mode-.md)（WinDbg 入门（内核模式））

[调试程序操作](https://go.microsoft.com/fwlink/p?linkid=399247)

[调试方法](https://go.microsoft.com/fwlink/p?linkid=399248)

[适用于 Windows 的调试工具 (WinDbg、KD、CDB、NTSD)](https://go.microsoft.com/fwlink/p?linkid=223405)

 

 






