---
title: NtXxx 例程
description: NtXxx 例程
ms.assetid: 71db6fa6-d1f8-4aed-9de1-bba1f6cee1ce
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ca8db16cb9f46700301d320f58d3e13a41645fe
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393417"
---
# <a name="ntxxx-routines"></a>NtXxx 例程


本部分介绍**Nt * Xxx*** 版本的 Windows 本机系统服务例程。 大多数自带的系统服务例程有两个版本，其中一个其中有一个名称以前缀开头**Nt**; 另一个版本具有前缀开头的名称**Zw**。 例如，调用[ **NtCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)并[ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)执行类似的操作，并且，事实上，提供由同一个服务内核模式系统例程。

从内核模式驱动程序调用**Nt * Xxx*** 和**Zw * Xxx*** 版本的 Windows 本机系统服务例程在它们处理和解释输入的参数的方式行为可能有所不同。 有关详细信息之间的关系**Nt * Xxx*** 和**Zw * Xxx*** 的例程的版本，请参阅[使用 Nt 和 Zw 版本的本机系统服务例程](using-nt-and-zw-versions-of-the-native-system-services-routines.md).

下表总结了**Nt * Xxx*** 和**Zw * Xxx*** 例程的版本：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>NtXxx</th>
<th>ZwXxx</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NtAllocateLocallyUniqueId</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwallocatelocallyuniqueid" data-raw-source="[&lt;strong&gt;ZwAllocateLocallyUniqueId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwallocatelocallyuniqueid)"><strong>ZwAllocateLocallyUniqueId</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtAllocateVirtualMemory</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566416" data-raw-source="[&lt;strong&gt;ZwAllocateVirtualMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566416)"><strong>ZwAllocateVirtualMemory</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtClose</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)"><strong>ZwClose</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtCommitComplete</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete" data-raw-source="[&lt;strong&gt;ZwCommitComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)"><strong>ZwCommitComplete</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtCommitEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment" data-raw-source="[&lt;strong&gt;ZwCommitEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)"><strong>ZwCommitEnlistment</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtCommitTransaction</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction" data-raw-source="[&lt;strong&gt;ZwCommitTransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)"><strong>ZwCommitTransaction</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtCreateDirectoryObject</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject" data-raw-source="[&lt;strong&gt;ZwCreateDirectoryObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)"><strong>ZwCreateDirectoryObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtCreateEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment" data-raw-source="[&lt;strong&gt;ZwCreateEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment)"><strong>ZwCreateEnlistment</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtCreateEvent</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566423" data-raw-source="[&lt;strong&gt;ZwCreateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566423)"><strong>ZwCreateEvent</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtCreateFile</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)"><strong>ZwCreateFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtCreateKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)"><strong>ZwCreateKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtCreateResourceManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager" data-raw-source="[&lt;strong&gt;ZwCreateResourceManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager)"><strong>ZwCreateResourceManager</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtCreateSection</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatesection" data-raw-source="[&lt;strong&gt;ZwCreateSection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatesection)"><strong>ZwCreateSection</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtCreateTransaction</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction" data-raw-source="[&lt;strong&gt;ZwCreateTransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)"><strong>ZwCreateTransaction</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtCreateTransactionManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransactionmanager" data-raw-source="[&lt;strong&gt;ZwCreateTransactionManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransactionmanager)"><strong>ZwCreateTransactionManager</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtCurrentProcess</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;ZwCurrentProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>ZwCurrentProcess</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtCurrentThread</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;ZwCurrentThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>ZwCurrentThread</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtDeleteFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566435" data-raw-source="[&lt;strong&gt;ZwDeleteFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566435)"><strong>ZwDeleteFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtDeleteKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey)"><strong>ZwDeleteKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtDeleteValueKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletevaluekey" data-raw-source="[&lt;strong&gt;ZwDeleteValueKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletevaluekey)"><strong>ZwDeleteValueKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtDeviceIoControlFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566441" data-raw-source="[&lt;strong&gt;ZwDeviceIoControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566441)"><strong>ZwDeviceIoControlFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtDuplicateObject</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566445" data-raw-source="[&lt;strong&gt;ZwDuplicateObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566445)"><strong>ZwDuplicateObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtDuplicateToken</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566446" data-raw-source="[&lt;strong&gt;ZwDuplicateToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566446)"><strong>ZwDuplicateToken</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtEnumerateKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratekey" data-raw-source="[&lt;strong&gt;ZwEnumerateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratekey)"><strong>ZwEnumerateKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtEnumerateTransactionObject</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntenumeratetransactionobject" data-raw-source="[&lt;strong&gt;ZwEnumerateTransactionObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntenumeratetransactionobject)"><strong>ZwEnumerateTransactionObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtEnumerateValueKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratevaluekey" data-raw-source="[&lt;strong&gt;ZwEnumerateValueKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratevaluekey)"><strong>ZwEnumerateValueKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtFlushBuffersFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566454" data-raw-source="[&lt;strong&gt;ZwFlushBuffersFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566454)"><strong>ZwFlushBuffersFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtFlushBuffersFileEx</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh967720" data-raw-source="[&lt;strong&gt;ZwFlushBuffersFileEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh967720)"><strong>ZwFlushBuffersFileEx</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtFlushKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwflushkey" data-raw-source="[&lt;strong&gt;ZwFlushKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwflushkey)"><strong>ZwFlushKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtFlushVirtualMemory</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566458" data-raw-source="[&lt;strong&gt;ZwFlushVirtualMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566458)"><strong>ZwFlushVirtualMemory</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtFreeVirtualMemory</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566460" data-raw-source="[&lt;strong&gt;ZwFreeVirtualMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566460)"><strong>ZwFreeVirtualMemory</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtFsControlFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566462" data-raw-source="[&lt;strong&gt;ZwFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566462)"><strong>ZwFsControlFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtGetNotificationResourceManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntgetnotificationresourcemanager" data-raw-source="[&lt;strong&gt;ZwGetNotificationResourceManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntgetnotificationresourcemanager)"><strong>ZwGetNotificationResourceManager</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtLoadDriver</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwloaddriver" data-raw-source="[&lt;strong&gt;ZwLoadDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwloaddriver)"><strong>ZwLoadDriver</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtLockFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566474" data-raw-source="[&lt;strong&gt;ZwLockFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566474)"><strong>ZwLockFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtMakeTemporaryObject</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmaketemporaryobject" data-raw-source="[&lt;strong&gt;ZwMakeTemporaryObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmaketemporaryobject)"><strong>ZwMakeTemporaryObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtMapViewOfSection</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmapviewofsection" data-raw-source="[&lt;strong&gt;ZwMapViewOfSection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmapviewofsection)"><strong>ZwMapViewOfSection</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtNotifyChangeKey</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566488" data-raw-source="[&lt;strong&gt;ZwNotifyChangeKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566488)"><strong>ZwNotifyChangeKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtOpenDirectoryObject</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566492" data-raw-source="[&lt;strong&gt;ZwOpenDirectoryObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566492)"><strong>ZwOpenDirectoryObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtOpenEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenenlistment" data-raw-source="[&lt;strong&gt;ZwOpenEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenenlistment)"><strong>ZwOpenEnlistment</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtOpenEvent</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenevent" data-raw-source="[&lt;strong&gt;ZwOpenEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenevent)"><strong>ZwOpenEvent</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtOpenFile</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile" data-raw-source="[&lt;strong&gt;ZwOpenFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)"><strong>ZwOpenFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtOpenKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)"><strong>ZwOpenKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtOpenProcess</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ntopenprocess" data-raw-source="[&lt;strong&gt;ZwOpenProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ntopenprocess)"><strong>ZwOpenProcess</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtOpenProcessTokenEx</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567024" data-raw-source="[&lt;strong&gt;ZwOpenProcessTokenEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567024)"><strong>ZwOpenProcessTokenEx</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtOpenResourceManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenresourcemanager" data-raw-source="[&lt;strong&gt;ZwOpenResourceManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenresourcemanager)"><strong>ZwOpenResourceManager</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtOpenSection</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection" data-raw-source="[&lt;strong&gt;ZwOpenSection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)"><strong>ZwOpenSection</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtOpenSymbolicLinkObject</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensymboliclinkobject" data-raw-source="[&lt;strong&gt;ZwOpenSymbolicLinkObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensymboliclinkobject)"><strong>ZwOpenSymbolicLinkObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtOpenThreadTokenEx</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567032" data-raw-source="[&lt;strong&gt;ZwOpenThreadTokenEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567032)"><strong>ZwOpenThreadTokenEx</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtOpenTransaction</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransaction" data-raw-source="[&lt;strong&gt;ZwOpenTransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransaction)"><strong>ZwOpenTransaction</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtOpenTransactionManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransactionmanager" data-raw-source="[&lt;strong&gt;ZwOpenTransactionManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransactionmanager)"><strong>ZwOpenTransactionManager</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtPowerInformation</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpowerinformation" data-raw-source="[&lt;strong&gt;ZwPowerInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpowerinformation)"><strong>ZwPowerInformation</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtPrepareComplete</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete" data-raw-source="[&lt;strong&gt;ZwPrepareComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)"><strong>ZwPrepareComplete</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtPrepareEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment" data-raw-source="[&lt;strong&gt;ZwPrepareEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment)"><strong>ZwPrepareEnlistment</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtPrePrepareComplete</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete" data-raw-source="[&lt;strong&gt;ZwPrePrepareComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete)"><strong>ZwPrePrepareComplete</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtPrePrepareEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreprepareenlistment" data-raw-source="[&lt;strong&gt;ZwPrePrepareEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreprepareenlistment)"><strong>ZwPrePrepareEnlistment</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQueryDirectoryFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567047" data-raw-source="[&lt;strong&gt;ZwQueryDirectoryFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567047)"><strong>ZwQueryDirectoryFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQueryFullAttributesFile</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryfullattributesfile" data-raw-source="[&lt;strong&gt;ZwQueryFullAttributesFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryfullattributesfile)"><strong>ZwQueryFullAttributesFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQueryInformationEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationenlistment" data-raw-source="[&lt;strong&gt;ZwQueryInformationEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationenlistment)"><strong>ZwQueryInformationEnlistment</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQueryInformationFile</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)"><strong>ZwQueryInformationFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQueryInformationResourceManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationresourcemanager" data-raw-source="[&lt;strong&gt;ZwQueryInformationResourceManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationresourcemanager)"><strong>ZwQueryInformationResourceManager</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQueryInformationToken</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567055" data-raw-source="[&lt;strong&gt;ZwQueryInformationToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567055)"><strong>ZwQueryInformationToken</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQueryInformationTransaction</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction" data-raw-source="[&lt;strong&gt;ZwQueryInformationTransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction)"><strong>ZwQueryInformationTransaction</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQueryInformationTransactionManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransactionmanager" data-raw-source="[&lt;strong&gt;ZwQueryInformationTransactionManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransactionmanager)"><strong>ZwQueryInformationTransactionManager</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQueryKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerykey" data-raw-source="[&lt;strong&gt;ZwQueryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerykey)"><strong>ZwQueryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQueryObject</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567062" data-raw-source="[&lt;strong&gt;ZwQueryObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567062)"><strong>ZwQueryObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQueryQuotaInformationFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567064" data-raw-source="[&lt;strong&gt;ZwQueryQuotaInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567064)"><strong>ZwQueryQuotaInformationFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQuerySecurityObject</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567066" data-raw-source="[&lt;strong&gt;ZwQuerySecurityObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567066)"><strong>ZwQuerySecurityObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQuerySecurityObject</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerysymboliclinkobject" data-raw-source="[&lt;strong&gt;ZwQuerySymbolicLinkObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerysymboliclinkobject)"><strong>ZwQuerySymbolicLinkObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQueryValueKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryvaluekey" data-raw-source="[&lt;strong&gt;ZwQueryValueKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryvaluekey)"><strong>ZwQueryValueKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtQueryVirtualMemory</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn957455" data-raw-source="[&lt;strong&gt;ZwQueryVirtualMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn957455)"><strong>ZwQueryVirtualMemory</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtQueryVolumeInformationFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567070" data-raw-source="[&lt;strong&gt;ZwQueryVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567070)"><strong>ZwQueryVolumeInformationFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtReadFile</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)"><strong>ZwReadFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtReadOnlyEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntreadonlyenlistment" data-raw-source="[&lt;strong&gt;ZwReadOnlyEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntreadonlyenlistment)"><strong>ZwReadOnlyEnlistment</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtReadOnlyEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment" data-raw-source="[&lt;strong&gt;ZwRecoverEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment)"><strong>ZwRecoverEnlistment</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtRecoverResourceManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager" data-raw-source="[&lt;strong&gt;ZwRecoverResourceManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager)"><strong>ZwRecoverResourceManager</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtRecoverTransactionManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecovertransactionmanager" data-raw-source="[&lt;strong&gt;ZwRecoverTransactionManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecovertransactionmanager)"><strong>ZwRecoverTransactionManager</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtRollbackComplete</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete" data-raw-source="[&lt;strong&gt;ZwRollbackComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)"><strong>ZwRollbackComplete</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtRollbackEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment" data-raw-source="[&lt;strong&gt;ZwRollbackEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)"><strong>ZwRollbackEnlistment</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtRollbackTransaction</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction" data-raw-source="[&lt;strong&gt;ZwRollbackTransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)"><strong>ZwRollbackTransaction</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtRollforwardTransactionManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollforwardtransactionmanager" data-raw-source="[&lt;strong&gt;ZwRollforwardTransactionManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollforwardtransactionmanager)"><strong>ZwRollforwardTransactionManager</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtSetEvent</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567092" data-raw-source="[&lt;strong&gt;ZwSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567092)"><strong>ZwSetEvent</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtSetInformationEnlistment</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationenlistment" data-raw-source="[&lt;strong&gt;ZwSetInformationEnlistment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationenlistment)"><strong>ZwSetInformationEnlistment</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtSetInformationFile</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)"><strong>ZwSetInformationFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtSetInformationResourceManager</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationresourcemanager" data-raw-source="[&lt;strong&gt;ZwSetInformationResourceManager&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationresourcemanager)"><strong>ZwSetInformationResourceManager</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtSetInformationThread</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwsetinformationthread" data-raw-source="[&lt;strong&gt;ZwSetInformationThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwsetinformationthread)"><strong>ZwSetInformationThread</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtSetInformationToken</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567102" data-raw-source="[&lt;strong&gt;ZwSetInformationToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567102)"><strong>ZwSetInformationToken</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtSetInformationTransaction</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationtransaction" data-raw-source="[&lt;strong&gt;ZwSetInformationTransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationtransaction)"><strong>ZwSetInformationTransaction</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtSetQuotaInformationFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567105" data-raw-source="[&lt;strong&gt;ZwSetQuotaInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567105)"><strong>ZwSetQuotaInformationFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtSetSecurityObject</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567106" data-raw-source="[&lt;strong&gt;ZwSetSecurityObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567106)"><strong>ZwSetSecurityObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtSetValueKey</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwsetvaluekey" data-raw-source="[&lt;strong&gt;ZwSetValueKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwsetvaluekey)"><strong>ZwSetValueKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtSetVolumeInformationFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567112" data-raw-source="[&lt;strong&gt;ZwSetVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567112)"><strong>ZwSetVolumeInformationFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtSinglePhaseReject</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsinglephasereject" data-raw-source="[&lt;strong&gt;ZwSinglePhaseReject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsinglephasereject)"><strong>ZwSinglePhaseReject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtTerminateProcess</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwterminateprocess" data-raw-source="[&lt;strong&gt;ZwTerminateProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwterminateprocess)"><strong>ZwTerminateProcess</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtUnloadDriver</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunloaddriver" data-raw-source="[&lt;strong&gt;ZwUnloadDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunloaddriver)"><strong>ZwUnloadDriver</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtUnlockFile</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567118" data-raw-source="[&lt;strong&gt;ZwUnlockFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567118)"><strong>ZwUnlockFile</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtUnmapViewOfSection</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunmapviewofsection" data-raw-source="[&lt;strong&gt;ZwUnmapViewOfSection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunmapviewofsection)"><strong>ZwUnmapViewOfSection</strong></a></p></td>
</tr>
<tr class="even">
<td><p>NtWaitForSingleObject</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567120" data-raw-source="[&lt;strong&gt;ZwWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567120)"><strong>ZwWaitForSingleObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>NtWriteFile</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile)"><strong>ZwWriteFile</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




