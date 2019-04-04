---
title: QueuedSpinLock ルール (storport)
description: KeAcquireInStackQueuedSpinLock を使用して取得されるスタックでキューに置かれたスピン ロックがすぐに解放される KeReleaseInStackQueuedSpinLock を使用して QueuedSpinLock ルールを確認します。
ms.assetid: A5D80CD8-715F-4629-B3B3-E4AC0A201919
ms.date: 05/21/2018
keywords:
- QueuedSpinLock ルール (storport)
topic_type:
- apiref
api_name:
- QueuedSpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37b42de30b120feb2efbfe7c68f67b32b2e99914
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530381"
---
# <a name="queuedspinlock-rule-storport"></a>QueuedSpinLock ルール (storport)


**QueuedSpinLock**ルール - スタックでの検証を使用して取得されるスピン ロックをキューに置かれた[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899) を使用して迅速にリリース[**KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)します。 さらに、ディスパッチ、またはキャンセル ルーチンの末尾には、ドライバー保持しないようにするすべてのロック。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>QueuedSpinLock</strong>ルール。</p>
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

[**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)
[**KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)
 

 





