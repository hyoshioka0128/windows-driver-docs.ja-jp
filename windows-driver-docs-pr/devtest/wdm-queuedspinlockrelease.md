---
title: QueuedSpinLockRelease ルール (wdm)
description: QueuedSpinLockRelease ルールでは、厳密な交互に KeAcquireInStackQueuedSpinLock および KeReleaseInStackQueuedSpinLock への呼び出しが使用されることを指定します。
ms.assetid: 1d6ec912-ca38-4e8c-93c7-1c7aa4792676
ms.date: 05/21/2018
keywords:
- QueuedSpinLockRelease ルール (wdm)
topic_type:
- apiref
api_name:
- QueuedSpinLockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16fd659fb2df260c81e0b8242edbc1d627ebe5bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551850"
---
# <a name="queuedspinlockrelease-rule-wdm"></a>QueuedSpinLockRelease ルール (wdm)


**QueuedSpinLockRelease**への呼び出し規則を指定[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)と[ **KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130)厳密な代替構成で使用されます。

さらに、ディスパッチ、またはキャンセル ルーチンの末尾には、ドライバーは、その必要がありますなキューに置かれたスピンロックにも保持しません。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00040007) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>QueuedSpinLockRelease</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208#ddi-compliance-checking-additional" data-raw-source="[DDI compliance checking (additional)](https://msdn.microsoft.com/library/windows/hardware/hh454208#ddi-compliance-checking-additional)">DDI 準拠の確認 (追加)</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)
[**KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)
 

 





