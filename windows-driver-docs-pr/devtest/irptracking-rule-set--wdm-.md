---
title: IrpTracking の規則セット (WDM)
description: Irp が保留状態中にデバイスを削除しないようにには、ドライバーがその I/O 要求パケット (IRP) を正しく追跡することを確認するのにには、これらの規則を使用します。
ms.assetid: 9AD62397-6840-42FF-ADEC-6836EDD16647
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 792994e2a6071a8a94626b67611bd45649113693
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350516"
---
# <a name="irptracking-rule-set-wdm"></a>IrpTracking の規則セット (WDM)


Irp が保留状態中にデバイスを削除しないようにには、ドライバーがその I/O 要求パケット (IRP) を正しく追跡することを確認するのにには、これらの規則を使用します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-ioreleaseremovelockandwaitoutsideremovedevice.md" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWaitOutsideRemoveDevice&lt;/strong&gt;](wdm-ioreleaseremovelockandwaitoutsideremovedevice.md)"><strong>IoReleaseRemoveLockAndWaitOutsideRemoveDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreleaseremovelockandwaitoutsideremovedevice.md" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWaitOutsideRemoveDevice&lt;/strong&gt;](wdm-ioreleaseremovelockandwaitoutsideremovedevice.md)"> <strong>IoReleaseRemoveLockAndWaitOutsideRemoveDevice</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549567" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549567)"> <strong>IoReleaseRemoveLockAndWait</strong> </a>することはできませんPnP ドライバーの IRP_MJ_PNP IRP_MN_REMOVE_DEVICE と外部と呼ばれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-nsremovelockmnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnRemove&lt;/strong&gt;](wdm-nsremovelockmnremove.md)"><strong>NsRemoveLockMnRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-nsremovelockmnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnRemove&lt;/strong&gt;](wdm-nsremovelockmnremove.md)"> <strong>NsRemoveLockMnRemove</strong> </a> MinorFunction IRP_MN_REMOVE_DEVICE で IRP_MJ_PNP を処理するときに、ドライバーは STATUS_NOT_SUPPORTED を返しませんルールを確認します。 このルールは、FDO および FIDO ドライバーのみに適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-nsremovelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-nsremovelockmnsurpriseremove.md)"><strong>NsRemoveLockMnSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-nsremovelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-nsremovelockmnsurpriseremove.md)"> <strong>NsRemoveLockMnSurpriseRemove</strong> </a>ドライバーを返さないこと STATUS_NOT_SUPPORTED minorFunction IRP_MN_SUPRISE_REMOVAL IRP_MJ_PNP 要求を処理するときにルールを確認します。 このルールは、FDO および FIDO ドライバーのみに適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-nsremovelockquerymnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockQueryMnRemove&lt;/strong&gt;](wdm-nsremovelockquerymnremove.md)"><strong>NsRemoveLockQueryMnRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-nsremovelockquerymnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockQueryMnRemove&lt;/strong&gt;](wdm-nsremovelockquerymnremove.md)"> <strong>NsRemoveLockQueryMnRemove</strong> </a> MinorFunction IRP_MN_QUERY_REMOVE で IRP_MJ_PNP を処理するときに、ドライバーは STATUS_NOT_SUPPORTED を返しませんルールを確認します。 このルールは、FDO および FIDO ドライバーのみに適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelock.md" data-raw-source="[&lt;strong&gt;RemoveLock&lt;/strong&gt;](wdm-removelock.md)"><strong>RemoveLock</strong></a></p></td>
<td align="left"><p><a href="wdm-removelock.md" data-raw-source="[&lt;strong&gt;RemoveLock&lt;/strong&gt;](wdm-removelock.md)"> <strong>RemoveLock</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>が正しく使用します。 さらに、IRP_MJ_PNP または対し、IRP_MJ_POWER ルーチンの末尾には、ドライバー保持しないようにする、 <strong>RemoveLock</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockcheck.md" data-raw-source="[&lt;strong&gt;RemoveLockCheck&lt;/strong&gt;](wdm-removelockcheck.md)"><strong>RemoveLockCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockcheck.md" data-raw-source="[&lt;strong&gt;RemoveLockCheck&lt;/strong&gt;](wdm-removelockcheck.md)"> <strong>RemoveLockCheck</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549567" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549567)"> <strong>IoReleaseRemoveLockAndWait</strong> </a>が正しく MinorFunction IRP_MN_REMOVE_DEVICE で IRP_MJ_PNP を処理するときに使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforward.md" data-raw-source="[&lt;strong&gt;RemoveLockForward&lt;/strong&gt;](wdm-removelockforward.md)"><strong>RemoveLockForward</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforward.md" data-raw-source="[&lt;strong&gt;RemoveLockForward&lt;/strong&gt;](wdm-removelockforward.md)"> <strong>RemoveLockForward</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>が正しく、IRP を別のデバイスを転送するときに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforward2.md" data-raw-source="[&lt;strong&gt;RemoveLockForward2&lt;/strong&gt;](wdm-removelockforward2.md)"><strong>RemoveLockForward2</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforward2.md" data-raw-source="[&lt;strong&gt;RemoveLockForward2&lt;/strong&gt;](wdm-removelockforward2.md)"> <strong>RemoveLockForward2</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>が正しく IRP が別のデバイスに転送するときに使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl&lt;/strong&gt;](wdm-removelockforwarddevicecontrol.md)"><strong>RemoveLockForwardDeviceControl</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwarddevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl&lt;/strong&gt;](wdm-removelockforwarddevicecontrol.md)"> <strong>RemoveLockForwardDeviceControl</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>ドライバーを使用する場合が正しく使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a> IRP を別のデバイスを転送します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrol2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl2&lt;/strong&gt;](wdm-removelockforwarddevicecontrol2.md)"><strong>RemoveLockForwardDeviceControl2</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwarddevicecontrol2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl2&lt;/strong&gt;](wdm-removelockforwarddevicecontrol2.md)"> <strong>RemoveLockForwardDeviceControl2</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>ドライバーを使用する場合が正しく使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a> IRP を別のデバイスを転送します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrolinternal.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal.md)"><strong>RemoveLockForwardDeviceControlInternal</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwarddevicecontrolinternal.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal.md)"> <strong>RemoveLockForwardDeviceControlInternal</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"><strong>IoReleaseRemoveLock</strong> </a>がで正しく使用 IRP を使用して、転送するときに<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>別のデバイスにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrolinternal2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal2&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal2.md)"><strong>RemoveLockForwardDeviceControlInternal2</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwarddevicecontrolinternal2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal2&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal2.md)"> <strong>RemoveLockForwardDeviceControlInternal2</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"><strong>IoReleaseRemoveLock</strong> </a>がで正しく使用 IRP を使用して、転送するときに<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>別のデバイスにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwardread.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead&lt;/strong&gt;](wdm-removelockforwardread.md)"><strong>RemoveLockForwardRead</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwardread.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead&lt;/strong&gt;](wdm-removelockforwardread.md)"> <strong>RemoveLockForwardRead</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>で正しく使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwardread2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead2&lt;/strong&gt;](wdm-removelockforwardread2.md)"><strong>RemoveLockForwardRead2</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwardread2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead2&lt;/strong&gt;](wdm-removelockforwardread2.md)"> <strong>RemoveLockForwardRead2</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>が IRP を使用して、転送するときに正しく使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>別のデバイスにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwardwrite.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite&lt;/strong&gt;](wdm-removelockforwardwrite.md)"><strong>RemoveLockForwardWrite</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwardwrite.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite&lt;/strong&gt;](wdm-removelockforwardwrite.md)"> <strong>RemoveLockForwardWrite</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>が IRP を使用して、転送するときに正しく使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>別のデバイスにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwardwrite2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite2&lt;/strong&gt;](wdm-removelockforwardwrite2.md)"><strong>RemoveLockForwardWrite2</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwardwrite2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite2&lt;/strong&gt;](wdm-removelockforwardwrite2.md)"> <strong>RemoveLockForwardWrite2</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>が IRP を使用して、転送するときに正しく使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>別のデバイスにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockmnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove&lt;/strong&gt;](wdm-removelockmnremove.md)"><strong>RemoveLockMnRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockmnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove&lt;/strong&gt;](wdm-removelockmnremove.md)"> <strong>RemoveLockMnRemove</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549567" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549567)"> <strong>IoReleaseRemoveLockAndWait</strong> </a>が正しく MinorFunction IRP_MN_REMOVE_DEVICE で IRP_MJ_PNP を処理するときに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockmnremove2.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove2&lt;/strong&gt;](wdm-removelockmnremove2.md)"><strong>RemoveLockMnRemove2</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockmnremove2.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove2&lt;/strong&gt;](wdm-removelockmnremove2.md)"> <strong>RemoveLockMnRemove2</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549567" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549567)"> <strong>IoReleaseRemoveLockAndWait</strong> </a>が正しく IRP の前に IRP_MN_REMOVE_DEVICE 要求の処理が下位のドライバーに転送されるときに使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-removelockmnsurpriseremove.md)"><strong>RemoveLockMnSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-removelockmnsurpriseremove.md)"> <strong>RemoveLockMnSurpriseRemove</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549567" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549567)"> <strong>IoReleaseRemoveLockAndWait</strong> </a>が正しく MinorFunction IRP_MN_SUPRISE_REMOVAL で IRP_MJ_PNP を処理するときに使用します。 ドライバーは IRP が下位のスタックを転送する前に削除ロックを取得する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockquerymnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockQueryMnRemove&lt;/strong&gt;](wdm-removelockquerymnremove.md)"><strong>RemoveLockQueryMnRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockquerymnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockQueryMnRemove&lt;/strong&gt;](wdm-removelockquerymnremove.md)"> <strong>RemoveLockQueryMnRemove</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>が正しく MinorFunction IRP_MN_QUERY_REMOVE_DEVICE で IRP_MJ_PNP を処理するときに使用します。 ドライバーは IRP が下位のスタックを転送する前に削除ロックを取得する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockrelease2.md" data-raw-source="[&lt;strong&gt;RemoveLockRelease2&lt;/strong&gt;](wdm-removelockrelease2.md)"><strong>RemoveLockRelease2</strong></a></p></td>
<td align="left"><p>ルール<a href="wdm-removelockrelease2.md" data-raw-source="[&lt;strong&gt;RemoveLockRelease2&lt;/strong&gt;](wdm-removelockrelease2.md)"> <strong>RemoveLockRelease2</strong> </a>への呼び出しを確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)">  <strong>。IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasecleanup.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCleanup&lt;/strong&gt;](wdm-removelockreleasecleanup.md)"><strong>RemoveLockReleaseCleanup</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasecleanup.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCleanup&lt;/strong&gt;](wdm-removelockreleasecleanup.md)"> <strong>RemoveLockReleaseCleanup</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 呼び出しごとに<strong>IoAcquireRemoveLock</strong>に一致する呼び出しがあります。 <strong>IoReleaseRemoveLock</strong>します。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleaseclose.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseClose&lt;/strong&gt;](wdm-removelockreleaseclose.md)"><strong>RemoveLockReleaseClose</strong></a></p></td>
<td align="left"><p>ルール<a href="wdm-removelockreleaseclose.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseClose&lt;/strong&gt;](wdm-removelockreleaseclose.md)"> <strong>RemoveLockReleaseClose</strong> </a>への呼び出しを確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)">  <strong>。IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasecreate.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCreate&lt;/strong&gt;](wdm-removelockreleasecreate.md)"><strong>RemoveLockReleaseCreate</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasecreate.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCreate&lt;/strong&gt;](wdm-removelockreleasecreate.md)"> <strong>RemoveLockReleaseCreate</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleasedevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseDeviceControl&lt;/strong&gt;](wdm-removelockreleasedevicecontrol.md)"><strong>RemoveLockReleaseDeviceControl</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasedevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseDeviceControl&lt;/strong&gt;](wdm-removelockreleasedevicecontrol.md)"> <strong>RemoveLockReleaseDeviceControl</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleaseinternaldevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseInternalDeviceControl&lt;/strong&gt;](wdm-removelockreleaseinternaldevicecontrol.md)"><strong>RemoveLockReleaseInternalDeviceControl</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleaseinternaldevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseInternalDeviceControl&lt;/strong&gt;](wdm-removelockreleaseinternaldevicecontrol.md)"> <strong>RemoveLockReleaseInternalDeviceControl</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"><strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleasepnp.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePnp&lt;/strong&gt;](wdm-removelockreleasepnp.md)"><strong>RemoveLockReleasePnp</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasepnp.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePnp&lt;/strong&gt;](wdm-removelockreleasepnp.md)"> <strong>RemoveLockReleasePnp</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasepower.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePower&lt;/strong&gt;](wdm-removelockreleasepower.md)"><strong>RemoveLockReleasePower</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasepower.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePower&lt;/strong&gt;](wdm-removelockreleasepower.md)"> <strong>RemoveLockReleasePower</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleaseread.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseRead&lt;/strong&gt;](wdm-removelockreleaseread.md)"><strong>RemoveLockReleaseRead</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleaseread.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseRead&lt;/strong&gt;](wdm-removelockreleaseread.md)"> <strong>RemoveLockReleaseRead</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleaseshutdown.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseShutdown&lt;/strong&gt;](wdm-removelockreleaseshutdown.md)"><strong>RemoveLockReleaseShutdown</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleaseshutdown.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseShutdown&lt;/strong&gt;](wdm-removelockreleaseshutdown.md)"> <strong>RemoveLockReleaseShutdown</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleasesystemcontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseSystemControl&lt;/strong&gt;](wdm-removelockreleasesystemcontrol.md)"><strong>RemoveLockReleaseSystemControl</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasesystemcontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseSystemControl&lt;/strong&gt;](wdm-removelockreleasesystemcontrol.md)"> <strong>RemoveLockReleaseSystemControl</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasewrite.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseWrite&lt;/strong&gt;](wdm-removelockreleasewrite.md)"><strong>RemoveLockReleaseWrite</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasewrite.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseWrite&lt;/strong&gt;](wdm-removelockreleasewrite.md)"> <strong>RemoveLockReleaseWrite</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong> </a>厳密な代替構成で使用されます。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。</p></td>
</tr>
</tbody>
</table>

 

**IrpTracking ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **IrpTracking**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **IrpTracking.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpTracking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





