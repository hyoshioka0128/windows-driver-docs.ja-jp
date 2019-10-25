---
title: その他のネットワーク ミニリダイレクター ルーチン
description: その他のネットワーク ミニリダイレクター ルーチン
ms.assetid: bad5847c-8ac5-4e63-a0a5-3bbf13424928
keywords:
- ミニリダイレクター WDK、その他のルーチン
- 接続 Id WDK ネットワークリダイレクター
- 状態が "WDK ネットワーク" のリダイレクターをバッファリングする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0609a811748d009f3420e84a359dc8faf3295b18
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841126"
---
# <a name="miscellaneous-network-mini-redirector-routines"></a>その他のネットワーク ミニリダイレクター ルーチン


ネットワークミニリダイレクターによって実装される他のいくつかのルーチンでは、状態管理と接続 Id のバッファリングが処理されます。 ネットワークミニリダイレクターは、バッファリング状態管理ルーチンを使用して、リダイレクターおよびサーバーに実装されているさまざまなバッファリング方式を処理し、バッファリング状態の変化を通知します。 たとえば、 [**MRxCompleteBufferingStateChangeRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown)ルーチンは、サーバーに oplock 解除を送信するメカニズムの一部として SMB リダイレクターによって使用されます。

接続 Id は、複数の接続を多重化するために使用できます。 ネットワークミニリダイレクターは接続 Id をサポートする必要がないため、 [**MRxGetConnectionId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id)は省略可能です。

次の表に、その他の操作用にネットワークミニリダイレクターで実装できるルーチンを示します。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_change_buffering_state_calldown)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、バッファリング状態の変更要求が完了したことをネットワークミニリダイレクターに通知します。 たとえば、SMB リダイレクターは、このルーチンを使用して oplock 解除応答を送信するか、またはファイルが使用されなくなった場合に oplock 中断のハンドルを閉じます。 サーバーに対してフラッシュする必要があるバイト範囲ロックは、RX_CONTEXT のネットワークミニリダイレクターに渡されます。これは、そのロックの<strong>一覧</strong>のメンバーです。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_compute_new_buffering_state" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_compute_new_buffering_state)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS はこのルーチンを呼び出して、ネットワークミニリダイレクターが新しいバッファリング状態の変化を計算するように要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_get_connection_id)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターが、複数のセッションを処理するために使用できる接続の接続 ID を返すように要求します。 ネットワークミニリダイレクターで接続 Id がサポートされている場合、返された接続 ID は、name テーブルに格納されている接続構造に追加されます。 RDBSS は、接続 ID を非透過的な blob と見なし、指定された名前の net name テーブルを参照している間に、接続 ID blob をバイト単位で比較します。</p></td>
</tr>
</tbody>
</table>

 

 

 




