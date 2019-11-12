---
title: 着信呼び出しの受け入れ
description: 着信呼び出しの受け入れ
ms.assetid: bca837dc-b3de-4aca-9fc2-aed2faab1377
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、着信呼び出し
- 電話 services WDK WAN、着信呼び出し
- CoNDIS TAPI WDK ネットワーク、着信呼び出し
- NDPROXY WDK ネットワーク、着信呼び出し
- 着信呼び出しの WDK CoNDIS WAN
- WDK を呼び出す WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d8b041ce1495648f6a2512acc9c456c2e9759e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838255"
---
# <a name="accepting-incoming-calls"></a>着信呼び出しの受け入れ





アプリケーションは、受信呼び出しを受け入れる前に、最初に行を開いておく必要があります。 アプリケーションが TAPI **Lineopen**関数を呼び出した結果として、行が開かれます。 この TAPI 関数呼び出しにより、基になるドライバーは、受信呼び出しの受信を準備するために、NDIS 構造体に TAPI パラメーターをカプセル化します。 CoNDIS WAN ミニポートドライバーが着信呼び出しを受信した後、ミニポートドライバーは、まず NDPROXY ドライバーを使用して仮想接続 (VC) を作成し、次に着信呼び出しの NDPROXY に通知する必要があります。 NDPROXY は、TAPI によってアプリケーションに通知します。 次の一覧は、着信呼び出しの設定、接続、および作成方法を示しています。

-   NDPROXY は、受信接続の TAPI パラメーターを[**CO\_AF\_tapi\_SAP**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545376(v=vs.85))構造体で指定します。 NDPROXY は、この構造体のメンバーに、TAPI **Lineopen**関数で渡された次の情報を入力します。
    -   **UlLineID**メンバー内のオープンライン識別子
    -   **Uladdressid**メンバー内の受信接続のアドレス
    -   **UlMediaModes**メンバー内の受信接続の情報ストリームのメディアモード
-   NDPROXY は co\_AF\_TAPI\_SAP 構造体を[**co\_sap**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))構造の**sap メンバーに**オーバーレイし、Co\_sap の**SAPLENGTH**メンバーを co\_AF\_TAPI のサイズに設定し\_SAP。 NDPROXY では、CO\_SAP の sap**型**メンバーを AF\_TAPI\_SAP\_型に設定する必要もあります。

-   NDPROXY が TAPI パラメーターをカプセル化すると、NDPROXY は[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)関数を呼び出して、受信呼び出しを受信できるようにします。 この関数呼び出しでは、ndproxy は、NDPROXY が着信呼び出しを受信できるサービスアクセスポイント (SAP) を指定する、入力された CO\_SAP 構造体へのポインターを渡します。 NDIS は、CO\_SAP 構造体を CoNDIS WAN ミニポート呼び出しマネージャー (MCM) ドライバーの*Protocolcmregistersap*関数に転送します。 *Protocolcmregistersap*は、必要に応じてネットワークコントロールデバイスやその他のメディア固有のエージェントと通信し、ndproxy のネットワーク上に SAP を登録します。 ミニポートドライバーによって SAP が登録されると、その SAP に送られる着信呼び出しプランを受け入れることができます。

-   ネットワークからのメッセージをシグナリングすることで、着信呼び出しに対して CoNDIS WAN ミニポートドライバーが通知されます。 これらのシグナルメッセージから、コールミニドライバーは、呼び出しの呼び出しパラメーターを抽出します。これには、着信呼び出しの宛先となる SAP も含まれます。

-   NDPROXY への着信呼び出しを示す前に、ミニポートドライバーは[**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)関数を呼び出して、ndproxy を使用した VC の作成を開始します。 NDPROXY は、VC に必要なリソースを割り当てて初期化し、そのハンドルを VC に格納します。

-   CoNDIS WAN ミニポートドライバーは、入力された通話の TAPI パラメーターを、 [**CO\_AF\_tapi\_着信\_\_parameters**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545372(v=vs.85))構造体に設定します。 ミニポートドライバーは、この構造体のメンバーに、シグナリングメッセージから抽出された次の情報を入力します。
    -   **UlLineID**メンバーの行識別子
    -   **Uladdressid**メンバー内の着信呼び出しのアドレス
    -   CO\_TAPI\_フラグ\_、 **Ulflags**メンバーの着信\_呼び出しビットです。 **Ulflags**のその他すべてのビットは予約されており、0に設定する必要があります。
    -   **LineCallInfo**メンバーの LINECALLPARAMS 構造体。 LINECALLPARAMS のメンバーは、着信呼び出しの TAPI 呼び出しパラメーターを指定します。
