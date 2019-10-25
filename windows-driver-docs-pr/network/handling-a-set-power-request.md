---
title: 電源の設定要求の処理
description: 電源の設定要求の処理
ms.assetid: c69d4a9b-009a-4320-8e20-32a9cf9113bf
keywords:
- セット-パワー要求 WDK NDIS 中間
- 休止状態 WDK NDIS 中間
- 作業状態 WDK NDIS 中間
- スタンバイフラグ WDK NDIS 中間
- 電源状態 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7feebd393ea710c9e7a2f45f185ccb1eaa40ee79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842115"
---
# <a name="handling-a-set-power-request"></a>電源の設定要求の処理





中間ドライバーでは、電源を動作状態 (ネットワークデバイスの電源状態が D0) に設定する要求を処理し、スリープ状態 (D1、D2、または D3 のネットワークデバイスの電源状態) に設定する必要があります。 中間ドライバーは、電源状態変数とスタンバイフラグも保持する必要があります。 これらの問題については、このトピックで詳しく説明します。

中間ドライバーの電源管理の例については、GitHub の[Windows ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリにある[NDIS MUX 中間ドライバーと通知オブジェクト](https://go.microsoft.com/fwlink/p/?LinkId=617916)ドライバーのサンプルを参照してください。

### <a name="handling-a-set-power-request-to-a-sleeping-state"></a>電源要求をスリープ状態に設定する

中間ドライバーがスリープ状態に設定された電源要求を処理する必要がある場合は、次の2つがあります。

-   NDIS は、中間ドライバーの仮想ミニポートの上端がスリープ状態になることを要求します。

-   中間ドライバープロトコルの下端は、プラグアンドプレイ (PnP) イベント通知を受信したときに、基になるミニポートドライバーがスリープ状態に移行する処理を行います。

これらのイベントは任意の順序で発生する可能性があり、1つのイベントは必ずしも他のイベントに付随するとは限りません。

中間ドライバーの仮想ミニポートの上端が、電源をスリープ状態に設定する要求を受信すると、要求を処理するためのイベントのシーケンスは次のようになります。

1.  NDIS は、仮想ミニポートにバインドされている各プロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 *ProtocolNetPnPEvent*を呼び出すと、スリープ状態の**NetEventSetPower**イベントが指定されます。 中間ドライバーにバインドされているプロトコルドライバーは、ネットワークデータの送信を停止し、中間ドライバー仮想ミニポートに対する OID 要求を行います。 中間ドライバーの下位のプロトコルはネットワークデータの送信を継続でき、NDIS は基になるミニポートドライバーがスリープ状態に移行していることを示します。

2.  NDIS は、 **NetEventSetPower**イベントを発行した後、それ以降のドライバーを一時停止し、仮想ミニポートを停止します。 一時停止を指定する理由は、低電力状態への移行です。 仮想ミニポートの一時停止の詳細については、「[アダプターの一時停止](pausing-an-adapter.md)」を参照してください。

    **ただし**  は、OID [\_PNP\_\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)されている場合を除き、バーチャルミニポートが低電力状態のときには、このような oid 要求を送信することはできません。

     

3.  NDIS は、中間ドライバーの仮想ミニポートに対して電源要求\_設定されている[OID\_PNP\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)発行します。 中間ドライバーは、NDIS\_STATUS\_SUCCESS を返すことによって要求を受け入れます。 中間ドライバーでは、\_電源要求の OID\_\_PNP を基になるミニポートドライバーに伝達することはできません。 中間ドライバーは、この要求を完了した後、ネットワークデータを受信したかどうかを示していないか、または基になるミニポートドライバーからのネットワークデータと状態の表示を保持している場合でも、状態を示していません。

中間のドライバーの下端が、基になるミニポートドライバーをスリープ状態に移行すると、遷移を処理するためのイベントのシーケンスは次のようになります。

1.  NDIS は、中間ドライバープロトコルの下端の[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 *ProtocolNetPnPEvent*を呼び出すと、スリープ状態の**NetEventSetPower**イベントが指定されます。 中間ドライバーは、ネットワークデータの送信を停止し、基になるミニポートドライバーに OID 要求を行う必要があります。 未処理の要求または送信がある場合、中間ドライバーは*ProtocolNetPnPEvent*への呼び出しから保留中の NDIS\_状態\_を返します。 中間ドライバーは、 [**NdisCompleteNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletenetpnpevent)を呼び出して*ProtocolNetPnPEvent*への呼び出しを完了します。 中間ドライバーのプロトコルエッジでも、基になるミニポートドライバーから受信パケットと状態の表示を取得できます。 受信したネットワークデータは無視してかまいません。 中間のドライバーの実装が、基になるミニポートドライバーの状態の監視に依存している場合は、状態のインジケーターを引き続き監視する必要があります。

2.  NDIS は中間ドライバーのプロトコルエッジを一時停止し、 **NetEventSetPower**イベントを発行した後に、過少なミニポートアダプターを一時停止します。 一時停止を指定する理由は、低電力状態への移行です。 プロトコルバインドの一時停止の詳細については、「[バインディングの一時停止](pausing-a-binding.md)」を参照してください。

    **ただし**、基になるミニポートアダプターが低電力状態のときに、oid 要求を送信することはできません。  ただし、 [oid\_PNP\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)されている場合は\_電源が設定されます。

     

3.  NDIS は、基になるミニポートドライバーに対して[電源要求\_設定する OID\_PNP\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)発行します。 ただし、基になるミニポートドライバーが電源管理をサポートしていない場合は、停止されます。 この場合、NDIS が基になるミニポートドライバーを停止しても、基になるミニポートドライバーおよび NIC から中間ドライバープロトコルのバインドを解除するように要求されることはありません。 基になるミニポートドライバーが OID の処理を正常に完了した後 (またはミニポートドライバーが停止した場合)、それ以上のネットワークデータや状態は示されません。

### <a name="handling-a-set-power-request-to-the-working-state"></a>電源要求を動作状態に設定する

次の2つのケースでは、中間ドライバーが動作状態へのセットの電源要求を処理します。

-   NDIS は、中間ドライバーの仮想ミニポートの上端が動作状態になることを要求します。

-   中間ドライバープロトコルの下端は、プラグアンドプレイ (PnP) イベント通知を受信したときに、基になるミニポートドライバーの動作状態への遷移を処理します。

これらのイベントは任意の順序で発生する可能性があり、1つのイベントは必ずしも他のイベントに付随するわけではありません。

中間ドライバーの仮想ミニポートの上端が、電源を動作状態に設定する要求を受信すると、要求を処理するためのイベントのシーケンスは次のようになります。

1.  NDIS は、中間ドライバーの仮想ミニポートに[\_電力を設定する OID\_PNP\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)発行します。 中間ドライバーは、NDIS\_STATUS\_SUCCESS を set power request に返します。 中間ドライバーでは、\_電源要求の OID\_\_PNP を基になるミニポートドライバーに伝達することはできません。

2.  NDIS は仮想ミニポートを再起動した後、設定された power OID を発行した後、それ以降のドライバーを再起動します。 仮想ミニポートの再起動の詳細については、「[アダプターの開始](starting-an-adapter.md)」を参照してください。

3.  NDIS は、プロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 *ProtocolNetPnPEvent*を呼び出すと、動作状態 (D0) を設定する**NetEventSetPower**イベントが指定されます。 バインドされたプロトコルドライバーは、中間ドライバーの仮想ミニポートにネットワークデータの送信を開始できます。

中間のドライバーの下端が、基になるミニポートドライバーを動作状態に移行すると、遷移を処理するためのイベントのシーケンスは次のようになります。

1.  NDIS は、基になるミニポートドライバーに\_電力を設定するか、基になるミニポートドライバーが停止した場合に[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)ハンドラーを呼び出すことにより、 [OID\_\_PNP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)を発行します。

2.  NDIS は、基になるミニポートドライバーを再起動し、OID を発行した後、中間 NDIS および基になるミニポートアダプターのプロトコルエッジを再起動します。 プロトコルバインドの一時停止の詳細については、「[バインディングの再起動](restarting-a-binding.md)」を参照してください。

3.  NDIS は、中間ドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 *ProtocolNetPnPEvent*を呼び出すと、動作状態 (D0) を設定する**NetEventSetPower**イベントが指定されます。 中間ドライバーは、基になるミニポートドライバーへのネットワークデータの送信を開始できます。

### <a name="power-states-and-the-standby-flag"></a>電源の状態とスタンバイフラグ

中間ドライバーは、各仮想ミニポートインスタンスと、ドライバーがバインドされている基になるミニポートドライバーごとに、個別の電源状態変数を保持する必要があります。 中間ドライバーも、次のような仮想ミニポートごとにスタンドアロンフラグを維持する必要があります。

-   仮想ミニポートまたは基になるミニポートドライバーの電源状態が D0 のままである場合は、 **TRUE**に設定します。

-   仮想ミニポートまたは基になるミニポートドライバーの電源状態が D0 に戻る場合は、 **FALSE**に設定します。

  **注**MUX 中間ドライバーでは、基になるミニポートドライバーに関連付けられている複数の仮想ミニポート、または各仮想ミニポートに関連付けられている複数の基になるミニポートが存在する場合があります。 ミニポートアダプターの電源状態が変化すると、関連付けられているすべてのミニポートの動作も影響を受けます。 動作がどのように影響を受けるかは、実装に固有のものです。 たとえば、負荷分散フェールオーバー (LBFO) ソリューションを実装するドライバーは、基になる1つのミニポートドライバーが非アクティブ化されている場合に、仮想ミニポートを非アクティブ化しないことがあります。 ただし、基になるすべてのミニポートドライバーに依存するドライバーの実装では、基になるミニポートドライバーが非アクティブ化されるときに、仮想ミニポートの非アクティブ化が必要になります。

 

中間ドライバーは、次のように要求を処理するときに、スタンドアロンフラグと電源状態変数を使用する必要があります。

-   仮想ミニポートとその基になるミニポートアダプターの両方が D0 にある場合を除き、ドライバーの[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数は失敗します。

-   ドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、常に\_PNP\_クエリ\_電源に成功する必要があります。これにより、ドライバーは、その後、電源要求\_設定された後続の OID\_PNP を受け取ることができます。

-   仮想ミニポートが D0 にない場合、またはスタンドアロンが**TRUE**の場合、ドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は失敗します。 それ以外の場合は、基になるミニポートドライバーが D0 にない場合は、単一の要求をキューに置いてください。 基になるミニポートドライバーの状態が D0 になると、キューに登録された要求を処理する必要があります。

-   中間のドライバー仮想ミニポートは、基になるミニポートドライバーと仮想ミニポートの両方が D0 にある場合にのみ、ステータスを報告する必要があります。

 

 





