---
title: ロックの規則セット (WDM)
description: ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。
ms.assetid: B23863BD-66F0-4E6F-B150-97FD2066F69C
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b5d7b3b00888327ec27402edaabf849aa6c3544a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349525"
---
# <a name="locking-rule-set-wdm"></a>ロックの規則セット (WDM)


ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。

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
<td align="left"><p><a href="wdm-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock&lt;/strong&gt;](wdm-cancelspinlock.md)"><strong>CancelSpinLock</strong></a></p></td>
<td align="left"><p>CancelSpinLock ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548196" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548196)"> <strong>IoAcquireCancelSpinLock</strong> </a>呼び出す前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff549550" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549550)"> <strong>IoReleaseCancelSpinLock</strong> </a>ドライバーを呼び出すと<strong>IoReleaseCancelSpinLock</strong>への後続の呼び出しの前に<strong>IoAcquireCancelSpinLock</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"><strong>CancelSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"> <strong>CancelSpinlockRelease</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff548196" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548196)"> <strong>IoAcquireCancelSpinLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549550" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549550)"> <strong>IoReleaseCancelSpinLock</strong> </a>厳密な代替構成で使用されます。 すべての呼び出しには、 <strong>IoAcquireCancelSpinLock</strong>に対応する呼び出しがあります。 <strong>IoReleaseCancelSpinLock</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"><strong>CriticalRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"> <strong>CriticalRegions</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff552021" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552021)"> <strong>KeEnterCriticalRegion</strong> </a>呼び出す前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff552964" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552964)"><strong>KeLeaveCriticalRegion</strong> </a>ドライバーを呼び出すと<strong>KeLeaveCriticalRegion</strong>への後続の呼び出しの前に<strong>KeEnterCriticalRegion</strong>. (入れ子になった呼び出しが許可されます。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"><strong>ExclusiveResourceAccess</strong></a></p></td>
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"> <strong>ExclusiveResourceAccess</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"> <strong>ExAcquireResourceExclusiveLite</strong> </a>呼び出す前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff545597" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545597)"> <strong>ExReleaseResourceLite</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"> <strong>ExReleaseResourceForThreadLite</strong> </a>し、ドライバーがを呼び出すことを指定します。<strong>ExReleaseResourceLite</strong>または<strong>ExReleaseResourceForThreadLite</strong>への後続の呼び出しの前に<strong>ExAcquireResourceExclusiveLite</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"><strong>GuardedRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"> <strong>GuardedRegions</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff552028" data-raw-source="[&lt;strong&gt;KeEnterGuardedRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552028)"> <strong>KeEnterGuardedRegion</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff552967" data-raw-source="[&lt;strong&gt;KeLeaveGuardedRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552967)"> <strong>KeLeaveGuardedRegion</strong> </a>厳密な代替構成で使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"> <strong>QueuedSpinLock</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff551899" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551899)"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a> を呼び出す前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff553130" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553130)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a> 、ドライバーを呼び出すと<strong>KeReleaseInStackQueuedSpinLock</strong>への後続の呼び出しの前に<strong>KeAcquireInStackQueuedSpinLock</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"> <strong>QueuedSpinLockRelease</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff551899" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551899)"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff553130" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553130)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a>厳密な代替構成で使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>スピンロック</strong></a>ルールを指定するには、呼び出した後<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong></a>、ドライバー呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a>後続の呼び出しの前に<strong>KeAcquireSpinLock</strong>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"> <strong>SpinLockDpc</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a>厳密な交互に行う必要があります。 これを呼び出した後<strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>、ドライバーを呼び出す必要があります<strong>KeReleaseSpinLock</strong> 後続の呼び出しの前に<strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"> <strong>SpinlockRelease</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a> で厳密な代替構成に加えられた<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong></a>します。 つまり、ドライバーを呼び出す必要があります<strong>KeReleaseSpinLock</strong>呼び出した後<strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong> 後続の呼び出しの前に<strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"> <strong>SpinLockSafe</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff550358" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550358)"><strong>います</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong> </a>スピン ロックを保持しているときに呼び出されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"> <strong>WithinCriticalRegion</strong> </a>ルールでは、ドライバーの特定の同期の関数呼び出しを呼び出した後のみが表示されることを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff552021" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552021)"> <strong>KeEnterCriticalRegion</strong> </a>を呼び出す前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff552964" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552964)"> <strong>KeLeaveCriticalRegion</strong></a>します。</p>
<p>影響を受ける同期関数、次に示します。</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544363" data-raw-source="[&lt;strong&gt;ExAcquireResourceSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544363)"><strong>ExAcquireResourceSharedLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"><strong>ExAcquireResourceExclusiveLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544367" data-raw-source="[&lt;strong&gt;ExAcquireSharedStarveExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544367)"><strong>ExAcquireSharedStarveExclusive</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544370" data-raw-source="[&lt;strong&gt;ExAcquireSharedWaitForExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544370)"><strong>ExAcquireSharedWaitForExclusive</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545597" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545597)"><strong>ExReleaseResourceLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"><strong>ExReleaseResourceForThreadLite</strong></a></p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**ロックの規則を選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**ロック**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Locking.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





