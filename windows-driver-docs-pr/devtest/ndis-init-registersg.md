---
title: Init\_RegisterSG ルール (ndis)
description: Init\_RegisterSG ルールことを指定しますの初期化中には、通常、スキャッター/ギャザー リスト (SG) の登録する必要がありますいない done ミニポートが停止中または初期化プロセスで問題が発生した場合ドライバー。NdisMRegisterScatterGatherDma が MiniportInitializeEx 中に少なくとも 1 回呼び出される場合、MiniportHaltEx で少なくとも 1 回が NdisMDeregisterScatterGatherDma 関数に呼び出されます。
ms.assetid: c4d00be1-b44b-4769-bbe6-6128a742d088
ms.date: 05/21/2018
keywords:
- Init_RegisterSG ルール (ndis)
topic_type:
- apiref
api_name:
- Init_RegisterSG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d96e58d87328d61b7c4ff0733b45472880c81806
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550967"
---
# <a name="initregistersg-rule-ndis"></a>Init\_RegisterSG ルール (ndis)


Init\_RegisterSG ルールことを指定しますの初期化中には、通常、スキャッター/ギャザー リスト (SG) の登録する必要がありますいない done ミニポートが停止中または初期化プロセスで問題が発生した場合ドライバー。

場合**NdisMRegisterScatterGatherDma**中に少なくとも 1 回と呼びます**MiniportInitializeEx**、 **NdisMDeregisterScatterGatherDma**で関数を呼び出す必要があります少なくとも 1 回**MiniportHaltEx**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Init_RegisterSG</strong>ルール。</p>
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

[**NdisMDeregisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563581)
[**NdisMRegisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563659)
 

 





