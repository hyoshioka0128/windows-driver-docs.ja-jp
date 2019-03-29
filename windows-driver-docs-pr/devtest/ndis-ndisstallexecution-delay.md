---
title: NdisStallExecution\_遅延ルール (ndis)
description: NdisStallExecution\_遅延ルールでは、NdisStallExecution を MicrosecondsToStall 50 マイクロ秒よりも大きい値を使用して呼び出すことはありません必要がありますを指定します。
ms.assetid: 4c9368d0-4da7-4adc-bc63-4f21af90b682
ms.date: 05/21/2018
keywords:
- NdisStallExecution_Delay ルール (ndis)
topic_type:
- apiref
api_name:
- NdisStallExecution_Delay
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 624535ea66f6400aead6adb24cbcc157e27519d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570456"
---
# <a name="ndisstallexecutiondelay-rule-ndis"></a>NdisStallExecution\_遅延ルール (ndis)


NdisStallExecution\_遅延ルールを指定する**NdisStallExecution**の値を使用して呼び出す必要がありますしない*MicrosecondsToStall* 50 マイクロ秒よりも大きい。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisStallExecution_Delay</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**NdisStallExecution**](https://msdn.microsoft.com/library/windows/hardware/ff564568)
 

 





