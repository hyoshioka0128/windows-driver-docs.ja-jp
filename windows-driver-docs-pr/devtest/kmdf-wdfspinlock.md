---
title: WdfSpinlock ルール (kmdf)
description: WdfSpinlock ルールでは、WdfSpinLockAcquire メソッドの呼び出しが WdfSpinlockRelease で厳密な代替構成で使用されることを指定します。
ms.assetid: bf95509a-29f7-462d-b883-39aca4193ebb
ms.date: 05/21/2018
keywords:
- WdfSpinlock ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfSpinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ceb1195e0c9cac297d4382f96c552d739716135b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559312"
---
# <a name="wdfspinlock-rule-kmdf"></a>WdfSpinlock ルール (kmdf)


**WdfSpinlock**への呼び出し規則の指定、 [ **WdfSpinLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff550040)メソッドに厳密な代替構成で使用[ **WdfSpinlockRelease**](kmdf-wdfspinlockrelease.md)します。 KMDF コールバック ルーチンの末尾には、ドライバー保持しないようにするフレームワーク spinlock オブジェクトを以前の呼び出しによって取得された**WdfSpinLockAcquire**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WdfSpinlock</strong>ルール。</p>
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

[**WdfSpinLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff550040)
[**WdfSpinLockCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550042)
[**WdfSpinLockRelease**](https://msdn.microsoft.com/library/windows/hardware/ff550044)
 

 





