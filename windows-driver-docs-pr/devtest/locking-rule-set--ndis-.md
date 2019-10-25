---
title: ロックの規則セット (NDIS)
description: これらの規則を使用して、ドライバーが共有リソースを正しく管理していることを確認します。
ms.assetid: 1123A246-7833-4EAB-B1B8-0C71413CE86B
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3fa01d7b48e2891b655cc667df4b397b8225b53a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839413"
---
# <a name="locking-rule-set-ndis"></a>ロックの規則セット (NDIS)


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
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>スピンロック</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>スピン</strong></a>ロック規則は、NDIS スピンロックインターフェイスが正しく使用されていることを確認します。 このルールは、スピンロックがロック解除状態の場合にのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock)"><strong>NdisAcquireSpinLock</strong></a>の呼び出しが行われるように指定します。 また、このルールは、ミニポートハンドラールーチンが終了する前にスピンロックが解放されていることを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"><strong>SpinLockBalanced</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"><strong>SpinLockBalanced</strong></a>ルールは、スピンロックを取得する関数への呼び出しの数が、同じスピンロックを解放する関数の呼び出し回数と同じであることを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"><strong>SpinLockDpr</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"><strong>SpinLockDpr</strong></a>規則は、NDIS スピンロックインターフェイスの正しい使用を検証します。</p>
<p>このルールは、スピンロックがロック解除された状態の場合にのみ、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock)"><strong>NdisDprAcquireSpinLock</strong></a>の呼び出しが行われるように指定します。 また、このルールは、ミニポートハンドラールーチンが終了する前にスピンロックが解放されたことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"><strong>SpinLockDprRelease</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"><strong>SpinLockDprRelease</strong></a>ルールは、スピンロックが "ロック解除" 状態である場合にのみ、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock)"><strong>NdisAcquireSpinLock</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock)"><strong>NdisDprAcquireSpinLock</strong></a>の呼び出しが呼び出されることを確認します。 また、このルールでは、ミニポートハンドラルーチンを終了する前にスピンロックが解放されたことも確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](ndis-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>SpinLockRelease 規則は、ドライバーがスピンロック (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleasespinlock" data-raw-source="[&lt;strong&gt;NdisReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleasespinlock)"><strong>NdisReleaseSpinLock</strong></a>) を最初に取得せずに解放しないことを指定します。</p></td>
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

 

 





