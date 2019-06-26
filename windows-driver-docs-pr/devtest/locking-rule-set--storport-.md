---
title: ロックの規則セット (Storport)
description: ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。
ms.assetid: FBB75F07-E689-4B7C-B053-E0B6A3772764
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: dd8235333b23748222c947d08a495ef37c1b52f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354783"
---
# <a name="locking-rule-set-storport"></a>ロックの規則セット (Storport)


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
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock&lt;/strong&gt;](storport-cancelspinlock.md)"><strong>CancelSpinLock</strong></a></p></td>
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock Rule (Storport)&lt;/strong&gt;](storport-cancelspinlock.md)"> <strong>CancelSpinLock ルール (Storport)</strong> </a>ルールことを確認しますへの各呼び出し<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))"> <strong>IoAcquireCancelSpinLock</strong> </a>速やかに続けて、呼び出す<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))"> <strong>IoReleaseCancelSpinLock</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"> <strong>QueuedSpinLock</strong> </a>ルール - スタックでの検証を使用して取得されるスピン ロックをキューに置かれた<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>を使用してすぐに解放<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"> <strong>KeReleaseInStackQueuedSpinLock</strong></a>します。 さらに、ディスパッチ、またはキャンセル ルーチンの末尾には、ドライバー保持しないようにするすべてのロック。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](storport-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p>このルールは、ドライバーは呼び出さないことを確認します。 <strong>KeReleaseInStackQueuedSpinLock</strong>最初に使用してロックの獲得<strong>KeAcquireInStackQueuedSpinLock</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](storport-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p>このルールを確認する呼び出しを<strong>KeAcquireSpinLock</strong>への呼び出しの後にすぐに<strong>KeReleaseSpinlock</strong>。 ドライバーを呼び出す場合<strong>KeAcquireSpinLockRaiseToDpc</strong>または<strong>KeAcquireSpinLock</strong>ルールが失敗したロックを解放する前にもう一度です。 さらに、ディスパッチ、またはキャンセル ルーチンを終了する前に、ドライバーは、スピン ロックを解放する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](storport-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p>このルールを確認する呼び出しを<strong>KeAcquireSpinLockRaiseToDpc</strong>への呼び出しの後にすぐに<strong>KeReleaseSpinlock</strong>。 ドライバーを呼び出す場合<strong>KeAcquireSpinLock</strong>または<strong>KeAcquireSpinLockRaiseToDpc</strong>ルールが失敗したロックを解放する前にもう一度です。 さらに、ディスパッチ、またはキャンセル ルーチンを終了する前に、ドライバーは、スピン ロックを解放する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](storport-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>このルールは、ドライバーが経由でのロックの解放を試行しないことを確認します<strong>KeReleaseSpinLock</strong>取得経由で最初に<strong>KeAquireSpinlock</strong>または<strong>KeAcquireSpinLockRaiseToDpc。</strong> ルールは、取得したスピン ロックが解放されるときに渡されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](storport-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p>このルールは、ことを確認、<strong>います</strong>と<strong>IoCompleteRequest</strong>ルーチンは、スピン ロックを保持しているときに呼び出されません。 ルールの追跡、いつでも、スピン ロックの数と、その番号がない場合 0 いずれかのルーチンが呼び出されると、ドライバーが、規則に失敗します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportmsilock.md" data-raw-source="[&lt;strong&gt;StorPortMSILock&lt;/strong&gt;](storport-storportmsilock.md)"><strong>StorPortMSILock</strong></a></p></td>
<td align="left"><p>のみの場合、メッセージの MSI スピン ロックを取得するミニポート ドライバーが必要、 <strong>InterruptSynchronizationMode</strong>のメンバー、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))"> <strong>PORT_CONFIGURATION_INFORMATION (Storport)</strong></a>構造に設定されている<strong>InterruptSynchronizePerMessage</strong>します。 このルールへの呼び出しを検証<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportacquiremsispinlock" data-raw-source="[&lt;strong&gt;StorPortAcquireMSISpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportacquiremsispinlock)"> <strong>StorPortAcquireMSISpinLock</strong> </a>同期モードの場合のみ行われます<strong>InterruptSynchronizePerMessage</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock&lt;/strong&gt;](storport-storportspinlock.md)"><strong>StorPortSpinLock</strong></a></p></td>
<td align="left"><p>このルールの検証を使用して取得されるロックを<strong>StorPortAcquireSpinLock</strong>を使用して迅速にリリースされる<strong>StorPortReleaseSpinLock</strong>します。 ミニポート ドライバーが既に取得されるロックの取得を開こうとすると、またはしない取得したロックを解放しようとしている場合、ルールが失敗します。 さらに、ディスパッチ、またはキャンセル ルーチンの末尾には、ドライバー保持しないようにする、スピン ロックします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"><strong>StorPortSpinLock3</strong></a></p></td>
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"> <strong>StorPortSpinLock3</strong> </a>ルールの検証のドキュメントで説明されているロックの取得の階層、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportacquirespinlock" data-raw-source="[&lt;strong&gt;StorPortAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportacquirespinlock)"> <strong>StorPortAcquireSpinLock</strong></a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock4.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock4&lt;/strong&gt;](storport-storportspinlock4.md)"><strong>StorPortSpinLock4</strong></a></p></td>
<td align="left"><p>このルールは、<em>リリース</em>対応の<strong>StorPortSpinLock</strong>します。 似ています、 <strong>SpinLockRelease</strong>ルール。</p></td>
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

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





