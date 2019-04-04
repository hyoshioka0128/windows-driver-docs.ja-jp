---
title: Init\_RegisterInterrupt ルール (ndis)
description: Init\_RegisterInterrupt ルールでは、ミニポート ドライバーが停止中または初期化プロセスで問題が発生した場合にする必要がありますの初期化中には、通常、割り込みの登録の元に戻すを解除することを指定します。NdisMRegisterInterruptEx は MiniportInitializeEx 中に少なくとも 1 回呼び出されると、NdisMDeregisterInterruptEx 関数が MiniportHaltEx で少なくとも 1 つ回呼び出される必要があります。
ms.assetid: f12cc1b9-396b-4351-ad13-c1750b54b709
ms.date: 05/21/2018
keywords:
- Init_RegisterInterrupt ルール (ndis)
topic_type:
- apiref
api_name:
- Init_RegisterInterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d06113268ccf06453eb774c94b205f1924808e7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577906"
---
# <a name="initregisterinterrupt-rule-ndis"></a>Init\_RegisterInterrupt ルール (ndis)


Init\_RegisterInterrupt ルールでは、ミニポート ドライバーが停止中または初期化プロセスで問題が発生した場合にする必要がありますの初期化中には、通常、割り込みの登録の元に戻すを解除することを指定します。

場合**NdisMRegisterInterruptEx**中に少なくとも 1 回と呼びます**MiniportInitializeEx**、 **NdisMDeregisterInterruptEx**関数は、少なくとも 1 回呼び出す必要があります**MiniportHaltEx**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Init_RegisterInterrupt</strong>ルール。</p>
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

[**NdisMDeregisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563575)
[**NdisMRegisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563649)
 

 





