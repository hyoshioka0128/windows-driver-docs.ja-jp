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
ms.openlocfilehash: 66c9fd99d3c6b40cddb340c686bf28bb845b5687
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353679"
---
# <a name="bug-check-0x13a-kernelmodeheapcorruption"></a>バグ チェック 0x13A:カーネル\_モード\_ヒープ\_破損


カーネル\_モード\_ヒープ\_破損バグ チェックが 0x0000013A の値を持ちます。 これは、カーネル モードのヒープ マネージャーによって、ヒープの破損が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


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

 

 

 




