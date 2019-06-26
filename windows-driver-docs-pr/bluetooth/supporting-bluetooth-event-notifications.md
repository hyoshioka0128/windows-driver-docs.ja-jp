---
title: Bluetooth イベント通知のサポート
description: Bluetooth イベント通知のサポート
ms.assetid: ddb6f1d4-0f6e-4b11-93fc-b0886d262749
keywords:
- Bluetooth の WDK、イベント通知
- イベント通知 WDK Bluetooth
- WDK の Bluetooth の通知
- プロファイル ドライバー WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94215bc44f3fbc382a85c6f221a871b6d38f369e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364611"
---
# <a name="supporting-bluetooth-event-notifications"></a>Bluetooth イベント通知のサポート


プロファイル ドライバーでは、リモート デバイスへの接続が開いたら、接続が閉じられたときに、またはその他の接続に変更が発生したときに通知を受け取る自体に登録する必要があります。 さらをプロファイル ドライバーが着信接続を受け入れる自体を登録する場合にリモート デバイスが接続しようとしたときに通知を受け取ることがあります。

Synchronous Connection-Oriented (SCO) 接続を使用するプロファイルのドライバーを実装および登録を[ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)します。 クライアント プロファイルのドライバーは、リモート デバイスへの接続を要求するときに、適切なコールバック関数を登録します。

SCO プロファイルのドライバーを発行したとき、 **BRB\_SCO\_オープン\_チャネル**BRB へのポインターを指定、 [ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)で、**コールバック**、BRB のメンバーの対応する[  **\_BRB\_SCO\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel)構造体。 リモート デバイスが SCO 接続要求を受け入れる場合、Bluetooth ドライバー スタックし、通知を送信できますコールバック関数を使ってプロファイル ドライバー SCO 接続に変更されたとき。

SCO 接続の作成の詳細については、次を参照してください。 [SCO リモート デバイスにクライアント接続を作成する](creating-a-sco-client-connection-to-a-remote-device.md)します。

論理リンク コント ローラーと適応プロトコル (L2CAP) 接続を使用するプロファイルのドライバーを実装および登録、 [ *L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbthport_indication_callback)します。

L2CAP プロファイルのドライバーを発行したとき、 **BRB\_L2CA\_オープン\_チャネル**BRB へのポインターを指定、 [ *L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbthport_indication_callback)で、**コールバック**、BRB のメンバーの対応する[  **\_BRB\_L2CA\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel)構造体。 リモート デバイスが L2CAP 接続要求を受け入れる場合、Bluetooth ドライバー スタックし、通知を送信できますコールバック関数を使ってプロファイル ドライバー L2CAP 接続に変更されたとき。

L2CAP 接続の作成の詳細については、次を参照してください。 [L2CAP リモート デバイスにクライアント接続を作成する](creating-a-l2cap-client-connection-to-a-remote-device.md)します。

同様に、ときにプロファイル ドライバー自身を登録 (L2CAP、SCO) の着信接続を受け入れることを要求するリモート デバイスが接続しようとしたときに通知を受け取るコールバック関数を登録する必要があります。

L2CAP を使用するプロファイルのドライバーを指定、 [ *L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbthport_indication_callback)で、 **IndicationCallback**のメンバー、 [  **\_BRB\_L2CA\_登録\_SERVER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_register_server)構造体。 Bluetooth ドライバー スタックは、リモート デバイスが、プロファイルのドライバーに L2CAP 接続を開始しようとすると、プロファイルのドライバーに通知するコールバック関数を呼び出してことができます。

SCO を使用するプロファイルのドライバーを指定、 [ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)で、 **IndicationCallback**のメンバー、 [  **\_BRB\_SCO\_登録\_SERVER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_register_server)構造体。 Bluetooth ドライバー スタックは、リモート デバイスが、プロファイルのドライバーに SCO 接続を開始しようとすると、プロファイルのドライバーに通知するコールバック関数を呼び出してことができます。

プロファイル ドライバーが適切なコールバック関数を登録した後は、開いている接続経由でイベントが発生した場合、Bluetooth ドライバー スタックもプロファイル ドライバーを通知できます。

**注**  プロファイル ドライバーは、変更を送信して同じコールバック関数を登録できますチャネルを開くとそれに接続しようとしています。 リモート デバイスについて通知します。

 

L2CAP 接続の場合、 [ *L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbthport_indication_callback)は 3 つのパラメーターを受け取ります。

-   L2CAP 接続に対して定義されているコンテキスト。 BRB 場合\_L2CA\_登録\_サーバー要求、このコンテキストに渡された値とは、 **IndicationCallbackContext**のメンバー、 \_BRB\_L2CA\_登録\_サーバー構造が要求に渡されます。 場合に**BRB\_L2CA\_オープン\_チャネル**または**BRB\_L2CA\_オープン\_チャネル\_応答**要求すると、このコンテキストに渡された値とは、 **CallbackContext**のメンバー、 \_BRB\_L2CA\_オープン\_要求で渡されるチャネルの構造体。

