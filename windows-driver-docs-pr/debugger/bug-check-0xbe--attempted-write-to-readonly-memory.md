---
title: Bug Check 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
description: ATTEMPTED_WRITE_TO_READONLY_MEMORY のバグ チェックでは、0x000000BE の値を持ちます。 ドライバーが読み取り専用メモリ セグメントに書き込もうとしている場合に発行されます。
ms.assetid: d6247828-09ae-4071-9b4f-917af29265bc
keywords:
- Bug Check 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
- ATTEMPTED_WRITE_TO_READONLY_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_WRITE_TO_READONLY_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08fc66ec8d146bbc70453c210f9573fe3c265fcc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573976"
---
# <a name="bug-check-0xbe-attemptedwritetoreadonlymemory"></a>バグ チェック 0xBE:試行\_書き込み\_TO\_READONLY\_メモリ


試行\_書き込み\_TO\_READONLY\_メモリのバグ チェックが 0x000000BE の値を持ちます。 ドライバーが読み取り専用メモリ セグメントに書き込もうとしている場合に発行されます。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="attemptedwritetoreadonlymemory-parameters"></a>試行\_書き込み\_TO\_READONLY\_メモリ パラメーター


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
<td align="left"><p>書き込みの試行の仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>PTE 内容</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。


<a name="remarks"></a>コメント
-------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。
 



