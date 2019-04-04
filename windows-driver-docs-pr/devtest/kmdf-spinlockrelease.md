---
title: SpinlockRelease ルール (kmdf)
description: SpinlockRelease ルールでは、KMDF コールバック内でバランスの取れた方法で KeAcquireSpinLock、KeAcquireSpinLockRaiseToDpc、および KeReleaseSpinLock への呼び出しが使用されることを指定します。 任意の KMDF コールバック ルーチンの末尾には、ドライバーは、スピン ロックを保持しないようにします。
ms.assetid: 23BEB857-309D-4C11-A361-D72F87C84154
ms.date: 05/21/2018
keywords:
- SpinlockRelease ルール (kmdf)
topic_type:
- apiref
api_name:
- SpinlockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ec96ad055691e66ead6059f9470fb2cce3d275a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530211"
---
# <a name="spinlockrelease-rule-kmdf"></a>SpinlockRelease ルール (kmdf)


**SpinlockRelease**への呼び出し規則を指定[ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)、 [ **KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)、および[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145) KMDF コールバック内でバランスの取れた方法で使用されます。 任意の KMDF コールバック ルーチンの末尾には、ドライバーは、スピン ロックを保持しないようにします。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SpinlockRelease</strong>ルール。</p>
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

[**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)
[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
 

 





