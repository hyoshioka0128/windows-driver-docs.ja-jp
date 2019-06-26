---
title: 着信呼び出しの受け入れ
description: 着信呼び出しの受け入れ
ms.assetid: bca837dc-b3de-4aca-9fc2-aed2faab1377
keywords:
- いる CoNDIS WAN ドライバー WDK、ネットワークの着信呼び出し
- WDK WAN、着信電話サービス
- いる CoNDIS TAPI WDK、ネットワークの着信呼び出し
- NDPROXY WDK、ネットワークの着信呼び出し
- 着信呼び出しの WDK いる CoNDIS WAN
- WDK いる CoNDIS WAN の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a90c92c71a2b362cec0f11be80b0c46889c4dbb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378698"
---
# <a name="accepting-incoming-calls"></a>着信呼び出しの受け入れ





アプリケーションでは、着信呼び出しを使用できますが、前にまずが必要開く行です。 TAPI を呼び出すアプリケーションの結果として、行が開かれる**lineOpen**関数。 この TAPI 関数呼び出しには、着信呼び出しを受信するための準備をするために TAPI NDIS 構造体のパラメーターをカプセル化する基になるドライバーが原因です。 いる CoNDIS WAN ミニポート ドライバーが着信呼び出しを受信した後、ミニポート ドライバーは NDPROXY ドライバーを使用した仮想接続 (VC) をまず作成し、着信通話の NDPROXY に通知します。 NDPROXY は、TAPI 経由でアプリケーションをさらに通知します。 次の一覧は、接続、および作成に、着信呼び出しを設定する方法について説明します。

-   NDPROXY で着信接続の TAPI パラメーターを指定する、 [ **CO\_AF\_TAPI\_SAP** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545376(v=vs.85))構造体。 NDPROXY、TAPI で渡された次の情報でこの構造体のメンバーを格納する**lineOpen**関数。
    -   開く行識別子、 **ulLineID**メンバー
    -   着信接続のアドレス、 **ulAddressID**メンバー
    -   着信接続の情報ストリームのメディア モード、 **ulMediaModes**メンバー
-   NDPROXY オーバーレイ CO\_AF\_TAPI\_上の SAP 構造、 **Sap**のメンバー、 [ **CO\_SAP** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))構造体設定と、 **SapLength** CO のメンバー\_CO のサイズに SAP\_AF\_TAPI\_SAP します。 NDPROXY を設定する必要がありますも、 **SapType** CO のメンバー\_AF に SAP\_TAPI\_SAP\_型。

-   NDPROXY を呼び出す NDPROXY は、TAPI パラメーターをカプセル化すると、 [ **NdisClRegisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap)自体を着信呼び出しを受信できる状態にします。 この関数の呼び出しで NDPROXY は塗りつぶされた CO にポインターを渡します\_NDPROXY が着信呼び出しを受信できるサービス アクセス ポイント (SAP) を指定する SAP 構造体。 NDIS 転送 CO\_SAP 構造体を*ProtocolCmRegisterSap*いる CoNDIS WAN ミニポート コール マネージャー (MCM) ドライバーの機能です。 *ProtocolCmRegisterSap* NDPROXY のネットワーク上の SAP の登録に、必要に応じてネットワーク デバイスの制御やその他のメディア固有エージェントと通信します。 ミニポート ドライバーが登録されると、SAP、その SAP に送信、受信呼び出しプランを受け入れることができます。

-   ネットワークからの着信通話をするシグナリング メッセージによっている CoNDIS WAN ミニポート ドライバーで発生します。 シグナリング メッセージから、ミニポート ドライバーは、着信呼び出しが対応する SAP を含む、呼び出しの呼び出しのパラメーターを抽出します。

-   ミニポート ドライバーを呼び出す NDPROXY に着信呼び出しを示す、前に、 [ **NdisMCmCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc) NDPROXY と VC の作成を開始する関数。 NDPROXY では、割り当て、VC に必要なリソースを初期化しますと VC を識別するハンドルを格納します。

-   いる CoNDIS WAN ミニポート ドライバーでの着信呼び出しの TAPI パラメーターの設定、 [ **CO\_AF\_TAPI\_受信\_呼び出す\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545372(v=vs.85))構造体。 ミニポート ドライバーでは、シグナリング メッセージから抽出した次の情報でこの構造体のメンバーを塗りつぶします。
    -   行の識別子、 **ulLineID**メンバー
    -   着信呼び出しのアドレス、 **ulAddressID**メンバー
    -   CO\_TAPI\_フラグ\_受信\_でビットを呼び出す、 **ulFlags**メンバー。 その他のすべてのビット**ulFlags**は予約されており、0 に設定する必要があります。
    -   構造体 LINECALLPARAMS、 **LineCallInfo**メンバー。 LINECALLPARAMS のメンバーでは、着信呼び出しの TAPI 呼び出しのパラメーターを指定します。
