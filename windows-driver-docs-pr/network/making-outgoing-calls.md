---
title: 発信の実行
description: 発信の実行
ms.assetid: 295b3f6d-d53b-4030-b7e9-35ab7524d9aa
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、発信呼び出し
- 電話 services WDK WAN、発信呼び出し
- CoNDIS TAPI WDK ネットワーク、発信呼び出し
- 送信呼び出し WDK CoNDIS
- WDK を呼び出す WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84556e2595d728716f31c6b9cbc6c475d8804797
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844129"
---
# <a name="making-outgoing-calls"></a>発信の実行





アプリケーションが発信呼び出しを行う場合は、最初に行を開く必要があります。 アプリケーションが TAPI **Lineopen**関数を呼び出した結果として、行が開かれます。 前に開いた行にテレフォニー通話を配置するために、アプリケーションは TAPI **lineMakeCall**関数を呼び出し、特定の宛先アドレスへのポインターを渡します。 既定の呼び出しセットアップパラメーターが要求されていても、アプリケーションは、LINECALLPARAMS 構造体へのポインターを渡します。 アプリケーションで既定の呼び出し設定パラメーターが使用されている場合、 **lineMakeCall**はこれらのパラメーターを LINECALLPARAMS 構造体に提供します。 この構造体のメンバーは、テレフォニー呼び出しの設定方法を指定します。

これらの TAPI 関数呼び出しによって、NDPROXY ドライバーは、最初に CoNDIS WAN ミニポートドライバーを使用して仮想接続 (VC) を作成し、次に発信呼び出しを行うために NDIS 構造体に TAPI パラメーターをカプセル化します。 ミニポートドライバーは、これらの TAPI パラメーターを使用して発信呼び出しを設定します。 発信呼び出しの接続方法、設定方法、および発信方法を次に示します。

-   NDPROXY は[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)を呼び出し、ミニポートドライバーを使用して VC の作成を開始します。 NDPROXY が**NdisCoCreateVc**を呼び出すと、NDIS は、ミニポートドライバーに統合されている呼び出しマネージャーの*ProtocolCoCreateVc*関数を同期操作として呼び出します。 NDIS は、VC を表すハンドルを*ProtocolCoCreateVc*に渡します。 **NdisCoCreateVc**の呼び出しが成功した場合、NDIS は VC ハンドルを入力して返します。 *ProtocolCoCreateVc*は、ポートコールマネージャー (mcm) ドライバーが、後でアクティブ化される VC に対して後続の操作を実行するために必要な動的リソースおよび構造体に必要な割り当てを実行します。 このようなリソースには、メモリバッファー、データ構造、イベント、その他の同様のリソースが含まれますが、これらに限定されません。

-   NDPROXY は、 [**CO\_AF\_tapi**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545373(v=vs.85))の送信通話に使用する tapi パラメーターを指定します。これにより、\_パラメーター構造\_呼び出し\_ます。 NDPROXY は、この構造体のメンバーに、TAPI **lineMakeCall**関数で渡された次の情報を入力します。
    -   **Destaddress**メンバーの宛先アドレス
    -   **UlLineID**メンバー内のオープンライン識別子
    -   **LINECALLPARAMS**メンバーの LINECALLPARAMS 構造体
-   NDPROXY は CO\_AF\_TAPI をオーバーレイし\_\_co [ **\_特定の\_パラメーター**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))構造の**パラメーター**メンバーに\_パラメーター構造を呼び出し、co の**Length**メンバーを設定します。\_特定の\_パラメーターを CO\_AF\_TAPI\_のサイズに設定し\_パラメーターを呼び出します。

-   NDPROXY は、co\_固有の\_パラメーター構造を[**co\_MEDIA\_PARAMETERS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545388(v=vs.85))構造体の**MediaSpecific**メンバーに設定します。

