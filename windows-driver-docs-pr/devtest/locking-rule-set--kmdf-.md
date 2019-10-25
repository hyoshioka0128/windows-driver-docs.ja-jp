---
title: ロックの規則セット (KMDF)
description: これらの規則を使用して、ドライバーが共有リソースを正しく管理していることを確認します。
ms.assetid: B6DD41A5-E7E5-4070-8752-68E26804A5D5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 981781b0245c21211474590434cd825bc6a9595d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840135"
---
# <a name="locking-rule-set-kmdf"></a>ロックの規則セット (KMDF)


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
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"><strong>ParentObjectCheckLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"><strong>ParentObjectCheckLock</strong></a>ルールでは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate" data-raw-source="[&lt;strong&gt;WdfWaitLockCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate)"><strong>Wdfwaitlockcreate</strong></a>を<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate" data-raw-source="[&lt;strong&gt;WdfSpinLockCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate)"><strong>呼び出し、親オブジェクトを設定する</strong></a>必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"><strong>ReqSendWhileSpinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"><strong>ReqSendWhileSpinlock</strong></a>規則は、ドライバーがスピンロックを保持している間に要求が送信されないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>スピンロック</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>スピンロック</strong></a>の規則は、厳密な代替で<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>または<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinlock</strong></a>への呼び出しが使用されることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"><strong>SpinlockDpc</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"><strong>SpinlockDpc</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>または<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinlock</strong></a>の呼び出しが厳密な代替で使用されることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"><strong>SpinlockRelease</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>への呼び出しが kmdf コールバック内でバランスの取れた方法で使用されることを指定します。 KMDF コールバックルーチンの最後に、ドライバーはスピンロックを保持しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"><strong>WdfInterruptLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"><strong>WdfInterruptLock</strong></a>規則は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547340" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547340)"><strong>WdfInterruptAcquireLock</strong></a>メソッドの呼び出しが<a href="https://msdn.microsoft.com/library/windows/hardware/ff547376" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547376)"><strong>WdfInterruptReleaseLock</strong></a>の呼び出しで厳格な代替で使用されることを指定します。 さらに、KMDF コールバックルーチンの最後では、ドライバーは、前の<strong>WdfInterruptAcquireLock</strong>の呼び出しで取得されたフレームワークのスピンロックオブジェクトを保持することはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"><strong>WdfInterruptLockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"><strong>WdfInterruptLockRelease</strong></a>規則は、kmdf コールバックルーチン内で、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547340" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547340)"><strong>WdfInterruptAcquireLock</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff547376" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547376)"><strong>WdfInterruptReleaseLock</strong></a>の呼び出しが均衡の取れた方法で使用されることを指定します。 KMDF コールバックルーチンの最後では、 <strong>WdfInterruptAcquireLock</strong>への以前の呼び出しによって取得されたフレームワークのスピンロックオブジェクトをドライバーが保持することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"><strong>WdfSpinlock ロック</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"><strong>Wdfspinlock ロック</strong></a>規則は、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))"><strong>WdfSpinLockAcquire</strong></a>メソッドへの呼び出しを<a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a>との厳密な代替で使用することを指定します。 KMDF コールバックルーチンの最後では、 <strong>WdfSpinLockAcquire</strong>への以前の呼び出しによって取得されたフレームワークスピンロックオブジェクトをドライバーが保持することはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a>規則は、kmdf イベントのコールバック関数内で、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))"><strong>WdfSpinLockAcquire</strong></a>と<strong>WdfSpinlockRelease</strong>の呼び出しが均衡の取れた方法で使用されることを指定します。 KMDF イベントのコールバック関数からが返された場合、ドライバーは、以前の<strong>WdfSpinLockAcquire</strong>の呼び出しによって取得されたフレームワークのスピンロックオブジェクトを保持することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"><strong>WdfWaitlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"><strong>Wdfwaitlock</strong></a>規則は、Wdfwaitlockrelease を使用した厳密な代替で<a href="https://msdn.microsoft.com/library/windows/hardware/ff551168" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551168)"><strong>Wdfwaitlock獲得</strong></a>の呼び出しが使用されることを指定します。 <a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"></a> KMDF イベントのコールバック関数から制御が戻ったときに、以前の<strong>Wdfwaitlockacquire</strong>の呼び出しで取得されたフレームワークのスピンロックオブジェクトをドライバーが保持することはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>Wdfwaitlockrelease</strong></a>ルールでは、kmdf イベントコールバック関数内で、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551168" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551168)"><strong>Wdfwaitlockrelease</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease" data-raw-source="[&lt;strong&gt;WdfWaitLockRelease&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)"><strong>wdfwaitlockrelease</strong></a>の呼び出しが均衡の取れた方法で使用されることを指定します。 KMDF イベントのコールバック関数から制御が戻ったときに、以前の<strong>Wdfwaitlockacquire</strong>の呼び出しで取得されたフレームワークのスピンロックオブジェクトをドライバーが保持することはできません。</p></td>
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

 

 





