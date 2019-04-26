---
title: QueuedSpinLockRelease ルール (storport)
description: このルールは、最初 KeAcquireInStackQueuedSpinLock を使用してロックを取得しなくても KeReleaseInStackQueuedSpinLock はドライバーによって呼び出すしないことを確認します。
ms.assetid: F523D77B-F848-4128-9B6D-7D92E01C4632
ms.date: 05/21/2018
keywords:
- QueuedSpinLockRelease ルール (storport)
topic_type:
- apiref
api_name:
- QueuedSpinLockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40d3c81f9281bdbf09b6f55f8103b6529db083b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345733"
---
# <a name="queuedspinlockrelease-rule-storport"></a>QueuedSpinLockRelease ルール (storport)


このルールは、ドライバーは呼び出さないことを確認します。 **KeReleaseInStackQueuedSpinLock**最初に使用してロックの獲得**KeAcquireInStackQueuedSpinLock**します。

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

<a name="applies-to"></a>適用対象
----------

[**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)
[**KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)
 

 





