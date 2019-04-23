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
ms.openlocfilehash: 0905251263f54bc33f1a80ca05ec60026b566576
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903498"
---
# <a name="bug-check-0xcf-terminalserverdrivermadeincorrectmemoryreference"></a>バグ チェック 0xCF:ターミナル\_SERVER\_ドライバー\_加えられた\_正しくない\_メモリ\_リファレンス


ターミナル\_SERVER\_ドライバー\_加えられた\_正しくない\_メモリ\_参照のバグ チェックが 0x000000CF の値を持ちます。 これは、ことドライバーが正しくに移植されていない、ターミナル サーバーを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


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

 

 




