---
title: バグ チェック 0 xfd DIRTY_NOWRITE_PAGES_CONGESTION
description: DIRTY_NOWRITE_PAGES_CONGESTION のバグ チェックでは、0x000000FD の値を持ちます。 これは、基本的なシステム操作を続行する使用可能な空きページがないことを示します。
ms.assetid: b657fffe-8331-4b4f-9d29-fea8ee1e1682
keywords:
- バグ チェック 0 xfd DIRTY_NOWRITE_PAGES_CONGESTION
- DIRTY_NOWRITE_PAGES_CONGESTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DIRTY_NOWRITE_PAGES_CONGESTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e5c86cda8e607e5f6570d5ab38c33138c074b4ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367599"
---
# <a name="bug-check-0xfd-dirtynowritepagescongestion"></a>バグ チェック 0xFD:ダーティ\_NOWRITE\_ページ\_輻輳


DIRTY\_NOWRITE\_ページ\_輻輳のバグ チェックが 0x000000FD の値を持ちます。 これは、基本的なシステム操作を続行する使用可能な空きページがないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="dirtynowritepagescongestion-parameters"></a>ダーティ\_NOWRITE\_ページ\_輻輳パラメーター


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
<td align="left"><p>1</p></td>
<td align="left"><p>ダーティ ページの合計数</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>書き込み不可のダーティ ページの数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>書き込みエラー状態は最も最近変更されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックは、メモリ管理に対する「書き込みいない」として、関連するファイルをマークした後にこれらのページ書き込みに変更された書き込み不可のページを所有するコンポーネントが失敗したために通常発生します。 これは、ドライバーのバグを示します。

<a name="resolution"></a>解決方法
----------

詳細についてはに関する問題の原因で、ドライバーを使用して、 [ **! vm 3** ](-vm.md)拡張機能、続けて[ **! memusage 1** ](-memusage.md)します。

 

 




