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
ms.openlocfilehash: 13f79af8376ad977854d05d3c64a9c436ee94b2a
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392363"
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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>Init_RegisterSG</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisMDeregisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterscattergatherdma)
[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterscattergatherdma)
 

 





