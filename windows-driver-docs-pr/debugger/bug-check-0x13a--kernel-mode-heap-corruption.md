---
title: バグ チェック 0x13A KERNEL_MODE_HEAP_CORRUPTION
description: KERNEL_MODE_HEAP_CORRUPTION のバグ チェックでは、0x0000013A の値を持ちます。 これは、カーネル モードのヒープ マネージャーによって、ヒープの破損が検出されたことを示します。
ms.assetid: 806669B3-B811-462A-A3B6-2F583BF0E19A
keywords:
- バグ チェック 0x13A KERNEL_MODE_HEAP_CORRUPTION
- KERNEL_MODE_HEAP_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_MODE_HEAP_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d56d1644afd9458e8714e7715051d3f24392f6d0
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520227"
---
# <a name="bug-check-0x13a-kernelmodeheapcorruption"></a>バグ チェック 0x13A:カーネル\_モード\_ヒープ\_破損


カーネル\_モード\_ヒープ\_破損バグ チェックが 0x0000013A の値を持ちます。 これは、カーネル モードのヒープ マネージャーによって、ヒープの破損が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="kernelmodeheapcorruption-parameters"></a>カーネル\_モード\_ヒープ\_破損パラメーター


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
<td align="left"><p>種類の破損が検出されました</p>
0x3:破損しているエントリのヘッダーが検出されました。
0x4:複数のエントリが破損しているヘッダーが検出されました。
0x5。大規模な割り当てでエントリが破損しているヘッダーが検出されました。
0x6:バッファー オーバーランの一貫性のある機能では、破損が検出されました。
0x7:バッファー アンダーランで一貫性のある機能では、破損が検出されました。
0x8:ブロックを解放しますが、ビジー状態のブロックに対してのみ有効ですが、操作に渡されました。
0x9:現在の操作に無効な引数が指定されました。
0 xa:無料使用後のエラーで一貫性のある機能で、破損が検出されました。
0 xb:現在の操作が正しくないヒープが指定されました。
0 xc:破損のフリー リストが検出されました。
0 xd:ヒープでは、フリー リスト以外のリストでリストの破損が検出されました。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">破損が報告されるヒープのアドレス</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">アドレスの破損が検出されました</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