-   ミニポートドライバーは、co\_AF\_TAPI\_着信\_、 [**co\_特定の\_パラメーター**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))構造の**パラメーター**メンバーに\_パラメーターを呼び出して、の**長さ**のメンバーを設定します。特定の\_パラメーターを co\_AF\_TAPI のサイズに\_し、\_パラメーターを呼び出します。\_\_

-   ミニポートドライバーは、co\_固有の\_パラメーター構造を[**co\_MEDIA\_PARAMETERS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545388(v=vs.85))構造体の**MediaSpecific**メンバーに設定します。

-   ミニポートドライバーは、CO\_MEDIA\_PARAMETERS 構造体へのポインターを、 [**co\_呼び出し\_parameters**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体の**MediaParameters**メンバーに設定します。

-   また、ミニポートドライバーは、CO\_CALL\_PARAMETERS 構造体の**CallMgrParameters**メンバーを設定して、帯域幅などのパケット転送のサービス品質 (QoS) を指定する必要があります。 この**CallMgrParameters**メンバーを設定するために、ミニポートドライバーは、 [**CO\_呼び出し\_MANAGER\_PARAMETERS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))構造体のメンバーを読み込み、この構造体を**CallMgrParameters**に指定します。 たとえば、VC の1秒あたりの送信速度と受信速度を示すために、ミニポートドライバーは、CO\_CALL\_MANAGER の**送信**メンバーと**受信**メンバーの**peakbandwidth 幅**メンバーを設定する必要があり\_パラメータ. **送信**メンバーと**受信**メンバーは FLOWSPEC 構造体です。 FLOWSPEC 構造体の詳細については、Microsoft Windows SDK を参照してください。

-   ミニポートドライバーによって TAPI パラメーターがカプセル化され、 **CallMgrParameters**メンバーが CO\_呼び出し\_MANAGER\_パラメーターに入力された後、 [**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)関数を呼び出して、への着信呼び出しを示します。NDPROXY。 この呼び出しでは、ミニポートドライバーは次のものを渡します。
    -   着信呼び出しの宛先となる SAP を識別するハンドル
    -   着信呼び出しの VC を識別するハンドル
    -   入力された CO\_呼び出し\_PARAMETERS 構造体へのポインター
-   NDPROXY は、NDIS\_STATUS\_をミニポートドライバーに返します。これにより、NDPROXY は**NdisMCmDispatchIncomingCall**を非同期に完了できます。

-   TAPI アプリケーションが**Lineanswer**関数を使用して着信呼び出しに応答すると、Ndproxy は[**NdisClIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclincomingcallcomplete)関数を呼び出します。 さらに、NDIS はミニポートドライバーの*Protocolcmincomingcallcomplete*関数を呼び出します。 NDPROXY が NDIS\_STATUS\_SUCCESS コードを返す場合は、呼び出しパラメーターの受け入れを示します。 NDPROXY が呼び出しパラメーターを受け入れないことを検出した場合、呼び出しパラメーターの変更を要求できます。そのためには、CO\_呼び出し\_PARAMETERS 構造体に**Flags**メンバーを設定して、変更された\_パラメーターを呼び出し、変更した\_パラメーターを指定して変更します。パラメーターを呼び出します。 NDPROXY が着信呼び出しを受け入れる場合、ミニポートドライバーは、呼び出しが受け入れられたことを呼び出し元のエンティティに示すために、シグナリングメッセージを送信する必要があります。 それ以外の場合、ミニポートドライバーは、呼び出しが拒否されたことを示すシグナルメッセージを送信する必要があります。 NDPROXY が呼び出しパラメーターの変更を要求している場合、ミニポートドライバーは、シグナルメッセージを送信して、呼び出しパラメーターの変更を要求します。

-   ミニポートドライバーは、NDPROXY で作成されたミニポートドライバーで VC をアクティブにします。また、 [**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)関数を呼び出して、ミニポートドライバーが vc でパケットを転送する準備ができていることを ndproxy に通知する必要もあります。

-   NDPROXY が呼び出しを拒否した場合、ミニポートドライバーは[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)関数を呼び出して、ミニポートドライバーが受信呼び出し用に作成した VC を非アクティブにします。 VC が非アクティブになると、ミニポートドライバーは[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)関数を呼び出して vc を削除します。

