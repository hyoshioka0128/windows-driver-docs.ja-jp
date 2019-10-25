---
title: フィルター モジュールの状態と操作
description: フィルター モジュールの状態と操作
ms.assetid: b5798865-8332-477b-b155-79a3db6ff6fa
keywords:
- フィルタードライバーの WDK ネットワーク、状態
- NDIS フィルタードライバー WDK、状態
- 状態 WDK NDIS フィルタ
- 切り離された状態 WDK ネットワーク
- 状態 WDK ネットワークの接続
- 一時停止状態 WDK ネットワーク
- 状態 WDK ネットワークを再起動しています
- 実行状態 WDK ne
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c517f8fa7433f18fbcceb4d7dc854f825a8b2885
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838099"
---
# <a name="filter-module-states-and-operations"></a>フィルター モジュールの状態と操作





フィルタードライバーでは、ドライバーによって管理されるフィルターモジュール (フィルタードライバーのインスタンス) ごとに次の動作状態がサポートされている必要があります。

<a href="" id="detached"></a>デタッチ  
*デタッチ*された状態は、フィルターモジュールの初期状態です。 フィルターモジュールがこの状態になると、NDIS はフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出して、フィルターモジュールをドライバースタックにアタッチできます。

<a href="" id="attaching"></a>付ける  
*アタッチ*中の状態では、フィルタードライバーはフィルターモジュールをドライバースタックにアタッチする準備をします。

<a href="" id="paused"></a>中  
*一時停止*状態では、フィルタードライバーは送信操作または受信操作を実行しません。

<a href="" id="restarting"></a>再起動  
*再起動*状態では、フィルタードライバーは、フィルターモジュールの送信操作および受信操作を再開するために必要なすべての操作を完了します。

<a href="" id="running"></a>起動  
*実行*状態では、フィルタードライバーはフィルターモジュールに対して通常の送受信処理を実行します。

<a href="" id="pausing"></a>一時停止  
*一時停止*状態では、フィルタードライバーは、フィルターモジュールの送信操作および受信操作を停止するために必要なすべての操作を完了します。

次の表の見出しは、フィルターモジュールの状態です。 主要なイベントは、最初の列に表示されます。 テーブル内の残りのエントリは、状態内でイベントが発生した後にフィルターモジュールが入力する次の状態を指定します。 空のエントリは、無効なイベントと状態の組み合わせを表します。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント/状態</th>
<th align="left">Detached</th>
<th align="left">アタッチ</th>
<th align="left">一時停止</th>
<th align="left">再起動</th>
<th align="left">Running</th>
<th align="left">一時停止</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>フィルターのアタッチ</p></td>
<td align="left"><p>アタッチ</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>アタッチが完了しました</p></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>フィルターの解除</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Detached</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>フィルターの再起動</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>再起動</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>再起動が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Running</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>一時停止のフィルター</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>一時停止が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="even">
<td align="left"><p>アタッチに失敗しました</p></td>
<td align="left"></td>
<td align="left"><p>Detached</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>再起動に失敗しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>送信と受信</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Running</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OID 要求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"><p>再起動</p></td>
<td align="left"><p>Running</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
</tbody>
</table>

 

プライマリフィルタードライバーイベントは、次のように定義されています。

<a href="" id="--------filter-attach--------"></a>フィルターのアタッチ   
NDIS は、ドライバースタックにフィルターモジュールをアタッチするために、ドライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出しました。 フィルターモジュールのアタッチの詳細については、「[フィルターモジュールのアタッチ](attaching-a-filter-module.md)」を参照してください。

<a href="" id="attach-is-complete"></a>アタッチが完了しました  
フィルターモジュールが*アタッチ*状態のときに、フィルタードライバーがフィルターモジュールが必要とするすべてのリソースの初期化を完了すると、フィルターモジュールは*一時停止*状態になります。

<a href="" id="--------filter-detach--------"></a>フィルターの解除   
NDIS は、ドライバースタックからフィルターモジュールをデタッチするために、ドライバーの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出しました。 詳細については、「[フィルターモジュールのデタッチ](detaching-a-filter-module.md)」を参照してください。

<a href="" id="--------filter-restart--------"></a>フィルターの再起動   
NDIS は、一時停止されたフィルターモジュールを再起動するために、ドライバーの[*Filterrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出しました。 詳細については、「[フィルターモジュールを開始する](starting-a-filter-module.md)」を参照してください。

<a href="" id="restart-is-complete"></a>再起動が完了しました  
フィルターモジュールが*再起動*中の状態で、ドライバーが送信および受信操作を実行する準備ができたら、フィルターモジュールは*実行中*の状態になります。

<a href="" id="--------filter-pause--------"></a>一時停止のフィルター   
NDIS は、フィルターモジュールを一時停止するために、ドライバーの[*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)関数を呼び出しました。 詳細については、「[フィルターモジュールの一時停止](pausing-a-filter-module.md)」を参照してください。

<a href="" id="pause-is-complete"></a>一時停止が完了しました  
送信と受信の操作を停止するために必要なすべての操作がドライバーによって完了すると、一時停止操作が完了し、フィルターモジュールが*一時停止*状態になります。

<a href="" id="attach-failed"></a>アタッチに失敗しました  
NDIS がドライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出し、アタッチ操作が失敗した場合 (たとえば、必要なリソースが使用できないため)、フィルターモジュールは*デタッチ*された状態に戻ります。

<a href="" id="restart-failed"></a>再起動に失敗しました  
NDIS がドライバーの[*Filterrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)関数を呼び出し、再起動の試行が失敗した場合、フィルターモジュールは*一時停止*状態に戻ります。

<a href="" id="send-and-receive-operations"></a>送信および受信操作  
ドライバーは、*実行中*および*一時停止*中の状態で送受信操作を処理できます。 送信操作と受信操作の詳細については、「[フィルターモジュールの送受信操作](filter-module-send-and-receive-operations.md)」を参照してください。

<a href="" id="oid-requests"></a>OID 要求  
ドライバーは、*実行中*、*再起動*中、*一時停止*中、*一時停止*中の各状態の OID 要求を処理できます。 OID 要求の詳細については、「[フィルターモジュール OID 要求](filter-module-oid-requests.md)」を参照してください。

 

 





