---
title: 電源の設定要求の処理
description: 電源の設定要求の処理
ms.assetid: c69d4a9b-009a-4320-8e20-32a9cf9113bf
keywords:
- セット power WDK NDIS 中間の要求します。
- スリープ状態 WDK NDIS 中間
- WDK NDIS 中間の作業の状態
- スタンバイ フラグ WDK NDIS 中間
- WDK ネットワークの状態を電源します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209a5eade46e226cf29319332410ff92fd4b7f9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379827"
---
# <a name="handling-a-set-power-request"></a>電源の設定要求の処理





中間のドライバーでは、作業の状態 (ネットワーク デバイス D0 の電源状態) とスリープの状態 (ネットワーク デバイス D1、d2 に切り替わり、または D3 の電源状態) に電源を設定する要求を処理する必要があります。 中間のドライバーには、電源状態変数とスタンバイ フラグもを維持する必要があります。 これらの問題が説明されているこのトピックでさらにします。

中間ドライバーの電源管理の例については、次を参照してください。、 [NDIS MUX 中間ドライバーとオブジェクトの通知](https://go.microsoft.com/fwlink/p/?LinkId=617916)でドライバーのサンプル、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

### <a name="handling-a-set-power-request-to-a-sleeping-state"></a>スリープ状態にセット Power 要求の処理

中間のドライバーがスリープ状態にセット power 要求を処理する必要があります 2 つのケースがあります。

-   スリープ状態には、中間のドライバーの上端仮想ミニポート NDIS 要求。

-   中間ドライバー プロトコルの下端は、プラグ アンド プレイ (PnP) イベント通知を受け取ったときに、スリープ状態を基になるミニポート ドライバーの移行を処理します。

これらのイベントは、任意の順序で発生することができ、1 つのイベントは必ずしもに付属して、その他。

仮想ミニポート中間ドライバーの上端は、電源をスリープ状態に設定する要求を受信したときに、要求を処理するためのイベントの順序のとおりです。

1.  NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)各プロトコル ドライバーの機能が仮想ミニポートにバインドします。 呼び出し*ProtocolNetPnPEvent*を指定します、 **NetEventSetPower**スリープ状態のイベント。 中間のドライバーにバインドされているプロトコル ドライバーには、ネットワーク データを送信して、仮想ミニポート ドライバーの中間の OID の要求を行うが停止します。 NDIS は、基になるミニポート ドライバーがスリープ状態への移行を行っていることを示すまで、ネットワーク データと要求を送信する中間のドライバーのプロトコルの下端を続行できます。

2.  NDIS が発行した後、上にあるドライバーおよびし仮想ミニポートを一時停止します、 **NetEventSetPower**イベント。 一時停止の原因は、低電力状態に遷移です。 仮想ミニポートを一時停止の詳細については、次を参照してください。[アダプターを一時停止](pausing-an-adapter.md)します。

    **注**  いいえ OID 要求は、例外として、低電力状態になっている仮想ミニポートに送信できる[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)します。

     

3.  NDIS 問題、 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)中間ドライバーの仮想ミニポートに要求します。 中間ドライバーは、NDIS を返すことによって、要求を受け入れる\_状態\_成功します。 中間ドライバーが、OID を伝達する必要がありますされません\_PNP\_設定\_電源要求の基になるミニポート ドライバーにします。 中間ドライバーには、この要求が完了すると、そのしたりしないでください、受信した複数のネットワーク データを示す場合でも、その基になるミニポート ドライバーからネットワーク データと状態インジケーターを受信し、状態を示します。

中間のドライバーのプロトコルの下枠には、スリープ状態を基になるミニポート ドライバーが遷移、遷移を処理するためのイベントのシーケンスがとおりです。

1.  NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)中間ドライバー プロトコルの下端の関数。 呼び出し*ProtocolNetPnPEvent*を指定します、 **NetEventSetPower**スリープ状態のイベント。 ネットワーク データを送信して、基になるミニポート ドライバーに OID 要求を行う、中間のドライバーを停止する必要があります。 未処理の要求または送信の場合は、中間のドライバーが NDIS を返す必要があります\_状態\_への呼び出しから PENDING *ProtocolNetPnPEvent*します。 中間ドライバー呼び出し[ **NdisCompleteNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletenetpnpevent)への呼び出しを完了する*ProtocolNetPnPEvent*します。 ただし、中間のドライバーのプロトコルのエッジは、基になるミニポート ドライバーから受信したパケットと状態インジケーターをアクセスできます。 受信したネットワーク データを無視できます。 中間のドライバーの実装が基になるミニポート ドライバーの状態の監視に依存している場合、状態インジケーター引き続き監視する必要があります。

2.  NDIS は中間のドライバーのプロトコルのエッジを一時停止しを実行した後、underying ミニポート アダプターを置いた、 **NetEventSetPower**イベント。 一時停止の原因は、低電力状態に遷移です。 プロトコル バインドを一時停止の詳細については、次を参照してください。[バインディングを一時停止](pausing-a-binding.md)します。

    **注**  いいえ OID 要求は、例外として、低電力状態になっている、基になるミニポート アダプターに送信できます[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)します。

     

