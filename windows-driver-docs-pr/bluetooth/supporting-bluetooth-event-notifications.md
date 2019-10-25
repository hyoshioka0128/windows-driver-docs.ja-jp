---
title: Bluetooth イベント通知のサポート
description: Bluetooth イベント通知のサポート
ms.assetid: ddb6f1d4-0f6e-4b11-93fc-b0886d262749
keywords:
- Bluetooth WDK、イベント通知
- イベント通知 WDK Bluetooth
- 通知 WDK Bluetooth
- プロファイル ドライバー WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb4cae3bee95ad5523df62294b2de24715875c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837535"
---
# <a name="supporting-bluetooth-event-notifications"></a>Bluetooth イベント通知のサポート


プロファイルドライバーは、リモートデバイスへの接続を開くときに、接続が閉じられたとき、または接続に対して他の変更が発生したときに通知を受け取るように自身を登録する必要があります。 さらに、プロファイルドライバーが着信接続を受け入れるように登録すると、リモートデバイスからの接続が試行されたときに通知を受け取ることができる必要があります。

同期接続指向 (SCO) 接続を使用するプロファイルドライバーは、 [*Sco コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)を実装し、登録します。 クライアントプロファイルドライバーは、リモートデバイスへの接続を要求するときに、適切なコールバック関数を登録します。

SCO プロファイルドライバーが**brb\_sco\_** を発行するときに\_CHANNEL BRB を開くと、その Sco[*コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)へのポインターが brb の対応する\_brb\_sco の**コールバック**メンバーに指定され[ **\_OPEN\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)構造体。 リモートデバイスが SCO 接続要求を受け入れた場合、デバイスが SCO 接続に変更されたときにコールバック関数を通じて、Bluetooth ドライバースタックからプロファイルドライバーに通知を送信できます。

SCO 接続の作成の詳細については、「[リモートデバイスへの Sco クライアント接続の作成](creating-a-sco-client-connection-to-a-remote-device.md)」を参照してください。

論理リンクコントローラーとアダプテーションプロトコル (L2CAP) 接続を使用するプロファイルドライバーは、 [*L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)を実装して登録します。

L2CAP プロファイルドライバーが**brb\_L2CA**を発行するときに\_CHANNEL brb\_開くと、その[*L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)へのポインターが brb の対応する\_brb\_L2CA の**コールバック**メンバーに指定されます。 [ **\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)構造体。 リモートデバイスが L2CAP 接続要求を受け入れると、Bluetooth ドライバースタックは、L2CAP 接続が変更されたときにコールバック関数を介してプロファイルドライバーに通知を送信できます。

L2CAP 接続の作成の詳細については、「[リモートデバイスへの L2CAP クライアント接続の作成](creating-a-l2cap-client-connection-to-a-remote-device.md)」を参照してください。

同様に、プロファイルドライバーが受信 (L2CAP、SCO) 接続要求を受け入れるように自身を登録する場合は、リモートデバイスが接続を試行したときに通知されるコールバック関数を登録する必要があります。

L2CAP を使用するプロファイルドライバーでは、 [ **\_サーバー構造の登録\_、\_BRB\_L2CA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server)の**IndicationCallback**メンバー内の[*L2CAP Callback 関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)を指定します。 その後、Bluetooth ドライバースタックはコールバック関数を呼び出して、リモートデバイスがプロファイルドライバーへの L2CAP 接続を開始しようとしたときに、プロファイルドライバーに通知できます。

SCO を使用するプロファイルドライバーは、sco[*コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)を[ **\_BRB\_SCO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server)の**IndicationCallback**メンバーに指定し\_サーバー構造を登録\_ます。 その後、Bluetooth ドライバースタックはコールバック関数を呼び出して、リモートデバイスがプロファイルドライバーへの SCO 接続を開始しようとしたときに、プロファイルドライバーに通知することができます。

プロファイルドライバーによって適切なコールバック関数が登録されると、Bluetooth ドライバースタックは、開いている接続全体でイベントが発生したかどうかをプロファイルドライバーに通知することもできます。

プロファイルドライバーは、開いているチャネルと、それに接続しようとしているリモートデバイスに関する変更通知を送信するために、同じコールバック関数を登録でき  ことに**注意**してください。

 

L2CAP 接続の場合、 [*L2CAP callback 関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)は次の3つのパラメーターを受け取ります。

-   L2CAP 接続に対して定義されているコンテキスト。 BRB\_L2CA\_登録\_サーバー要求の場合、このコンテキストは \_BRB\_L2CA の**IndicationCallbackContext**メンバーで渡される値です。このコンテキストは、申請. **Brb\_L2CA\_open\_channel**または**BRB\_L2CA\_open\_channel\_応答**要求の場合、このコンテキストはの**コンテキスト**メンバーで渡される値です \_BRB\_L2CA は、要求で渡されたオープン\_チャネル構造\_ます。

