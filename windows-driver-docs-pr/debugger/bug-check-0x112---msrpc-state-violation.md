---
title: バグ チェック 0x112 MSRPC_STATE_VIOLATION
description: MSRPC_STATE_VIOLATION のバグ チェックでは、0x00000112 の値を持ちます。 これは、Msrpc.sys ドライバーのバグ チェックが開始されたことを示します。
ms.assetid: b7cd531d-518e-4d11-8edb-d52dbbe51043
keywords:
- バグ チェック 0x112 MSRPC_STATE_VIOLATION
- MSRPC_STATE_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MSRPC_STATE_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9419d102cfafa89ffd3546b35e55d47c2d9829dc
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903368"
---
# <a name="bug-check-0x112-msrpcstateviolation"></a>バグ チェック 0x112:MSRPC\_状態\_違反


MSRPC\_状態\_違反のバグ チェックが 0x00000112 の値を持ちます。 これは、Msrpc.sys ドライバーのバグ チェックが開始されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="msrpcstateviolation-parameters"></a>MSRPC\_状態\_違反パラメーター


パラメーター 1 と 2 は、関心のある唯一のパラメーターです。 パラメーター 1 が状態の違反種類; ことを示しますパラメーター 2 の値は、パラメーター 1 の値によって決まります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>例外コード</p></td>
<td align="left"><p>不可能な例外は、呼び出し元が続行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>高度なローカル プロシージャ呼び出し (ALPC) には、無効なエラーが返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>サーバーへのセッション</p></td>
<td align="left"><p>呼び出し元は、使用中であった Microsoft リモート プロシージャ呼び出し (MSRPC) ドライバーをアンロードします。 開いているバインド ハンドルが残っている可能性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04 と</p>
<p>0x05</p></td>
<td align="left"><p>サーバーへのセッション</p></td>
<td align="left"><p>無効な閉じるコマンドは、ALPC から受信しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>バインド ハンドル</p></td>
<td align="left"><p>リモート プロシージャ コール (RPC) のハンドルを 2 回目のバインドが試行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>バインド ハンドル</p></td>
<td align="left"><p>バインドされていないバインド ハンドルに操作を実行する試行されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>バインド ハンドル</p></td>
<td align="left"><p>既にバインドされていたバインド ハンドルにセキュリティ情報の設定が試行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>バインド ハンドル</p></td>
<td align="left"><p>既にバインドされているバインド ハンドルのオプションを設定しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>呼び出しオブジェクト</p></td>
<td align="left"><p>無効な非同期リモート プロシージャ コールの取り消しが試行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>呼び出しオブジェクト</p></td>
<td align="left"><p>これが予期されていない場合、パイプの非同期呼び出しのプッシュが試行されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C と</p>
<p>0x0E</p></td>
<td align="left"><p>パイプ オブジェクト</p></td>
<td align="left"><p>通知を待つことがなく、非同期のパイプでプッシュが試行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>パイプ オブジェクト</p></td>
<td align="left"><p>パイプを 2 回目を同期的に終了が試行されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>エラーに最も近いオブジェクト</p></td>
<td align="left"><p>RPC の内部エラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>2 つの順序付けられた causally 呼び出し発行されている順番で、RPC によって強制できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>呼び出しオブジェクト</p></td>
<td align="left"><p>サーバー マネージャーのルーチンは、呼び出しを完了する前に通知のサブスクライブ解除しないでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>非同期のハンドル</p></td>
<td align="left"><p>非同期のハンドルに無効な操作が発生しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックの最も一般的な原因は、Msrpc.sys ドライバーの呼び出し元がこのような呼び出しの状態のセマンティクスに違反したことです。

 

 




