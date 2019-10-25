---
title: ミニポート アダプターの状態と操作
description: ミニポート アダプターの状態と操作
ms.assetid: b47e2cbe-9da3-4600-9afe-b082e60b87fb
keywords:
- ミニポートアダプター WDK ネットワーク、状態
- の WDK ネットワーク、状態
- ミニポートアダプター WDK ネットワーク、操作
- WDK ネットワーク、操作のアダプター
- 状態 WDK ネットワークを停止しました
- シャットダウン状態 WDK ネットワーク
- 状態 WDK を初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9c2ca3fdef1546a836265afdc00762c7dbe112f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844245"
---
# <a name="miniport-adapter-states-and-operations"></a>ミニポート アダプターの状態と操作





管理するアダプターごとに、NDIS 6.0 以降のミニポートドライバーが、次の動作状態のセットをサポートしている必要があります。

<a href="" id="halted"></a>停止  
停止状態は、すべてのアダプターの初期状態です。 アダプターが停止状態のとき、NDIS はドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出してアダプターを初期化できます。

<a href="" id="shutdown"></a>シャットダウン  
シャットダウン状態の場合、システムのシャットダウンと再起動は、システムがアダプターを再度使用できるようになる前に実行する必要があります。

<a href="" id="initializing"></a>初期化  
初期状態では、ミニポートドライバーは、アダプターの初期化に必要なすべての操作を完了します。

<a href="" id="paused"></a>中  
一時停止状態のアダプターは、受信したネットワークデータを示していないか、送信要求を受け入れていません。

<a href="" id="restarting"></a>再起動  
再起動状態の場合、ミニポートドライバーは、アダプターの送信および受信操作を再開するために必要なすべての操作を完了します。

<a href="" id="running"></a>起動  
実行状態では、ミニポートドライバーがアダプターの送受信処理を実行します。

<a href="" id="pausing"></a>一時停止  
一時停止中の状態では、アダプターの送信および受信操作を停止するために必要なすべての操作が、ミニポートドライバーによって完了されます。

次の表では、ヘッダーがアダプターの状態になっています。 主要なイベントは、最初の列に表示されます。 テーブル内の残りのエントリは、状態内でイベントが発生した後にアダプターが入力する次の状態を指定します。 空のエントリは、無効なイベントと状態の組み合わせを表します。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント \ 状態</th>
<th align="left">停止</th>
<th align="left">シャットダウン</th>
<th align="left">初期化</th>
<th align="left">一時停止</th>
<th align="left">再起動</th>
<th align="left">Running</th>
<th align="left">一時停止</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a></p></td>
<td align="left"><p>初期化</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>初期化が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)"><em>MiniportShutdownEx</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>シャットダウン</p></td>
<td align="left"><p>シャットダウン</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>ミニ Porthaltex</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart" data-raw-source="[&lt;em&gt;MiniportRestart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)"><em>MiniportRestart</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>再起動</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>再起動が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Running</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)"><em>MiniportPause</em></a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>一時停止が完了しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="odd">
<td align="left"><p>初期化に失敗しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>停止</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>再起動に失敗しました</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>送信および受信操作</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>Running</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
<tr class="even">
<td align="left"><p>OID 要求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>一時停止</p></td>
<td align="left"><p>再起動</p></td>
<td align="left"><p>Running</p></td>
<td align="left"><p>一時停止</p></td>
</tr>
</tbody>
</table>

 

前の表に記載されているイベントは、NDIS 6.0 以降のアダプターのプライマリイベントで  **ことに注意**してください。

 

**注**  リセット操作は、ミニポートアダプターの操作状態に影響しません。 リセット操作の進行中は、アダプターの状態が変わる可能性があります。 たとえば、NDIS は、実行中のリセット操作があるときにドライバーの pause ハンドラーを呼び出す場合があります。 この場合、ドライバーは、各操作の通常の要件に従って、任意の順序でリセット操作または一時停止操作を完了できます。 リセット操作の場合、ドライバーは要求パケットの送信に失敗することがあります。または、キューをキューに入れて後で完了させることができます。 ただし、送信パケットが保留されている間は、後続のドライバーが一時停止操作を完了できないことに注意してください。

 

プライマリミニポートドライバーイベントは、次のように定義されています。

<a href="" id="miniportinitializeex"></a>MiniportInitializeEx  
NDIS は、アダプターを初期化するために、ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出しました。 アダプターの初期化の詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

<a href="" id="initialize-is-complete"></a>初期化が完了しました  
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が正常に返されると、初期化操作が完了し、アダプターが一時停止状態になります。

<a href="" id="miniportshutdownex"></a>MiniportShutdownEx  
NDIS は、アダプターをシャットダウンするために、ドライバーの[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)関数を呼び出しました。 詳細については、「[ミニポートアダプターのシャットダウン](miniport-adapter-shutdown.md)」を参照してください。

<a href="" id="miniporthaltex"></a>ミニ Porthaltex  
NDIS は、アダプターを停止するために、ドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出しました。 詳細については、「[ミニポートアダプターの停止](halting-a-miniport-adapter.md)」を参照してください。

<a href="" id="miniportrestart"></a>MiniportRestart  
NDIS は、一時停止しているアダプターを再起動するために、ドライバーの[**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出しました。 アダプターは初期化後に一時停止状態になるので、アダプターの初期化が完了した後にアダプターを起動するためにもこのイベントが必要になります。 詳細については、「[アダプターの開始](starting-an-adapter.md)」を参照してください。

<a href="" id="restart-is-complete"></a>再起動が完了しました  
ドライバーが送信および受信操作を処理する準備が完了すると、再起動操作が完了し、アダプターが実行中の状態になります。

<a href="" id="miniportpause"></a>MiniportPause  
NDIS は、アダプターを一時停止するために、ドライバーの[*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)関数を呼び出しました。 詳細については、「[アダプターの一時停止](pausing-an-adapter.md)」を参照してください。

<a href="" id="pause-is-complete"></a>一時停止が完了しました  
送信と受信の操作を停止するために必要なすべての操作がドライバーによって完了すると、一時停止操作が完了し、アダプターが一時停止状態になります。

一時停止操作が完了する前に、ドライバーがすべての未処理の受信確認を返すのを待機する必要がある  に**注意**してください。

 

<a href="" id="initialize-failed"></a>初期化に失敗しました  
NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出し、初期化が失敗した場合、アダプターは停止状態に戻ります。

<a href="" id="restart-failed"></a>再起動に失敗しました  
NDIS がドライバーの[**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出し、再起動の試行が失敗した場合、アダプターは一時停止状態のままになります。

<a href="" id="send-and-receive-operations"></a>送信および受信操作  
ドライバーは、実行中および一時停止中の状態で送信および受信操作を処理する必要があります。 送信操作と受信操作の詳細については、「[ミニポートドライバーの送受信操作](miniport-driver-send-and-receive-operations.md)」を参照してください。

<a href="" id="oid-requests"></a>OID 要求  
ドライバーは、実行中、再起動中、一時停止中、一時停止中の各状態の OID 要求を処理する必要があります。 OID 要求の詳細については、「[アダプターに対する Oid 要求](miniport-adapter-oid-requests.md)」を参照してください。

## <a name="related-topics"></a>関連トピック


[ミニポートアダプターの停止](halting-a-miniport-adapter.md)

[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)

[ミニポートアダプターのシャットダウン](miniport-adapter-shutdown.md)

[ミニポートドライバーの送信と受信の操作](miniport-driver-send-and-receive-operations.md)

[アダプターの一時停止](pausing-an-adapter.md)

[アダプターを開始する](starting-an-adapter.md)

 

 






