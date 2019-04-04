---
title: Winsock カーネル イベント
description: Winsock カーネル イベント
ms.assetid: 84f7b547-cfbf-468b-b80e-1441c8aa3cf3
keywords:
- Winsock カーネル WDK が、ネットワーク イベント
- ネットワーク、WSK WDK イベント
- WDK Winsock カーネル イベント
- 基本的なソケット WDK Winsock カーネル
- リッスンしているソケット WDK Winsock カーネル
- データグラム ソケット WDK Winsock カーネル
- 接続指向のソケット WDK Winsock カーネル
- イベント通知 WDK Winsock カーネル
- WDK Winsock Kernel の通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 690ddad7de51960e6de7799b93d32c090c79ed04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551530"
---
# <a name="winsock-kernel-events"></a>Winsock カーネル イベント


ソケットの特定のイベントが発生した場合に、ソケットで新しいデータを受信したときや、ソケットが切断された場合など、Winsock カーネル (WSK) サブシステムは WSK アプリケーションを非同期的に通知できます。 ソケット イベントの非同期的に通知を受ける WSK アプリケーションのために、WSK アプリケーションが適切なイベントのコールバック関数を実装し、そのイベントのコールバック関数で作成されたソケットを有効にする必要があります。

**注**  A WSK アプリケーションを実装したり、イベントのコールバック関数を使用する必要はありません。 WSK アプリケーションでは、適切な WSK ソケット関数を呼び出すことによって、ほとんどの WSK ソケット操作を実行できます。 イベントのコールバック関数を使用する必要があります。 唯一の WSK 機能は、リッスン ソケットのモードを条件付きに承認します。 詳細については、長所と短所 WSK 関数イベントのコールバック関数を使用するとの間では、[Winsock カーネル関数を使用するとを参照してください。イベントのコールバック関数](using-winsock-kernel-functions-vs--event-callback-functions.md)します。

 

各 WSK[ソケット カテゴリ](winsock-kernel-socket-categories.md)ソケット イベントのさまざまなセットをサポートしています。

**基本的なソケット**

基本的なソケットは、ソケット、イベントをサポートしていません。

**ソケットをリッスンしています。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント</th>
<th align="left">イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>着信接続が受け付けられました。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571120" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571120)"><em>WskAcceptEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>受信接続要求が到着しました。<em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571137" data-raw-source="[&lt;em&gt;WskInspectEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571137)"><em>WskInspectEvent</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>受信接続要求が削除されました。</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571108" data-raw-source="[&lt;em&gt;WskAbortEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571108)"><em>WskAbortEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

\* のみ適用されますがリッスンしているソケットの条件付き許可モードを有効にします。 条件付きの使用に関する詳細情報の受け入れソケットをリッスンしているモードを参照してください[リッスン中の接続と着信接続を受け入れる](listening-for-and-accepting-incoming-connections.md)します。

**データグラム ソケット**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント</th>
<th align="left">イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 つまたは複数の新しいデータグラムを受信するとします。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571142" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571142)"><em>WskReceiveFromEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

**接続指向のソケット**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント</th>
<th align="left">イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>新しいデータを受信しました。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571140" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571140)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ソケットが切断されました。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571130" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571130)"><em>WskDisconnectEvent</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>最適な送信バックログのサイズが変更されました。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571147" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571147)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

WSK アプリケーションでは、ソケットを作成するときは、ソケットのイベントのコールバック関数が既定で無効にします。 WSK アプリケーションには、ソケットのイベントが発生したときに、ソケットのイベントのコールバック関数を呼び出す WSK サブシステムの順序でソケットのイベントのコールバック関数が有効にする必要があります。 有効にして、ソケットのイベントのコールバック関数を無効化の詳細については、[の有効化と無効にするとイベントのコールバック関数](enabling-and-disabling-event-callback-functions.md)を参照してください。

WSK アプリケーションを登録する場合、[拡張機能インターフェイス](winsock-kernel-extension-interfaces.md)ソケットに関して、拡張機能インターフェイスが追加のイベントをサポート可能性があります。 ソケットの拡張インターフェイスを登録の詳細については、[拡張機能インターフェイスを登録する](registering-an-extension-interface.md)を参照してください。

WSK サブシステムは、特定のソケットに固有ではないイベントの WSK アプリケーションを通知することもできます。 これらのイベントの通知を受け取る WSK アプリケーションで、WSK アプリケーションを実装する必要があります、 [ *WskClientEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571123)イベント コールバック関数。 現在ないイベント定義を特定のソケットに固有ではありません。 WSK アプリケーションの*WskClientEvent*イベント コールバック関数は常に有効し、無効にすることはできません。

WSK アプリケーションのイベントのコールバック関数は、WSK 完了またはイベントのコールバック関数のコンテキストでは、他の WSK 要求の完了を待つ必要がありますされません。 コールバックは、その他の WSK 要求を開始できる (ディスパッチで時間をかけることがあることを前提\_レベル)、IRQL でコールバックが呼び出されたときが完了する必要があります待機できませんが、パッシブ =\_レベル。

 

 





