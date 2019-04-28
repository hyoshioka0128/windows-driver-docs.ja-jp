---
title: スマート カード リーダーの状態
description: スマート カード リーダーの状態
ms.assetid: 7596ba27-206a-4590-aec0-c9009e7a12b6
keywords:
- スマート カードのドライバー WDK、リーダーを状態します。
- リーダーの状態の WDK スマート カード
- WDK スマート カードの状態
- ベンダーから提供されたドライバー WDK のスマート カード リーダーの状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75d8c9a777c878d8cdf682cfbe964bb47e2d58c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382535"
---
# <a name="smart-card-reader-states"></a>スマート カード リーダーの状態


## <span id="_ntovr_smart_card_reader_states"></span><span id="_NTOVR_SMART_CARD_READER_STATES"></span>


次の表では、スマート カード リーダーの状態を定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SCARD_UNKNOWN</p></td>
<td align="left"><p>リーダーのドライバーにリーダーの現在の状態に関する情報が含まれていないことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_ABSENT</p></td>
<td align="left"><p>リーダーにカードがないことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_PRESENT</p></td>
<td align="left"><p>カードは、リーダーに使用するための位置に移動されていないことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_SWALLOWED</p></td>
<td align="left"><p>カードは、リーダーと位置を使用することを示します。 カードが入っていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_POWERED</p></td>
<td align="left"><p>カードを活用すると、リーダーのドライバーは、カードの状態に関する追加情報を持たないことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_NEGOTIABLE</p></td>
<td align="left"><p>カードがリセットされました PTS ネゴシエーションを待機していることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_SPECIFIC</p></td>
<td align="left"><p>カードをリセットすると、特定の通信プロトコルが確立されていることを示します。</p></td>
</tr>
</tbody>
</table>

 

 

 





