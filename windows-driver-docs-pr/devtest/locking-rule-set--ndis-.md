---
title: ロックの規則の設定 (NDIS)
description: ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。
ms.assetid: 1123A246-7833-4EAB-B1B8-0C71413CE86B
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 01d779c83a934bd5037ad5c7e82663b621902564
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527266"
---
# <a name="locking-rule-set-ndis"></a>ロックの規則の設定 (NDIS)


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
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>スピンロック</strong></a>ルールは、NDIS スピン ロック インターフェイスの正しい使用を確認します。 このルールへの呼び出しを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff560699" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560699)"> <strong>NdisAcquireSpinLock</strong> </a>は、スピンロックがロックされていない状態の場合にのみ行われます。 このルールでは、ミニポート ハンドラー ルーチンを終了する前に、スピンロックが解放されるも検証します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"><strong>SpinLockBalanced</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"> <strong>SpinLockBalanced</strong> </a>ルールは、スピン ロックを取得する関数の呼び出しの数が同じスピンロックを解放関数への呼び出しの数に等しいことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"><strong>SpinLockDpr</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"> <strong>SpinLockDpr</strong> </a>ルールは、NDIS スピン ロック インターフェイスの正しい使用を確認します。</p>
<p>このルールへの呼び出しを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff561749" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561749)"> <strong>NdisDprAcquireSpinLock</strong> </a>は、スピン ロックがロックされていない状態の場合にのみ行われます。 このルールでは、ミニポート ハンドラー ルーチンを終了する前に、スピン ロックが解放されるも検証します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"><strong>SpinLockDprRelease</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"> <strong>SpinLockDprRelease</strong> </a>への呼び出し規則を確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff560699" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560699)"> <strong>NdisAcquireSpinLock</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff561749" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561749)"> <strong>NdisDprAcquireSpinLock</strong> </a>スピンロックときのみ呼び出される、&quot;ロックされていない&quot;状態。 このルールでは、ミニポート ハンドラーを終了する前に、スピンロックのルーチンがされたリリースも確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](ndis-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>SpinLockRelease ルールでは、ドライバーが、スピン ロックを解放する必要がありますされないことを指定します (<a href="https://msdn.microsoft.com/library/windows/hardware/ff564524" data-raw-source="[&lt;strong&gt;NdisReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564524)"><strong>NdisReleaseSpinLock</strong></a>) 最初に取得します。</p></td>
</tr>
</tbody>
</table>

 

**ロックの規則を選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**ロック**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Locking.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