-   ミニポート ドライバー オーバーレイ CO\_AF\_TAPI\_受信\_呼び出す\_パラメーターを**パラメーター**のメンバー、 [ **CO\_特定\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))構造と設定、**長さ**CO のメンバー\_特定\_CO のサイズ パラメーター\_AF\_TAPI\_受信\_呼び出す\_パラメーター。

-   ミニポート ドライバーの設定、CO\_特定\_パラメーター構造体を**MediaSpecific**のメンバー、 [ **CO\_メディア\_パラメーター**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545388(v=vs.85))構造体。

-   ミニポート ドライバーの CO にポインターを設定\_メディア\_パラメーター構造体を**MediaParameters**のメンバー、 [ **CO\_呼び出す\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体。

-   ミニポート ドライバーを設定する必要がありますも、 **CallMgrParameters** CO のメンバー\_呼び出す\_帯域幅などのパケットを転送するサービス (QoS) の品質を指定するパラメーターの構造体。 これを設定する**CallMgrParameters**メンバー、ミニポート ドライバーがのメンバー、 [ **CO\_呼び出す\_MANAGER\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))構造体し、この構造体を指す**CallMgrParameters**します。 たとえば、送信し、(VC の 1 秒あたりのバイト単位) の速度が表示される、ミニポート ドライバー設定する必要があります、**数字再生 PeakBandwidth**のメンバー、**送信**と**受信**CO のメンバー\_呼び出す\_MANAGER\_パラメーター。 **送信**と**受信**メンバーは FLOWSPEC 構造体。 FLOWSPEC 構造の詳細については、Microsoft Windows SDK を参照してください。

-   TAPI パラメーターと塗りつぶし後、ミニポート ドライバーをカプセル化、 **CallMgrParameters** CO のメンバー\_呼び出し\_マネージャー\_呼び出し、パラメーター、 [ **NdisMCmDispatchIncomingCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcall) NDPROXY への着信通話を示す関数。 この呼び出しで、ミニポート ドライバーは、次に渡します。
    -   着信呼び出しが対応する SAP を識別するハンドル
    -   着信通話の VC を識別するハンドル
    -   塗りつぶされた CO へのポインター\_呼び出す\_パラメーター構造体
-   NDPROXY 返します NDIS\_状態\_NDPROXY を完了できるように、ミニポート ドライバーを PENDING **NdisMCmDispatchIncomingCall**非同期的にします。

-   アプリケーションの着信呼び出しの回答、TAPI の後、 **lineAnswer**関数、NDPROXY 呼び出し、 [ **NdisClIncomingCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclincomingcallcomplete)関数。 NDIS ミニポート ドライバーに呼び出されます*ProtocolCmIncomingCallComplete*関数。 NDPROXY、NDIS を返す場合\_状態\_成功コード、呼び出しパラメーターへの同意を示します。 設定して関数のパラメーターに変更を要求できる NDPROXY 検出と呼び出しのパラメーターが許容できない、**フラグ**CO でメンバー\_呼び出す\_パラメーター構造体の呼び出しを\_パラメーター\_CHANGED と変更後の呼び出しのパラメーターを指定しています。 ミニポート ドライバーに送信する必要があります NDPROXY が着信呼び出しを受け入れる場合の呼び出しが受け入れられたことを呼び出し元のエンティティに示すためにメッセージを通知します。 ミニポート ドライバーに送信する必要がありますそれ以外の場合、呼び出しが拒否されたことを示すメッセージを通知します。 場合 NDPROXY は、関数のパラメーター、シグナリング メッセージ呼び出しのパラメーターの変更を要求するミニポート ドライバーの送信に変更を要求しています。

-   ミニポート ドライバーに VC ミニポート ドライバーが NDPROXY を作成しても呼び出す必要がありますがアクティブ化、 [ **NdisMCmActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)ミニポート ドライバーが転送する準備が整っている NDPROXY に通知する関数VC 上のパケットです。