-   NDPROXY が着信呼び出しを受け入れたかどうか、およびエンドツーエンド接続が正常に確立されたかどうかに応じて、ミニポートドライバーは[**NdisMCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchcallconnected)関数または[**NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingclosecall)関数のいずれかを呼び出します. リモート呼び出しエンティティが呼び出しを t とすると、エンドツーエンドの接続が正常に確立されなかったことを示すシグナリングメッセージが送信されることに注意してください。 **NdisMCmDispatchCallConnected**は、ミニポートドライバーが受信呼び出し用に作成およびアクティブ化した VC でデータ転送を開始できることを ndproxy に通知します。 **NdisMCmDispatchIncomingCloseCall**は、入力された呼び出しを破棄するように ndproxy に通知します。

-   NDPROXY が着信呼び出しを破棄するように指定されている場合は、 [**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)関数を呼び出して、VC でのデータの受信を試行しないことを確認します。 さらに、NDIS はミニポートドライバーの*ProtocolCmCloseCall*関数を呼び出します。 次に、ミニポートドライバーは、 **NdisMCmDeactivateVc**関数を呼び出して VC を非アクティブ化します。 VC が非アクティブになると、ミニポートドライバーは**NdisMCmDeleteVc**関数を呼び出して vc を削除します。

-   TAPI アプリケーションが着信呼び出しを受け入れ、NDPROXY が呼び出しが接続されていることをアプリケーションに通知した後、アプリケーションは TAPI **lineGetID**関数を呼び出して、ndproxy に対して適切な condis 検索するように通知します。 この**lineGetID**の呼び出しでは、tapi アプリケーションは、アプリケーションがハンドルを必要とする特定の tapi デバイスクラスに文字列を提供します。 NDPROXY は、この文字列を使用して、以前に特定の TAPI デバイスクラスに対して SAP を登録した CoNDIS クライアントを検索します。 CoNDIS クライアントが指定されている場合、文字列は NDIS です。 NDPROXY が、TAPI アプリケーションによって渡された文字列と一致する文字列を含む SAP を検索する場合、NDPROXY は**NdisMCmCreateVc**を呼び出して、着信呼び出しの通知をディスパッチできる NDISWAN を持つ接続エンドポイントを設定します。 さらに、NDIS は NDISWAN の*ProtocolCoCreateVc*関数を呼び出し、VC を表すハンドルを渡します。

-   NDPROXY は、NDISWAN を使用して接続エンドポイントを設定した後、 [**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)関数を呼び出して、着信呼び出しについて NDISWAN に通知します。 この呼び出しでは、NDPROXY は、カプセル化された CO\_AF\_TAPI\_着信\_、着信呼び出しパラメーターを含む\_PARAMETERS 構造体を渡します。 さらに、NDIS は NDISWAN の*ProtocolClIncomingCall*関数を呼び出します。この関数では、要求された接続を受け入れるか拒否します。

-   接続を受け入れるかどうかを決定し、場合によっては呼び出しパラメーターを変更した後に、NDISWAN は**NdisClIncomingCallComplete**関数を呼び出します。 さらに、NDIS はミニポートドライバーの*Protocolcmincomingcallcomplete*関数を呼び出します。 NDISWAN が着信呼び出しを受け入れたかどうか、およびミニポートドライバーが呼び出しパラメーターに対する NDISWAN の提案された変更を受け入れるか拒否するかによって、ミニポートドライバーは**NdisCmDispatchCallConnected**または**を呼び出します。NdisCmDispatchIncomingCloseCall**関数。 **NdisCmDispatchCallConnected**は、ミニポートドライバーが受信呼び出し用に作成した VC でデータ転送を開始できることを NDISWAN に通知します。 **NdisCmDispatchIncomingCloseCall**は、着信呼び出しを破棄するように NDISWAN と ndproxy に通知します。

-   NDISWAN が着信呼び出しを受け入れると、NDPROXY は[**NdisCoGetTapiCallId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscogettapicallid)関数を呼び出して、VC の NDISWAN のコンテキストを識別する文字列を取得します。 NDPROXY は、この文字列を TAPI アプリケーションに渡します。 TAPI アプリケーションは、この VC コンテキスト文字列を使用して**lineGetID**の呼び出しを完了します。

 

 





