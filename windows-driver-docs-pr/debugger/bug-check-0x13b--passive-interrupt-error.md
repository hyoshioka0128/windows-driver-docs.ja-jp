---
title: バグ チェック 0x13B PASSIVE_INTERRUPT_ERROR
description: PASSIVE_INTERRUPT_ERROR のバグ チェックでは、0x0000013B の値を持ちます。 これは、カーネルのパッシブ レベル割り込みに関する問題が検出されたことを示します。
ms.assetid: 6C921FCB-B945-4909-BAD3-1DBD6E3CAA54
keywords:
- バグ チェック 0x13B PASSIVE_INTERRUPT_ERROR
- PASSIVE_INTERRUPT_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PASSIVE_INTERRUPT_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3795a076eb9ad0864ac80d86a7693778a4455e3c
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520226"
---
# <a name="bug-check-0x13b-passiveinterrupterror"></a>バグ チェック 0x13B:パッシブ\_INTERRUPT\_エラー


パッシブ\_INTERRUPT\_エラーのバグ チェックが 0x0000013B の値を持ちます。 これは、カーネルのパッシブ レベル割り込みに関する問題が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="passiveinterrupterror-parameters"></a>パッシブ\_INTERRUPT\_エラー パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>検出されたエラーの種類</p>
0x1:ドライバーは、割り込みのスピン ロックを取得しようとしましたが、パッシブ レベル割り込みオブジェクトに渡されます。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パッシブ レベル割り込みに対する KINTERRUPT オブジェクトのアドレス。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">予約済み</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




