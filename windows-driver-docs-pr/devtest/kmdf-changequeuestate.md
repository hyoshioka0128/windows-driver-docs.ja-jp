---
title: ChangeQueueState ルール (kmdf)
description: ChangeQueueState ルールでは、WDF ドライバーが同時実行のスレッドから、キューの状態を変更しようとしていないまたはから変更する Ddi 1 つずつ、同じスレッド内で状態を呼び出さないことを指定します。
ms.assetid: C05A04E8-F8F2-4339-AAB7-FD62BE1DAAA2
ms.date: 05/21/2018
keywords:
- ChangeQueueState ルール (kmdf)
topic_type:
- apiref
api_name:
- ChangeQueueState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e9f1bc407c192dbb431fa9d229405c1c88f7edaa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550552"
---
# <a name="changequeuestate-rule-kmdf"></a>ChangeQueueState ルール (kmdf)


**ChangeQueueState**ルールは、WDF ドライバーが同時実行のスレッドから、キューの状態を変更しようとしていないまたはから変更する Ddi 1 つずつ、同じスレッド内で状態を呼び出さないことを指定します。 キューの状態が変化するコールバック関数は[ **WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)、 [ **WdfIoQueueStopSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548489)、[ **WdfIoQueuePurge**](https://msdn.microsoft.com/library/windows/hardware/ff548442)、[**WdfIoQueuePurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548449)、 [ **WdfIoQueueDrain** ](https://msdn.microsoft.com/library/windows/hardware/ff547406)、 [ **WdfIoQueueDrainSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff547412)、 [ **WdfIoQueueStopAndPurge** ](https://msdn.microsoft.com/library/windows/hardware/hh439289)と[ **WdfIoQueueStopAndPurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/hh439293)します。 キューの状態の変更が既に進行中の場合、これらの Ddi が呼び出された場合、クラッシュや応答しなくなるコンピューターがなります。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ChangeQueueState</strong>ルール。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)
[**WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)
 [ **WdfIoQueueDrain**](https://msdn.microsoft.com/library/windows/hardware/ff547406)
[**WdfIoQueueDrainSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff547412) 
 [ **WdfIoQueuePurge**](https://msdn.microsoft.com/library/windows/hardware/ff548442)
[**WdfIoQueuePurgeSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548449) 
 [**WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)
[**WdfIoQueueStopAndPurge** ](https://msdn.microsoft.com/library/windows/hardware/hh439289) 
 [ **WdfIoQueueStopAndPurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/hh439293)
[**WdfIoQueueStopSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548489)
 

 





