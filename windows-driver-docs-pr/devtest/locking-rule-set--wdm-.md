---
title: ロックの規則セット (WDM)
description: これらの規則を使用して、ドライバーが共有リソースを正しく管理していることを確認します。
ms.assetid: B23863BD-66F0-4E6F-B150-97FD2066F69C
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 23dc87ab87dd7ee0869521a471c15c13ce8c9431
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839411"
---
# <a name="locking-rule-set-wdm"></a>ロックの規則セット (WDM)


これらの規則を使用して、ドライバーが共有リソースを正しく管理していることを確認します。

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
<td align="left"><p><a href="wdm-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock&lt;/strong&gt;](wdm-cancelspinlock.md)"><strong>CancelSpinLock ロック</strong></a></p></td>
<td align="left"><p>CancelSpinLock ロック規則は、ドライバーが<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))"><strong>IoReleaseCancelSpinLock</strong></a>を呼び出す前に<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))"><strong>IoAcquireCancelSpinLock</strong></a>を呼び出し、ドライバーが IoReleaseCancelSpinLock を呼び出してから <strong>次のの呼び出しの前にを呼び出すことを指定します。IoAcquireCancelSpinLock</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"><strong>CancelSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"><strong>CancelSpinlockRelease</strong></a>規則は、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))"><strong>IoAcquireCancelSpinLock</strong></a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))"><strong>IoReleaseCancelSpinLock</strong></a>の呼び出しが厳密な代替で使用されることを指定します。 つまり、 <strong>IoAcquireCancelSpinLock</strong>を呼び出すたびに、 <strong>IoReleaseCancelSpinLock</strong>への対応する呼び出しが必要になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"><strong>CriticalRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"><strong>CriticalRegions</strong></a>規則は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)"><strong>KeLeaveCriticalRegion</strong></a>を呼び出す前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)"><strong>KeEnterCriticalRegion</strong></a>を呼び出す必要があることと、ドライバーが<strong>KeLeaveCriticalRegion</strong>を呼び出した後にを<strong>呼び出します。KeEnterCriticalRegion</strong>。 (入れ子になった呼び出しが許可されます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"><strong>ExclusiveResourceAccess</strong></a></p></td>
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"><strong>ExclusiveResourceAccess</strong></a>規則は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)"><strong>ExReleaseResourceLite</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"><strong>ExReleaseResourceForThreadLite</strong></a>を呼び出す前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"><strong>ExAcquireResourceExclusiveLite</strong></a>を呼び出し、ドライバーがを呼び<strong>出すように指定します。ExReleaseResourceLite</strong>または<strong>ExReleaseResourceForThreadLite</strong>は、それ以降の<strong>ExAcquireResourceExclusiveLite</strong>の呼び出しの前に発生します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"><strong>GuardedRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"><strong>GuardedRegions</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion" data-raw-source="[&lt;strong&gt;KeEnterGuardedRegion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)"><strong>KeEnterGuardedRegion</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion" data-raw-source="[&lt;strong&gt;KeLeaveGuardedRegion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)"><strong>KeLeaveGuardedRegion</strong></a>の呼び出しが厳密な代替で使用されることを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a>規則は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>を呼び出す前に<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a>を呼び出し、ドライバーが<strong>KeReleaseInStackQueuedSpinLock</strong>を呼び出す前に、後続の<strong>KeAcquireInStackQueuedSpinLock</strong>の呼び出し。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a>規則は、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>の呼び出しが厳密な代替で使用されることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>スピンロック</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>スピンロック</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>を呼び出した後、 <strong>KeAcquireSpinLock</strong>または<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>への後続の呼び出しの前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>を呼び出すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"><strong>SpinLockDpc</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>または<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>の呼び出しを厳密な代替で行う必要があることを指定します。 つまり、 <strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>を呼び出した後、ドライバーは、 <strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>への後続の呼び出しの前に<strong>KeReleaseSpinLock</strong>を呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"><strong>SpinlockRelease</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>への呼び出しが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>を持つ厳密な代替で行われることを指定します。 つまり、ドライバーは、 <strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>を呼び出した後、 <strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>への後続の呼び出しの前に、 <strong>KeReleaseSpinLock</strong>を呼び出す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"><strong>SpinLockSafe</strong></a>ルールでは、スピンロックを保持している間に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)"><strong>Iostartnextpacket</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>が呼び出されないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a>規則は、特定の同期関数に対するドライバーの呼び出しが、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)"><strong>KeEnterCriticalRegion</strong></a>を呼び出した後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)"><strong>KeLeaveCriticalRegion</strong></a>を呼び出す前にのみ表示されることを指定します。</p>
<p>影響を受ける同期関数は次のとおりです。</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544363" data-raw-source="[&lt;strong&gt;ExAcquireResourceSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544363)"><strong>ExAcquireResourceSharedLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"><strong>ExAcquireResourceExclusiveLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544367" data-raw-source="[&lt;strong&gt;ExAcquireSharedStarveExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544367)"><strong>ExAcquireSharedStarveExclusive</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544370" data-raw-source="[&lt;strong&gt;ExAcquireSharedWaitForExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544370)"><strong>ExAcquireSharedWaitForExclusive</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)"><strong>ExReleaseResourceLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"><strong>ExReleaseResourceForThreadLite</strong></a></p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**ロック規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[ロック]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを使用して**sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





