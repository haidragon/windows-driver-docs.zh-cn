---
title: 对象句柄
description: 对象句柄
ms.assetid: deeeb3c0-54e4-4727-ac43-6da79be515d7
keywords:
- 对象将处理 WDK 用户模式
- 对象句柄 WDK 内核
- 句柄 WDK 用户模式
- 句柄 WDK 内核
- 私有对象句柄 WDK
- 共享的对象句柄 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0efc0ac43ed1430734c2f5d1a1f6f69ba6a9efa4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385997"
---
# <a name="object-handles"></a>对象句柄





驱动程序和用户模式组件访问大多数系统定义的对象，通过*句柄*。 由句柄不透明的数据类型表示句柄。 （请注意句柄不用于访问设备对象或驱动程序对象。）

对于大多数对象类型，创建或打开该对象的内核模式例程提供给调用方的句柄。 然后，调用方对象上的后续操作中使用该句柄。

下面是一系列对象类型的驱动程序通常使用，并提供指向该类型的对象的句柄的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对象类型</th>
<th>相应的创建/打开例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文件</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile" data-raw-source="[&lt;strong&gt;IoCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)"><strong>IoCreateFile</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)"> <strong>ZwCreateFile</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile" data-raw-source="[&lt;strong&gt;ZwOpenFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)"> <strong>ZwOpenFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>注册表项</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey" data-raw-source="[&lt;strong&gt;IoOpenDeviceInterfaceRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)"><strong>IoOpenDeviceInterfaceRegistryKey</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey" data-raw-source="[&lt;strong&gt;IoOpenDeviceRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)"> <strong>IoOpenDeviceRegistryKey</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)"> <strong>ZwCreateKey</strong></a>，<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)"> <strong>ZwOpenKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>线程</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread" data-raw-source="[&lt;strong&gt;PsCreateSystemThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)"><strong>PsCreateSystemThread</strong></a></p></td>
</tr>
<tr class="even">
<td><p>Events</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesynchronizationevent" data-raw-source="[&lt;strong&gt;IoCreateSynchronizationEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesynchronizationevent)"><strong>IoCreateSynchronizationEvent</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatenotificationevent" data-raw-source="[&lt;strong&gt;IoCreateNotificationEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatenotificationevent)"> <strong>IoCreateNotificationEvent</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>符号链接</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensymboliclinkobject" data-raw-source="[&lt;strong&gt;ZwOpenSymbolicLinkObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensymboliclinkobject)"><strong>ZwOpenSymbolicLinkObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>目录对象</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject" data-raw-source="[&lt;strong&gt;ZwCreateDirectoryObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)"><strong>ZwCreateDirectoryObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>部分对象</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection" data-raw-source="[&lt;strong&gt;ZwOpenSection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)"><strong>ZwOpenSection</strong></a></p></td>
</tr>
</tbody>
</table>

 

当驱动程序不再需要对对象的访问时，它将调用[ **ZwClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)例程，以关闭句柄。 这适用于所有上述表中列出的对象类型。

提供句柄的例程的大多数采取[**对象\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_object_attributes)结构作为参数。 此结构可用于指定句柄的属性。

驱动程序可以指定以下的句柄属性：

-   OBJ\_KERNEL\_HANDLE

    仅可以从内核模式下访问该句柄。

-   OBJ\_继承

    在创建时，当前进程的任何子级将收到一份句柄。

-   OBJ\_FORCE\_访问\_检查

    此属性指定在系统执行句柄上的所有访问权限检查。 默认情况下，系统会绕过对句柄在内核模式下创建的所有访问权限检查。

使用[ **InitializeObjectAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes)例程中设置这些属性**对象\_特性**结构。

有关验证对象句柄的信息，请参阅[验证对象句柄失败](failure-to-validate-object-handles.md)。

### <a name="private-object-handles"></a>私有对象句柄

每当一个驱动程序创建供其专用对象句柄，该驱动程序必须指定 OBJ\_内核\_句柄属性。 这可确保该句柄都无法访问用户模式应用程序。

### <a name="shared-object-handles"></a>共享对象句柄

必须仔细编写共享内核模式和用户模式之间的对象句柄的驱动程序，以避免意外创建的安全漏洞。 以下是一些准则：

1.  在内核模式下创建句柄并将其传递给用户模式下，而不是在相反方向。 句柄创建的用户模式组件，传递给驱动程序不应为受信任。

2.  如果该驱动程序必须处理代表用户模式应用程序的句柄，则使用 OBJ\_FORCE\_访问\_检查属性以验证该应用程序具有必要的访问权限。

3.  使用[ **ObReferenceObjectByPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)将保留在共享的句柄上的内核模式引用。 否则为如果用户模式组件关闭句柄，引用计数变为零，并且系统如果驱动程序然后尝试使用或关闭句柄将崩溃。

如果在用户模式应用程序创建一个事件对象，则驱动程序可以安全地等待该事件收到信号，但仅当应用程序将句柄传递到通过 IOCTL 驱动程序的事件对象。 该驱动程序必须处理的进程创建事件，必须验证该句柄已事件句柄通过调用上下文中 IOCTL [ **ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)。

 

 




