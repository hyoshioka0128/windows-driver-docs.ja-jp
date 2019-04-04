---
title: Irql\_タイマー\_関数ルール (ndis)
description: Irql\_タイマー\_関数の規則は、適切な IRQL レベルで NDIS タイマー サービスの関数を呼び出す必要がありますを指定します。
ms.assetid: 4c946f79-7661-4ff6-b2a3-1a5851c9e215
ms.date: 05/21/2018
keywords:
- Irql_Timer_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Timer_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a1a54b8a73bd9052ac44300156456445122d06b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556600"
---
# <a name="irqltimerfunction-rule-ndis"></a>Irql\_タイマー\_関数ルール (ndis)


Irql\_タイマー\_関数の規則は、適切な IRQL レベルで NDIS タイマー サービスの関数を呼び出す必要がありますを指定します。

このルールは、次の NDIS 関数を確認します。

**NdisAllocateTimerObject**
**NdisCancelTimerObject**
**NdisFreeTimerObject**
**NdisSetTimerObject**

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_Timer_Function</strong>ルール。</p>
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

[**NdisAllocateTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff561618)
[**NdisCancelTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff561624)
[**NdisFreeTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff562605)
[**NdisSetTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff564563)








