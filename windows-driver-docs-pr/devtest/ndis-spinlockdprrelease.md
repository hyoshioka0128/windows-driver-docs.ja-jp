---
title: SpinLockDprRelease ルール (ndis)
description: SpinLockDprRelease ルールでは、スピンロックときのみ、NdisAcquireSpinLock または NdisDprAcquireSpinLock への呼び出しが呼び出されることを確認、\ 0034; ロックを解除 \ 0034;状態。
ms.assetid: B726B1AD-F49D-479B-AF1B-99E8901E2315
ms.date: 05/21/2018
keywords:
- SpinLockDprRelease ルール (ndis)
topic_type:
- apiref
api_name:
- SpinLockDprRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e3d36857f389524d2d18077493f3487c8399e05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531189"
---
# <a name="spinlockdprrelease-rule-ndis"></a>SpinLockDprRelease ルール (ndis)


**SpinLockDprRelease**への呼び出し規則を確認します[ **NdisAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff560699)または[ **NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749)スピンロックが「ロック解除」状態のときにのみ呼び出されます。 このルールでは、ミニポート ハンドラーを終了する前に、スピンロックのルーチンがされたリリースも確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SpinLockDprRelease</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff560699)
[**NdisAllocateSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561617)
[**NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749) 
 [ **NdisDprReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561753)
[**NdisReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff564524)
 

 