3.  NDIS 問題、 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)基になるミニポート ドライバーに要求します。 ただし、基になるミニポート ドライバーが電源管理をサポートしていない場合に中止されます。 この場合は、NDIS は、基になるミニポート ドライバーを停止し、場合でも要求が基になるミニポート ドライバーと NIC からバインド解除するプロトコルを中間ドライバー 基になるミニポート ドライバーの OID の処理が正常に完了 (または、ミニポート ドライバーが停止した) 後にこれ以上のネットワーク データまたは状態いない示されます。

### <a name="handling-a-set-power-request-to-the-working-state"></a>作業状態セット Power 要求の処理

中間のドライバーが稼働状態にセット power 要求を処理する、2 つのケースがあります。

-   動作状態には、中間のドライバーの上端仮想ミニポート NDIS 要求。

-   中間ドライバー プロトコルの下端は、プラグ アンド プレイ (PnP) イベント通知を受け取ったときに、基になるミニポート ドライバーへの移行作業の状態を処理します。

これらのイベントは、任意の順序で発生することができ、1 つのイベントは必ずしもに付属して他のします。

仮想ミニポート中間ドライバーの上端は、電源を動作状態に設定する要求を受信したときに、要求を処理するためのイベントの順序のとおりです。

1.  NDIS 問題、 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)中間ドライバーの仮想ミニポートにします。 中間ドライバー返します NDIS\_状態\_セット power 要求に成功します。 中間ドライバーが、OID を伝達する必要がありますされません\_PNP\_設定\_電源要求の基になるミニポート ドライバーにします。

2.  NDIS は、仮想ミニポートを再起動し、セット power OID を発行した後、上にあるドライバーを再起動します。 仮想ミニポートを再開する方法の詳細については、次を参照してください。[アダプター開始](starting-an-adapter.md)します。

3.  NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)上位プロトコル ドライバーの関数。 呼び出し*ProtocolNetPnPEvent*を指定します、 **NetEventSetPower**イベントを動作状態 (D0) を設定します。 バインド プロトコル ドライバーには、仮想ミニポートのドライバーの中間にネットワークのデータの送信を開始できます。

中間のドライバーの下端プロトコルでは、基になるミニポート ドライバーを動作状態を遷移、遷移を処理するためのイベントのシーケンスがとおりです。

1.  NDIS 問題、 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)基になるミニポート ドライバーまたは呼び出しをその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)基になるミニポート ドライバーが停止した場合はハンドラー。

2.  NDIS は、OID を発行した後、基になるミニポート ドライバー、プロトコルの端との中間の NDIS と基になるミニポート アダプターを再起動します。 プロトコル バインドを一時停止の詳細については、次を参照してください。[バインディングを再起動する](restarting-a-binding.md)します。

3.  NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)中間ドライバーの機能です。 呼び出し*ProtocolNetPnPEvent*を指定します、 **NetEventSetPower**イベントを動作状態 (D0) を設定します。 ネットワーク データを基になるミニポート ドライバーに送信する中間のドライバーを開始できます。

### <a name="power-states-and-the-standby-flag"></a>電源の状態およびスタンバイのフラグ

中間のドライバーは、仮想ミニポート インスタンスごとに別の電源状態変数を維持し、ドライバーを基になる各ミニポート ドライバーにバインドされている必要があります。 中間ドライバーである各仮想ミニポートの StandingBy フラグの管理もする必要があります。

-   設定**TRUE**仮想ミニポートまたは基になるミニポート ドライバーのいずれかの電源の状態から D0 離したときにします。

-   設定**FALSE**と D0 へ仮想ミニポートまたは基になるミニポート ドライバーのいずれかの電源状態を返します。

**注**  MUX 中間ドライバー、可能性があります、基になるミニポート ドライバーに関連付けられている複数の仮想ミニポートまたは各仮想ミニポートに関連付けられている複数の基になるミニポートします。 ミニポート アダプターの電源の状態が変更されたときに関連付けられているミニポートのすべての動作も影響を受けます。 動作の影響を受ける方法は、実装固有です。 たとえば、負荷分散フェールオーバー (LBFO) ソリューションを実装するドライバー可能性がありますは非アクティブ化仮想ミニポート 1 つの基になるミニポート ドライバーが非アクティブ化。 ただし、基になるすべてのミニポート ドライバーに依存しているドライバーの実装は、基になるミニポート ドライバーが非アクティブ化されたときに、仮想ミニポートの非アクティブ化を必要があります。

 

中間のドライバーは、次のように要求を処理するときに、StandingBy フラグと電源の状態変数を使用してください。

-   ドライバーの[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)仮想ミニポートおよびその基になるミニポート アダプターが両方とも D0 場合を除き、関数が失敗する必要があります。

-   ドライバーの[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数は、OID に常に成功する必要があります\_PNP\_クエリ\_ドライバーが後続の OID を受信するように電源\_PNP\_設定\_POWER 要求。

-   ドライバーの[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request) D0 に仮想ミニポートがない場合、または StandingBy がある場合、関数は失敗する必要があります**TRUE**します。 それ以外の場合、D0 に基になるミニポート ドライバーがない場合は、1 つの要求をキューにする必要があります。 D0 の基になるミニポート ドライバーの状態になったら、キューに置かれた要求を処理する必要があります。

-   基になるミニポート ドライバーと仮想ミニポートの両方が D0 場合にのみ、中間ドライバー仮想ミニポートは状態を報告する必要があります。

 

 