-   ミニポート ドライバーが呼び出す NDPROXY 呼び出しを拒否する場合、 [ **NdisMCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeactivatevc) VC ミニポート ドライバーが着信呼び出し用に作成を非アクティブ化する関数。 ミニポート ドライバーが呼び出す、VC が非アクティブ化した後、 [ **NdisMCmDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc) VC を削除する関数。

-   NDPROXY が着信通話を承諾したかどうかと、エンド ツー エンド接続が正常に確立されたかどうか、によって、ミニポート ドライバーを呼び出すか[ **NdisMCmDispatchCallConnected** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchcallconnected)または[ **NdisMCmDispatchIncomingCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingclosecall)関数。 注リモートの呼び出し元のエンティティは、呼び出しダウンされ、これから送信することシグナル通知は、エンド ツー エンド接続を正常に確立していないことを示すメッセージです。 **NdisMCmDispatchCallConnected** NDPROXY VC ミニポート ドライバーが作成され、着信通話のアクティブ化のデータ転送を開始できることを通知します。 **NdisMCmDispatchIncomingCloseCall** NDPROXY 着信通話を壊さずに通知します。

-   呼び出す NDPROXY が着信呼び出しを破棄する指示を受けた場合、 [ **NdisClCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)も送信も VC 上のデータを受信することを試みることが確認する関数。 NDIS ミニポート ドライバーに呼び出されます*ProtocolCmCloseCall*関数。 ミニポート ドライバーを呼び出して、 **NdisMCmDeactivateVc** VC を非アクティブ化する関数。 ミニポート ドライバーが呼び出す、VC が非アクティブ化した後、 **NdisMCmDeleteVc** VC を削除する関数。

-   TAPI を呼び出して、TAPI アプリケーションは、着信の呼び出しを受け付けるし、NDPROXY をアプリケーションに通知の呼び出しが接続されていること、 **lineGetID** NDPROXY 適切ないる CoNDIS クライアントに通知する関数。 この**lineGetID**呼び出し、TAPI アプリケーションにはこれをアプリケーションにハンドルが必要です。 特定の TAPI デバイス クラスの文字列が指定されています。 NDPROXY では、この文字列を使用して、特定の TAPI デバイス クラスに対する SAP に登録されている CoNDIS クライアントを見つけます。 いる CoNDIS クライアントが NDISWAN の場合は、文字列は、NDIS です。 かどうか、NDPROXY を見つけて、TAPI アプリケーション NDPROXY 呼び出しで渡される文字列に一致する文字列での SAP **NdisMCmCreateVc**着信通話の通知、送出できる NDISWAN と接続エンドポイントを設定します。 NDIS 呼び出します NDISWAN の*ProtocolCoCreateVc*関数し、VC を表すハンドルを渡します。

-   呼び出す NDPROXY が NDISWAN と接続エンドポイントを設定した後、 [ **NdisCmDispatchIncomingCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingcall) NDISWAN に着信通話を通知する関数。 この呼び出しで NDPROXY 渡しますカプセル化された CO\_AF\_TAPI\_受信\_呼び出す\_着信呼び出しのパラメーターを含むパラメーター構造体。 NDIS 呼び出します NDISWAN の*ProtocolClIncomingCall*関数を NDISWAN を受け入れるか、要求された接続を拒否します。

-   接続を許可するかどうかを決定した後と、場合によって、呼び出しのパラメーターを変更した後に、NDISWAN の呼び出し、 **NdisClIncomingCallComplete**関数。 NDIS ミニポート ドライバーに呼び出されます*ProtocolCmIncomingCallComplete*関数。 NDISWAN が着信通話を承諾したかどうかや、ミニポート ドライバーを受け入れるか NDISWAN の呼び出しのパラメーターに変更の提案を拒否するかどうか、によって、ミニポート ドライバーを呼び出すか**NdisCmDispatchCallConnected**または**NdisCmDispatchIncomingCloseCall**関数。 **NdisCmDispatchCallConnected** NDISWAN vc ミニポート ドライバーが着信呼び出し用に作成、データ転送が開始できることを通知します。 **NdisCmDispatchIncomingCloseCall** NDISWAN と NDPROXY 着信通話を壊さずに通知します。

-   着信通話を承諾した後 NDISWAN、NDPROXY を呼び出す、 [ **NdisCoGetTapiCallId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscogettapicallid) VC の NDISWAN のコンテキストを識別する文字列を取得する関数。 NDPROXY は、TAPI アプリケーションにこの文字列を渡します。 TAPI アプリケーションでは、この VC コンテキストの文字列を使用して、呼び出しを完了する**lineGetID**します。

 

 