-   NDPROXY は、CO\_MEDIA\_PARAMETERS 構造体へのポインターを、 [**co\_呼び出し\_parameters**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体の**MediaParameters**メンバーに設定します。

-   NDPROXY が TAPI パラメーターをカプセル化すると、NDPROXY は[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)関数を呼び出して発信呼び出しを開始します。 この関数呼び出しでは、NDPROXY は、入力された CO\_呼び出し\_PARAMETERS 構造体へのポインターを渡します。 さらに、NDIS は、CoNDIS WAN ミニポートドライバーの呼び出しマネージャーの[**ProtocolCmMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_make_call)関数を呼び出します。 ミニポートドライバーでは、CO\_AF\_TAPI\_を確認する必要があります。これにより、\_は\_パラメーター構造に埋め込まれた\_パラメーター構造を呼び出します。 この場合、他の呼び出しパラメーターは意味がありません。 その後、ミニポートドライバーが発信呼び出しの VC をアクティブにすると、ミニポートドライバーは[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)関数を呼び出し、入力された CO\_呼び出し\_パラメーターへのポインターを渡します。

-   ミニポートドライバーがネットワークとネゴシエートし、VC のテレフォニー呼び出しパラメーターを確立し、これらの呼び出しパラメーター用に NIC を設定した後、ミニポートドライバーは[**NdisMCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmakecallcomplete)関数を呼び出して、準備ができていることを示します。VC でのデータ転送。 この呼び出しでは、ミニポートドライバーは、テレフォニー呼び出しパラメーターに加えられた VC および変更のハンドルを渡す必要があります。

-   ミニポートドライバーは、CO\_CALL\_PARAMETERS 構造体の**CallMgrParameters**メンバーを変更して、帯域幅などのパケット転送のサービス品質 (QoS) を指定する必要があります。 この**CallMgrParameters**メンバーを設定するために、ミニポートドライバーは、 [**CO\_呼び出し\_MANAGER\_PARAMETERS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))構造体のメンバーを読み込み、この構造体を**CallMgrParameters**に指定します。 たとえば、VC の1秒あたりの送信速度と受信速度を示すために、ミニポートドライバーは、CO\_CALL\_MANAGER の**送信**メンバーと**受信**メンバーの**peakbandwidth 幅**メンバーを設定する必要があり\_パラメータ. **送信**メンバーと**受信**メンバーは FLOWSPEC 構造体です。 FLOWSPEC 構造体の詳細については、Microsoft Windows SDK を参照してください。

-   ミニポートドライバーがテレフォニー呼び出しパラメーターを変更した場合は、\_パラメーター\_変更された呼び出しを使用して、CO\_呼び出し\_パラメーター構造体に**フラグ**メンバーを設定する必要があります。 ミニポートドライバーによって実行される**NdisMCmMakeCallComplete**呼び出しの結果として、NDIS は、 **NdisClMakeCall**で開始された非同期操作を完了するために、ndproxy の*ProtocolClMakeCallComplete*関数を呼び出します。

-   ミニポートドライバーが発信呼び出しを正常に完了すると、NDPROXY は、その呼び出しが接続されていることを TAPI アプリケーションに通知します。 次に、この TAPI アプリケーションは、TAPI **lineGetID**関数を呼び出して、ndproxy に適切な condis クライアントを特定するように通知します。 この**lineGetID**の呼び出しでは、tapi アプリケーションは、アプリケーションがハンドルを必要とする特定の tapi デバイスクラスに文字列を提供します。 NDPROXY は、この文字列を使用して、以前に特定の TAPI デバイスクラスに対して SAP を登録した CoNDIS クライアントを検索します。 CoNDIS クライアントが指定されている場合、文字列は NDIS です。 NDPROXY が、TAPI アプリケーションによって渡された文字列と一致する文字列を含む SAP を検索する場合、NDPROXY は[**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)を呼び出して、作成された発信呼び出しの通知をディスパッチできる NDISWAN の接続エンドポイントを設定します。 さらに、NDIS は NDISWAN の*ProtocolCoCreateVc*関数を呼び出し、VC を表すハンドルを渡します。

-   NDPROXY は、NDISWAN を使用して接続エンドポイントを設定した後、 [**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)関数を呼び出して、送信された呼び出しについて NDISWAN に通知します。 この呼び出しでは、NDPROXY はカプセル化された CO\_AF\_TAPI\_\_渡し、発信呼び出しパラメーターを含む\_PARAMETERS 構造体を呼び出します。 さらに、NDIS は NDISWAN の*ProtocolClIncomingCall*関数を呼び出します。この関数では、要求された接続を受け入れるか拒否します。 渡された呼び出しパラメーターが NDISWAN によって変更された場合は、\_パラメーターを呼び出して変更\_、CO\_呼び出し\_PARAMETERS 構造体に**Flags**メンバーを設定する必要があります。

-   接続を受け入れるかどうかを決定し、場合によっては呼び出しパラメーターを変更した後に、NDISWAN は[**NdisClIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclincomingcallcomplete)関数を呼び出します。 さらに、NDIS はミニポートドライバーの*Protocolcmincomingcallcomplete*関数を呼び出します。 NDISWAN が発信呼び出しを受け入れたかどうか、およびミニポートドライバーが呼び出しパラメーターに対する NDISWAN の提案された変更を受け入れるか拒否するかによって、ミニポートドライバーは[**NdisCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchcallconnected)または[**を呼び出します。NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall)関数。 **NdisCmDispatchCallConnected**は、送信呼び出し用に作成された、ndproxy がある VC でデータ転送を開始できることを NDISWAN に通知します。 **NdisCmDispatchIncomingCloseCall**は、提案された発信呼び出しを破棄するように NDISWAN と ndproxy に通知します。

-   NDISWAN が発信呼び出しを受け入れると、NDPROXY は[**NdisCoGetTapiCallId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscogettapicallid)関数を呼び出して、VC の NDISWAN のコンテキストを識別する文字列を取得します。 NDPROXY は、この文字列を TAPI アプリケーションに渡します。 TAPI アプリケーションは、この VC コンテキスト文字列を使用して**lineGetID**の呼び出しを完了します。

 

 





