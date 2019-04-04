---
title: StorPortSpinLock ルール (storport)
description: このルールは、StorPortReleaseSpinLock 経由で StorPortAcquireSpinLock 経由で取得したロックがすぐに解放されるかを確認します。
ms.assetid: B7B918A0-3042-4961-8D33-EFDC15819D1F
ms.date: 05/21/2018
keywords:
- StorPortSpinLock ルール (storport)
topic_type:
- apiref
api_name:
- StorPortSpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b59f1711bb5dcdb1a8f05770cb405bda671e7f87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528017"
---
# <a name="storportspinlock-rule-storport"></a>StorPortSpinLock ルール (storport)


このルールの検証を使用して取得されるロックを**StorPortAcquireSpinLock**を使用して迅速にリリースされる**StorPortReleaseSpinLock**します。 ミニポート ドライバーが既に取得されるロックの取得を開こうとすると、またはしない取得したロックを解放しようとしている場合、ルールが失敗します。 さらに、ディスパッチ、またはキャンセル ルーチンの末尾には、ドライバー保持しないようにする、スピン ロックします。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortSpinLock</strong>ルール。</p>
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

[**StorPortAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff567025)
[**StorPortReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff567496)
 

 





