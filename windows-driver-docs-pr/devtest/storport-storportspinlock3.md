---
title: StorPortSpinLock3 ルール (storport)
description: StorPortSpinLock3 ルールは、StorPortAcquireSpinLock ルーチンのドキュメントで説明されているロックの取得の階層を確認します。
ms.assetid: EC637CBD-A45D-44C6-8FAA-7035A36144B6
ms.date: 05/21/2018
keywords:
- StorPortSpinLock3 ルール (storport)
topic_type:
- apiref
api_name:
- StorPortSpinLock3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb1d5b2b59ef28c0dcae0d14c99269eb89ee3de2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342510"
---
# <a name="storportspinlock3-rule-storport"></a>StorPortSpinLock3 ルール (storport)


**StorPortSpinLock3**ルールの検証のドキュメントで説明されているロックの取得の階層、 [ **StorPortAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff567025)ルーチン。

Storport ミニポート ドライバーでは、既に保持されているロックの取得を間違った順序でロックを取得したりしないことを確認してください。 これらの誤りのいずれかにより、システムのデッドロックが発生します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortSpinLock3</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**StorPortAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff567025)
 

 





