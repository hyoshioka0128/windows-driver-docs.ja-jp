---
title: バグ チェック 0xF7 DRIVER_OVERRAN_STACK_BUFFER
description: DRIVER_OVERRAN_STACK_BUFFER のバグ チェックでは、0x000000F7 の値を持ちます。 これは、ドライバーがスタック ベースのバッファー オーバーランが発生することを示します。
ms.assetid: 5981b5e0-90c1-486e-8bbf-2778f2595f6b
keywords:
- バグ チェック 0xF7 DRIVER_OVERRAN_STACK_BUFFER
- DRIVER_OVERRAN_STACK_BUFFER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_OVERRAN_STACK_BUFFER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e276533ddc3e9ed8eb608b8b271acd6c8b3e7701
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518715"
---
# <a name="bug-check-0xf7-driveroverranstackbuffer"></a>バグ チェック 0xF7:ドライバー\_OVERRAN\_スタック\_バッファー


ドライバー\_OVERRAN\_スタック\_バッファーのバグ チェックが 0x000000F7 の値を持ちます。 これは、ドライバーがスタック ベースのバッファー オーバーランが発生することを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="driveroverranstackbuffer-parameters"></a>ドライバー\_OVERRAN\_スタック\_バッファー パラメーター


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
<td align="left"><p>スタックから実際のセキュリティ チェックの cookie</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予期されるセキュリティ チェックの cookie</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予期されるセキュリティ チェックのクッキーのビット補数</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ドライバーでは、スタック ベースのバッファー (またはローカル変数) をオーバーランは関数のリターン アドレスが上書きされ、関数が返されるときに、任意のアドレスにジャンプするようにします。

これは、クラシック「バッファー オーバーラン」ハッキング攻撃です。 システムは、悪意のあるユーザーが、完全に制御するを防ぐに停止されています。

<a name="resolution"></a>解決方法
----------

使用して、 [ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)スタック トレースを取得するコマンド。

バッファー オーバーラン ハンドラーとバグの呼び出しを確認してください。 前に、スタックの最後のルーチンは、そのローカル変数をオーバーランです。

 

 