-   受信 L2CAP 接続または結合状態の変更の通知イベントの種類を示す[ **\_コード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ne-bthddi-_indication_code)列挙の値。

-   Notification イベントに関連付けられているパラメーターを格納している[ **\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_indication_parameters)構造体を示すポインター。

[*L2CAP callback 関数の*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)*表示パラメーターで*渡される値*は、プロファイル*ドライバーが使用するパラメーターパラメーター**の共用体**のメンバーを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>指示</em>パラメーターの値が...</th>
<th align="left">...<em>Parameters</em>パラメーターの次の共用体メンバーを使用します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IndicationRemoteConnect</strong></p></td>
<td align="left"><p><strong>関連付け</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IndicationRemoteConfigRequest</strong></p></td>
<td align="left"><p><strong>ConfigRequest</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IndicationRemoteConfigResponse</strong></p></td>
<td align="left"><p><strong>ConfigResponse</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IndicationFreeExtraOptions</strong></p></td>
<td align="left"><p><strong>FreeExtraOptions</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IndicationRemoteDisconnect</strong></p></td>
<td align="left"><p><strong>切断</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IndicationRecvPacket</strong></p></td>
<td align="left"><p><strong>RecvPacket</strong></p></td>
</tr>
</tbody>
</table>

 

SCO 接続の場合、 [*sco コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)は次の3つの引数を受け取ります。

-   SCO 接続に対して定義されているコンテキスト。 **Brb\_sco\_\_サーバー**要求を登録する場合、このコンテキストは \_BRB\_SCO\_REGISTER\_サーバー構造に渡さ**れた値**です。要求を使用します。 **Brb\_sco\_開いて\_channel**または**BRB\_sco\_open\_channel\_応答**要求の場合、このコンテキストは \_brb の の送信**コンテキスト**メンバーで渡される値です。\_SCO\_、要求で渡された\_チャネル構造を開きます。

-   [**Sco\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ne-bthddi-_sco_indication_code)れた値は、入力 sco 接続または結合状態の変更の通知の種類を示す\_コードの列挙です。

-   通知イベントに関連付けられているパラメーターを格納している\_パラメーター構造体を[**示す SCO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_sco_indication_parameters)を指すポインター。

[*SCO コールバック関数の*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)*表示パラメーターに*渡された値は、プロファイルドライバーが使用する*parameters*パラメーター**のパラメーターの共用体**のメンバーを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>指示</em>パラメーターの値が...</th>
<th align="left">...<em>Parameters</em>パラメーターの次の共用体メンバーを使用します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ScoIndicationRemoteConnect</strong></p></td>
<td align="left"><p><strong>関連付け</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ScoIndicationRemoteDisconnect</strong></p></td>
<td align="left"><p><strong>切断</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhandling_plug_and_play_removal_irpsspanspan-idhandling_plug_and_play_removal_irpsspanhandling-plug-and-play-removal-irps"></a><span id="handling_plug_and_play_removal_irps"></span><span id="HANDLING_PLUG_AND_PLAY_REMOVAL_IRPS"></span>プラグアンドプレイ削除 Irp の処理

プロファイルドライバーは、Bluetooth ドライバースタックによって処理されるように、直ちにすべての[**IRP\_\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)irp をスタック内に渡す必要があります。 突然削除される IRP の処理の一環として、開いているチャネルを閉じないようにしてください。 予期しない IRP を受け取った後に、基になるラジオにデータを送信する他の BRBs をビルドして送信することは避けてください。 ただし、プロファイルドライバーは、予期しない IRP の処理中に他のクリーンアップを実行できます。

Bluetooth ドライバースタックは、予期せぬ削除の IRP を受信した後、プロファイルドライバーが Brb\_SCO を構築して送信したときに、プロファイルドライバーによって指定された[*Sco コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)に*ScoIndicationRemoteDisconnect*を渡します。 [ **\_オープン\_チャネル**](https://docs.microsoft.com/previous-versions/ff536626(v=vs.85))または[**brb\_SCO\_オープン\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))要求を開いて、現在開いている sco チャネルを閉じます。 同様に、Bluetooth ドライバースタックは*IndicationRemoteDisconnect*を[*L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)に渡し、プロファイルドライバーが[**brb\_\_L2CA を構築して送信したときに、プロファイルドライバーによって指定された Callback 関数\_CHANNEL**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))または[**brb\_L2CA\_\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))要求を開いて、現在開いているすべての L2CAP チャネルを閉じることができます。

プロファイルドライバーは、Irp の処理中にすべてのサーバーの登録を解除し、\_デバイスの irp を[**削除\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)します。 SCO サーバーの登録を解除するには、プロファイルドライバーが[**Brb\_SCO\_** ](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85)) [作成して送信し](building-and-sending-a-brb.md)、\_サーバー要求の登録を解除します。 L2CAP サーバーの登録を解除するには、プロファイルドライバーで[**Brb\_L2CA**](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))を作成して送信し、\_サーバー要求の登録を解除\_ます。

 

 





