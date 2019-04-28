---
title: バグ チェック 0 xcc PAGE_FAULT_IN_FREED_SPECIAL_POOL
description: PAGE_FAULT_IN_FREED_SPECIAL_POOL のバグ チェックでは、0x000000CC の値を持ちます。 これは、システムが既に解放されているメモリを参照することを示します。
ms.assetid: 77823c38-76eb-49ca-aaf4-3cf5994a0525
keywords:
- バグ チェック 0 xcc PAGE_FAULT_IN_FREED_SPECIAL_POOL
- PAGE_FAULT_IN_FREED_SPECIAL_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_FREED_SPECIAL_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de3bccab64d3a52c6ad3220b183aa5c3012f90b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371780"
---
# <a name="bug-check-0xcc-pagefaultinfreedspecialpool"></a>バグ チェック 0xCC:ページ\_フォールト\_IN\_FREED\_特殊\_プール


ページ\_フォールト\_IN\_FREED\_特殊\_プールのバグ チェックが 0x000000CC の値を持ちます。 これは、システムが既に解放されているメモリを参照することを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="pagefaultinfreedspecialpool-parameters"></a>ページ\_フォールト\_IN\_FREED\_特殊\_プールのパラメーター


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
<td align="left"><p>参照されているメモリ アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>メモリ (わかる場合) を参照されているアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

<a name="cause"></a>原因
-----

Driver Verifier の特別なプール オプションには、これは、以前にアクセスするメモリを解放して、システムがキャッチします。 これは通常、システム ドライバーの同期の問題を示します。

特別なプールについては、Windows ドライバー キットの Driver Verifier のセクションを参照してください。

<a name="remarks"></a>注釈
-------

これで保護することはできません、 **- お試しくださいを除く**ハンドラー--プローブによってのみ保護できます。

 

 