-   値、 [ **INDICATION\_コード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ne-bthddi-_indication_code)受信 L2CAP 接続または結合状態変更の通知イベントの種類を示す列挙体。

-   ポインター、 [ **INDICATION\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_indication_parameters) notification イベントに関連付けられているパラメーターを含む構造体。

渡された値、 [ *L2CAP コールバック関数の*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbthport_indication_callback)*Indication*パラメーターがでどの共用体のメンバーを指定します、**パラメーター**共用体の*パラメーター*プロファイル ドライバーが使用するパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">場合の値、 <em>Indication</em>パラメーターと等しい.</th>
<th align="left">...次の共用体メンバーを使用して、<em>パラメーター</em>パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IndicationRemoteConnect</strong></p></td>
<td align="left"><p><strong>Connect</strong></p></td>
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

 

SCO 接続の場合、 [ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)は 3 つの引数を受け取ります。

-   SCO 接続に対して定義されているコンテキスト。 場合に**BRB\_SCO\_登録\_SERVER**要求すると、このコンテキストに渡された値とは、 **IndicationCallbackContext** のメンバー\_BRB\_SCO\_登録\_サーバー構造が要求に渡されます。 場合に**BRB\_SCO\_オープン\_チャネル**または**BRB\_SCO\_オープン\_チャネル\_応答**要求すると、このコンテキストに渡された値とは、 **CallbackContext**のメンバー、 \_BRB\_SCO\_オープン\_要求で渡されるチャネルの構造体。

-   値、 [ **SCO\_INDICATION\_コード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ne-bthddi-_sco_indication_code)受信 SCO 接続または結合状態変更の通知の種類を示す列挙体。

-   ポインターを[ **SCO\_INDICATION\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_sco_indication_parameters) notification イベントに関連付けられているパラメーターを含む構造体。

渡された値、 [ *SCO コールバック関数の*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)*Indication*パラメーターがでどの共用体のメンバーを指定します、**パラメーター**共用体*パラメーター*プロファイル ドライバーが使用するパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">場合の値、 <em>Indication</em>パラメーターと等しい.</th>
<th align="left">...次の共用体メンバーを使用して、<em>パラメーター</em>パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ScoIndicationRemoteConnect</strong></p></td>
<td align="left"><p><strong>Connect</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ScoIndicationRemoteDisconnect</strong></p></td>
<td align="left"><p><strong>切断</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhandlingplugandplayremovalirpsspanspan-idhandlingplugandplayremovalirpsspanhandling-plug-and-play-removal-irps"></a><span id="handling_plug_and_play_removal_irps"></span><span id="HANDLING_PLUG_AND_PLAY_REMOVAL_IRPS"></span>プラグ アンド プレイ削除 Irp の処理

プロファイルのドライバーがすべてを渡す必要があります[ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal) Bluetooth ドライバー スタックで処理するには、すぐに下位のスタックの Irp します。 突然の取り外し IRP の処理の一環として任意の開いているチャネルを閉じるしようとしないでください。 ビルドしないようにし、さらに BRBs 突然削除 IRP を受信した後、データを基になるラジオを送信する送信。 ただし、プロファイル ドライバーでは、突然の取り外し IRP の処理中に他のクリーンアップを実行することができます。

Bluetooth ドライバー スタックが突然削除 IRP を受信した後に合格*ScoIndicationRemoteDisconnect*を[ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)指定されています。プロファイルのドライバーが構築され、送信されたときに、プロファイル ドライバーによって、 [ **BRB\_SCO\_オープン\_チャネル**](https://docs.microsoft.com/previous-versions/ff536626(v=vs.85))または[ **BRB\_SCO\_開く\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))要求、現在開いている任意の SCO チャネルを閉じます。 同様に、Bluetooth ドライバー スタックが合格*IndicationRemoteDisconnect*を[ *L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbthport_indication_callback)プロファイル ドライバーによって指定されているときに、プロファイルのドライバーに構築され、送信、 [ **BRB\_L2CA\_オープン\_チャネル**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))または[ **BRB\_L2CA\_開く\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))要求、現在開いている任意の L2CAP チャネルを閉じます。

プロファイルのドライバーを処理するときに、すべてのサーバーを登録解除[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) Irp します。 SCO サーバーの登録を解除するプロファイルのドライバーがする必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_SCO\_登録解除\_SERVER** ](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))要求。 L2CAP、サーバーの登録を解除するプロファイルのドライバーをビルドを送信してください、 [ **BRB\_L2CA\_登録解除\_SERVER** ](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))要求。

 

 





