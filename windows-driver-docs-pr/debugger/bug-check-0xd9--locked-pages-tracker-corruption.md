---
title: Bug Check 0xD9 LOCKED_PAGES_TRACKER_CORRUPTION
description: LOCKED_PAGES_TRACKER_CORRUPTION のバグ チェックでは、0x000000D9 の値を持ちます。 これは、ロックされているページ追跡の内部構造が破損していることを示します。
ms.assetid: 81011ce6-159c-448f-9f68-7b1eb949ff68
keywords:
- Bug Check 0xD9 LOCKED_PAGES_TRACKER_CORRUPTION
- LOCKED_PAGES_TRACKER_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- LOCKED_PAGES_TRACKER_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc24da4c44399f1e548c6ee2412ed0344b3954d3
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518851"
---
# <a name="bug-check-0xd9-lockedpagestrackercorruption"></a>バグ チェック 0xD9:ロックされている\_ページ\_トラッカー\_破損


LOCKED\_ページ\_トラッカー\_破損バグ チェックが 0x000000D9 の値を持ちます。 これは、ロックされているページ追跡の内部構造が破損していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="lockedpagestrackercorruption-parameters"></a>ロックされている\_ページ\_トラッカー\_破損パラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>構造体を追跡する内部ロックのアドレス</p></td>
<td align="left"><p>メモリの記述子のリストのアドレス</p></td>
<td align="left"><p>現在のプロセスのロックされているページ数</p></td>
<td align="left"><p>MDL は、2 回、同じプロセスのリストに挿入します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>構造体を追跡する内部ロックのアドレス</p></td>
<td align="left"><p>メモリの記述子のリストのアドレス</p></td>
<td align="left"><p>現在のプロセスのロックされているページ数</p></td>
<td align="left"><p>MDL は、システム全体の一覧に 2 回挿入します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>見つかった最初の追跡の内部構造体のアドレス</p></td>
<td align="left"><p>構造体を追跡する内部ロックのアドレス</p></td>
<td align="left"><p>メモリの記述子のリストのアドレス</p></td>
<td align="left"><p>解放されるときにプロセスの一覧に 2 回 MDL が見つかりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>構造体を追跡する内部ロックのアドレス</p></td>
<td align="left"><p>メモリの記述子のリストのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MDL は、システム全体の一覧内で見つかりました無料削除した後。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

エラーは、パラメーター 1 の値によって示されます。

 

 




