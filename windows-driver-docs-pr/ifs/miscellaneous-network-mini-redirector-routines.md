---
title: その他のネットワーク ミニリダイレクター ルーチン
description: その他のネットワーク ミニリダイレクター ルーチン
ms.assetid: bad5847c-8ac5-4e63-a0a5-3bbf13424928
keywords:
- ミニ リダイレクター WDK、その他のルーチン
- 接続 Id の WDK ネットワーク リダイレクター
- バッファリング状態の WDK ネットワーク リダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aec5de46bc7d8e045b5abbbd3009049ff0125639
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375956"
---
# <a name="miscellaneous-network-mini-redirector-routines"></a>その他のネットワーク ミニリダイレクター ルーチン


いくつかその他のルーチンで状態管理と接続 Id をバッファリング ネットワーク ミニリダイレクター案件によって実装されます。 リダイレクターとサーバーで実装される、さまざまなバッファリング スキームを処理するために、バッファリング状態の変更を通信するために、ネットワークのミニ リダイレクターによってバッファリング状態管理ルーチンを使用できます。 たとえば、 [ **MRxCompleteBufferingStateChangeRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_change_buffering_state_calldown) oplock をサーバーに送信するメカニズムの一部として、ルーチンが SMB リダイレクターによって使用されます。

接続 Id は、複数の接続を多重化を使用できます。 接続 Id をサポートするために、ネットワーク ミニ リダイレクター必要ない[ **MRxGetConnectionId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_get_connection_id)は省略可能です。

次の表では、その他の操作、ネットワーク ミニ リダイレクターで実装できるルーチンを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_change_buffering_state_calldown" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_change_buffering_state_calldown)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター バッファリング状態の変更要求が完了したことを通知するには、このルーチンを呼び出します。 たとえば、SMB リダイレクターは、oplock 解除の応答を送信するか、ファイルが不要になった使用されている場合は、oplock のハンドルを閉じること、このルーチンを使用します。 サーバーにフラッシュする必要があるバイト範囲ロックは、ネットワークのミニ リダイレクターでに渡される、 <strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT のメンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_compute_new_buffering_state" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_compute_new_buffering_state)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクターが新しいバッファリング状態の変更を計算することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_get_connection_id" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_get_connection_id)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが複数のセッションを処理するために使用できる接続の接続 ID を返すことを要求するには、このルーチンを呼び出します。 接続 Id は、ネットワークのミニ リダイレクターでサポートされる場合、返される接続 ID は、名前のテーブルに格納されている接続の構造に追加されます。 接続 ID のバイト単位の比較は、指定した名前のネットワーク名のテーブルを検索する際にで blob し、RDBSS が不透明な blob として接続 ID と見なします。</p></td>
</tr>
</tbody>
</table>

 

 

 




