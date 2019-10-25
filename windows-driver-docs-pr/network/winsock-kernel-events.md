---
title: Winsock カーネル イベント
description: Winsock カーネル イベント
ms.assetid: 84f7b547-cfbf-468b-b80e-1441c8aa3cf3
keywords:
- Winsock カーネル WDK ネットワーク、イベント
- WSK WDK ネットワーク、イベント
- イベント WDK Winsock カーネル
- basic sockets WDK Winsock カーネル
- リスニングソケット WDK Winsock カーネル
- データグラムソケット WDK Winsock カーネル
- 接続指向ソケット WDK Winsock カーネル
- イベント通知 WDK Winsock カーネル
- 通知 WDK Winsock カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8ed0b7cd741f78b5cccda90f490d0ef16c9b222
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844376"
---
# <a name="winsock-kernel-events"></a>Winsock カーネル イベント


Winsock カーネル (WSK) サブシステムでは、特定のソケットイベントが発生したとき、たとえばソケットで新しいデータを受信したとき、またはソケットが切断されたときなど、WSK アプリケーションに非同期的に通知できます。 WSK アプリケーションでソケットイベントが非同期に通知されるようにするには、WSK アプリケーションで適切なイベントコールバック関数を実装し、それが作成するソケットでそれらのイベントコールバック関数を有効にする必要があります。

WSK アプリケーションでは、イベントのコールバック関数を実装または使用する必要がない  に**注意**してください。 WSK アプリケーションは、適切な WSK ソケット関数を呼び出すことによって、ほとんどの WSK ソケット操作を実行できます。 イベントコールバック関数を使用する必要がある WSK 機能は、リスニングソケットでの条件付き受け入れモードのみです。 WSK 関数を使用する場合とイベントコールバック関数を使用する場合の長所と短所の詳細については、「 [Winsock カーネル関数の使用」および「イベントコールバック関数](using-winsock-kernel-functions-vs--event-callback-functions.md)」を参照してください。

 

各 WSK[ソケットカテゴリ](winsock-kernel-socket-categories.md)は、異なるソケットイベントのセットをサポートしています。

**基本ソケット**

基本ソケットでは、ソケットイベントはサポートされません。

**リスニングソケット**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント</th>
<th align="left">イベントコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>受信接続が受け入れられました。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)"><em>WskAcceptEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>受信接続要求が到着しました。<em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event" data-raw-source="[&lt;em&gt;WskInspectEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event)"><em>WskInspectEvent</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>受信接続要求が削除されました。</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event" data-raw-source="[&lt;em&gt;WskAbortEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event)"><em>WskAbortEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

\* は、条件付き受け入れモードが有効になっているリスニングソケットにのみ適用されます。 リッスンソケットでの条件付き受け入れモードの使用の詳細については、「[受信接続のリッスンと受け入れ](listening-for-and-accepting-incoming-connections.md)」を参照してください。

**データグラムソケット**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント</th>
<th align="left">イベントコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1つ以上の新しいデータグラムを受信しました。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)"><em>WskReceiveFromEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

**接続指向ソケット**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント</th>
<th align="left">イベントコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>新しいデータを受信しました。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ソケットが切断されました。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event)"><em>Wsk切断イベント</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>最適な送信バックログのサイズが変更されました。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

WSK アプリケーションでソケットが作成されると、ソケットのイベントコールバック関数は既定で無効になります。 WSK アプリケーションは、ソケットイベントが発生したときに WSK サブシステムがソケットのイベントコールバック関数を呼び出すために、ソケットのイベントコールバック関数を有効にする必要があります。 ソケットのイベントコールバック関数の有効化と無効化の詳細については、「[イベントコールバック関数の有効化と無効化](enabling-and-disabling-event-callback-functions.md)」を参照してください。

WSK アプリケーションがソケットの[拡張インターフェイス](winsock-kernel-extension-interfaces.md)を登録する場合、拡張インターフェイスは追加のイベントをサポートすることがあります。 ソケットの拡張インターフェイスの登録の詳細については、「[拡張インターフェイスの登録](registering-an-extension-interface.md)」を参照してください。

WSK サブシステムは、特定のソケットに固有ではないイベントを WSK アプリケーションに通知することもできます。 WSK アプリケーションにこれらのイベントが通知されるようにするには、WSK アプリケーションで[*Wskclientevent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_client_event)イベントコールバック関数を実装する必要があります。 現在、特定のソケットに固有ではないイベントは定義されていません。 WSK アプリケーションの*Wskclientevent*イベントコールバック関数は常に有効になっており、無効にすることはできません。

Wsk アプリケーションのイベントコールバック関数は、WSK の完了またはイベントコールバック関数のコンテキストで他の WSK 要求の完了を待機することはできません。 このコールバックでは、他の WSK 要求を開始できます (ディスパッチ\_レベルでの時間が長すぎることを前提としています) が、IRQL = パッシブ\_レベルでコールバックが呼び出された場合でも、完了を待機することはできません。

 

 





