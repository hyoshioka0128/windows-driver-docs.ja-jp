---
title: バグ チェック 0x30 SET_OF_INVALID_CONTEXT
description: SET_OF_INVALID_CONTEXT のバグ チェックでは、0x00000030 の値を持ちます。 これは、トラップ フレームのスタック ポインターが無効な値を持っていることを示します。
ms.assetid: 77e86390-e387-4ffd-96dd-c32a98939c3a
keywords:
- バグ チェック 0x30 SET_OF_INVALID_CONTEXT
- SET_OF_INVALID_CONTEXT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SET_OF_INVALID_CONTEXT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e89759e48f404134f9bed870c0fdbe46e3223f2
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519530"
---
# <a name="bug-check-0x30-setofinvalidcontext"></a>バグ チェック 0x30:設定\_の\_無効な\_コンテキスト


セット\_の\_無効な\_コンテキストのバグ チェックが 0x00000030 の値を持ちます。 これは、トラップ フレームのスタック ポインターが無効な値を持っていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="setofinvalidcontext-parameters"></a>設定\_の\_無効な\_コンテキスト パラメーター


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
<td align="left"><p>新しいスタック ポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>以前のスタック ポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>トラップのフレームのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックでは、いくつかのルーチンが現在のスタック ポインターの値より小さい値にトラップ フレームのスタック ポインターを設定しようとしたときに発生します。

このエラーはキャッチされず場合、スタック ポインターがスタックが無効にする をポイントで実行するカーネルが発生します。

 

 




