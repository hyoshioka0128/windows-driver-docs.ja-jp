---
title: CancelSpinlockRelease ルール (wdm)
description: CancelSpinlockRelease ルールでは、厳密な交互に IoAcquireCancelSpinLock および IoReleaseCancelSpinLock への呼び出しが使用されることを指定します。 つまり、IoAcquireCancelSpinLock、呼び出すたびには、IoReleaseCancelSpinLock に対応する呼び出しが必要です。
ms.assetid: dba280c7-18ac-4d87-8d45-d30c214ef90e
ms.date: 05/21/2018
keywords:
- CancelSpinlockRelease ルール (wdm)
topic_type:
- apiref
api_name:
- CancelSpinlockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bc71bbf3c78b6f62839e19f6db5d56392fcbc21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570457"
---
# <a name="cancelspinlockrelease-rule-wdm"></a>CancelSpinlockRelease ルール (wdm)


**CancelSpinlockRelease**への呼び出し規則を指定[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)と[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)厳密な代替構成で使用されます。 すべての呼び出しには、 **IoAcquireCancelSpinLock**に対応する呼び出しがあります。 **IoReleaseCancelSpinLock**します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CancelSpinlockRelease</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**IoAcquireCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff548196)
[**IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)
 

 





