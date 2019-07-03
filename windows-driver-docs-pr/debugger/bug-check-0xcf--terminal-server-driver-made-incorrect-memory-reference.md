---
title: バグ チェック 0xCF TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
description: TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE のバグ チェックでは、0x000000CF の値を持ちます。 これは、ことドライバーが正しくに移植されていない、ターミナル サーバーを示します。
ms.assetid: 1c3351d8-95df-4a12-a9c5-36aa6a5cf236
keywords:
- バグ チェック 0xCF TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
- TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4c8f36004a3022b0a9dccd9b1446d1cee9f2d0e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518895"
---
# <a name="bug-check-0xcf-terminalserverdrivermadeincorrectmemoryreference"></a>バグ チェック 0xCF:ターミナル\_SERVER\_ドライバー\_加えられた\_正しくない\_メモリ\_リファレンス


ターミナル\_SERVER\_ドライバー\_加えられた\_正しくない\_メモリ\_参照のバグ チェックが 0x000000CF の値を持ちます。 これは、ことドライバーが正しくに移植されていない、ターミナル サーバーを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="terminalserverdrivermadeincorrectmemoryreference-parameters"></a>ターミナル\_SERVER\_ドライバー\_加えられた\_正しくない\_メモリ\_参照パラメーター


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

ドライバーは、システム プロセスのコンテキストからセッションの領域のアドレスを参照しています。 おそらく、この結果、ドライバーがシステム ワーカー スレッドに項目をキューから。

このドライバーは、ターミナル サーバーのメモリ管理規則に従っている必要があります。

 

 




