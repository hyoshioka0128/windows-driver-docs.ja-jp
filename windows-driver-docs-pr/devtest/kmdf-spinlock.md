---
title: Spinlock ルール (kmdf)
description: Spinlock ルールでは、厳密な交互に KeAcquireSpinLock や KeAcquireSpinLockRaiseToDpc KeReleaseSpinlock への呼び出しが使用されることを指定します。
ms.assetid: 911E4350-851F-4AC4-B982-B2B4B974C243
ms.date: 05/21/2018
keywords:
- Spinlock ルール (kmdf)
topic_type:
- apiref
api_name:
- Spinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b8c7e765a70990080b7aa5bfaae7cdccca1af5be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557133"
---
# <a name="spinlock-rule-kmdf"></a>Spinlock ルール (kmdf)


**スピンロック**への呼び出し規則を指定[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)または[ **KeAcquireSpinLockRaiseToDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff551928)と[ **KeReleaseSpinlock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)厳密な代替構成で使用されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、<strong>スピンロック</strong>ルール。</p>
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

[**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)
[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
 

 





