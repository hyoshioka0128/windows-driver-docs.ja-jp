---
title: ロックの規則セット (Storport)
description: これらの規則を使用して、ドライバーが共有リソースを正しく管理していることを確認します。
ms.assetid: FBB75F07-E689-4B7C-B053-E0B6A3772764
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1859aa5c19bfb7fc97c47b933952bf517ba3ab82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840131"
---
# <a name="locking-rule-set-storport"></a>ロックの規則セット (Storport)


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
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock&lt;/strong&gt;](storport-cancelspinlock.md)"><strong>CancelSpinLock ロック</strong></a></p></td>
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock Rule (Storport)&lt;/strong&gt;](storport-cancelspinlock.md)"><strong>Cancelspinlock ロック規則 (Storport)</strong></a>の規則は、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))"><strong>IoAcquireCancelSpinLock</strong></a>の各呼び出しの後に<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))"><strong>IoReleaseCancelSpinLock</strong></a>の呼び出しが行われることを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a>ルールは、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a>を使用して取得された、スタック内のキューに置かれたスピンロックが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>を使用してすぐに解放されることを確認します。 また、ディスパッチまたはキャンセルルーチンの終了時に、ドライバーはロックを保持しないようにする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](storport-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p>このルールは、ドライバーが<strong>KeAcquireInStackQueuedSpinLock</strong>を介してロックを取得せずに<strong>KeReleaseInStackQueuedSpinLock</strong>を呼び出さないことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](storport-spinlock.md)"><strong>スピンロック</strong></a></p></td>
<td align="left"><p>このルールでは、 <strong>KeAcquireSpinLock</strong>への呼び出しの後に<strong>KeReleaseSpinlock</strong>の呼び出しが行われていることを確認します。 ロックを解除する前に、ドライバーが<strong>KeAcquireSpinLockRaiseToDpc</strong>または<strong>KeAcquireSpinLock</strong>を再度呼び出すと、ルールは失敗します。 また、ディスパッチまたはキャンセルルーチンを終了する前に、ドライバーはスピンロックを解除する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](storport-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p>このルールでは、 <strong>KeAcquireSpinLockRaiseToDpc</strong>への呼び出しの後に<strong>KeReleaseSpinlock</strong>の呼び出しが行われていることを確認します。 ロックを解除する前に、ドライバーが<strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>を再度呼び出すと、ルールは失敗します。 また、ディスパッチまたはキャンセルルーチンを終了する前に、ドライバーはスピンロックを解除する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](storport-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>このルールは、ドライバーが<strong>KeAquireSpinlock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>を使用して最初に取得せずに、 <strong>KeReleaseSpinLock</strong>を使用してロックを解除しようとしていないことを確認します。 取得したスピンロックが解放されると、ルールはに合格します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](storport-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p>このルールは、スピンロックの保持中に<strong>Iostartnextpacket</strong>および<strong>IoCompleteRequest</strong>ルーチンが呼び出されないことを確認します。 このルールは、いつでも保持されているスピンロックの数を追跡します。いずれかのルーチンが呼び出されたときに、その数が0でない場合は、ドライバーがルールに失敗します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportmsilock.md" data-raw-source="[&lt;strong&gt;StorPortMSILock&lt;/strong&gt;](storport-storportmsilock.md)"><strong>StorPortMSILock</strong></a></p></td>
<td align="left"><p>ミニポートドライバーは、メッセージの MSI スピンロックを取得するために必要です。これは、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))"><strong>PORT_CONFIGURATION_INFORMATION (Storport)</strong></a>構造体の<strong>InterruptSynchronizationMode</strong>メンバーが<strong>InterruptSynchronizePerMessage</strong>に設定されている場合にのみ必要です。 このルールは、同期モードが<strong>InterruptSynchronizePerMessage</strong>の場合にのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquiremsispinlock" data-raw-source="[&lt;strong&gt;StorPortAcquireMSISpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquiremsispinlock)"><strong>StorPortAcquireMSISpinLock</strong></a>の呼び出しが行われることを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock&lt;/strong&gt;](storport-storportspinlock.md)"><strong>StorPortSpinLock</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>StorPortAcquireSpinLock</strong>経由で取得されたロックが<strong>Storportreleasespinlock ロック</strong>を使用してすぐに解放されることを確認します。 ミニポートドライバーは、既に取得されたロックを取得しようとした場合、または取得されなかったロックを解放しようとした場合に、規則に失敗します。 また、ディスパッチまたはキャンセルルーチンの終了時に、ドライバーはスピンロックを保持しないようにする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"><strong>StorPortSpinLock3</strong></a></p></td>
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"><strong>StorPortSpinLock3</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquirespinlock" data-raw-source="[&lt;strong&gt;StorPortAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquirespinlock)"><strong>StorPortAcquireSpinLock</strong></a>ルーチンのドキュメントで説明されているロック取得階層を検証します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock4.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock4&lt;/strong&gt;](storport-storportspinlock4.md)"><strong>StorPortSpinLock4</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>Storportspinlock ロック</strong>の<em>リリース</em>に相当します。 これは、 <strong>SpinLockRelease</strong>の規則に似ています。</p></td>
</tr>
</tbody>
</table>

 

**ロック規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[ロック]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを使用して**sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





