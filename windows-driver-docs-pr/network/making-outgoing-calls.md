---
title: 発信呼び出しを行う
description: 発信呼び出しを行う
ms.assetid: 295b3f6d-d53b-4030-b7e9-35ab7524d9aa
keywords:
- 発信呼び出しいる CoNDIS WAN のドライバー WDK ネットワーク
- 発信呼び出し WDK WAN、電話サービス
- いる CoNDIS TAPI WDK ネットワー キング、発信呼び出し
- WDK いる CoNDIS WAN の呼び出しを送信
- WDK いる CoNDIS WAN の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23022830173e92f28af2c28192824bc68dcfdc02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530016"
---
# <a name="making-outgoing-calls"></a>発信呼び出しを行う





アプリケーションは、発信通話を試みると、行を初めて開くする必要があります。 TAPI を呼び出すアプリケーションの結果として、行が開かれる**lineOpen**関数。 アプリケーションが、TAPI を呼び出す前に開かれた行にテレフォニーの呼び出しを配置する**lineMakeCall**関数を特定の宛先アドレスへのポインターを渡します。 パラメーターが要求されたセットアップの呼び出しが既定以外の場合、アプリケーションはまた、ポインターを LINECALLPARAMS 構造体を渡します。 アプリケーションが既定のセットアップの呼び出しのパラメーターを使用している場合**lineMakeCall** LINECALLPARAMS 構造体でこれらのパラメーターを提供します。 この構造体のメンバーでは、方法、テレフォニーの呼び出しではその設定をする必要がありますを指定します。

まずいる CoNDIS WAN ミニポート ドライバーを使用した仮想接続 (VC) を作成する NDPROXY ドライバーにより、これらの TAPI 関数呼び出しと、TAPI をカプセル化する NDIS 内のパラメーター構造体に、発信通話を行うためにします。 ミニポート ドライバーは発信通話を設定するこれらの TAPI パラメーターを使用します。 送信呼び出しが接続されている、設定、および行われる方法を次に示します。

-   NDPROXY 呼び出し[ **NdisCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561696)ミニポート ドライバーを使用した VC の作成を開始します。 NDPROXY 後**NdisCoCreateVc**、NDIS 呼び出しを同期操作として、 *ProtocolCoCreateVc*ミニポート ドライバーにコール マネージャーの機能が統合します。 NDIS に渡します*ProtocolCoCreateVc* VC を表すハンドルです。 場合に呼び出し**NdisCoCreateVc**が成功すると、NDIS 入力し、VC ハンドルを返します。 *ProtocolCoCreateVc*動的リソースおよびミニポートの呼び出しのマネージャー (MCM) ドライバーは、後でアクティブにされる VC の後続の処理を実行する必要があります構造のために必要な割り当てを実行します。 このようなリソースなどが、メモリ バッファー、データ構造体、イベント、およびそのようなその他の同様のリソースに限定されません。

-   NDPROXY で発信呼び出しの TAPI パラメーターを指定する、 [ **CO\_AF\_TAPI\_ように\_呼び出す\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff545373)構造体。 NDPROXY、TAPI で渡された次の情報でこの構造体のメンバーを格納する**lineMakeCall**関数。
    -   内の宛先アドレス、 **DestAddress**メンバー
    -   開く行識別子、 **ulLineID**メンバー
    -   構造体、LINECALLPARAMS、 **LineCallParams**メンバー
-   NDPROXY オーバーレイ CO\_AF\_TAPI\_こと\_呼び出す\_でパラメーターが構造体、**パラメーター**のメンバー、 [ **CO\_特定\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff545396)構造と設定、**長さ**CO のメンバー\_特定\_CO のサイズ パラメーター\_AF\_TAPI\_ように\_呼び出す\_パラメーター。

-   NDPROXY 設定 CO\_特定\_パラメーター構造体を**MediaSpecific**のメンバー、 [ **CO\_メディア\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff545388)構造体。

-   NDPROXY CO にポインターを設定する\_メディア\_パラメーター構造体を**MediaParameters**のメンバー、 [ **CO\_呼び出す\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff545384)構造体。

-   NDPROXY を呼び出す NDPROXY は、TAPI パラメーターをカプセル化すると、 [ **NdisClMakeCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561635)発信通話を開始する関数。 この関数の呼び出しで NDPROXY は塗りつぶされた CO にポインターを渡します\_呼び出す\_パラメーター構造体。 さらに NDIS、 [ **ProtocolCmMakeCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570246)いる CoNDIS WAN ミニポート ドライバーのコール マネージャーの関数。 ミニポート ドライバーが CO のみを調べる必要があります\_AF\_TAPI\_ように\_を呼び出す\_パラメーターに構造体に埋め込まれた CO\_呼び出す\_パラメーター。 その他の呼び出しのパラメーターがない意味のあるこの場合です。 ミニポート ドライバーを呼び出す場合は、その後、ミニポート ドライバーには、発信通話の VC がアクティブに、 [ **NdisMCmActivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562792)関数し、塗りつぶされた CO にポインターを渡す\_の呼び出し\_パラメーター。

-   後、ミニポート ドライバーは、VC のテレフォニー呼び出しのパラメーターを確立し、それらの NIC を設定するネットワークとネゴシエートしたパラメーター、ミニポート ドライバーの呼び出しを呼び出し、 [ **NdisMCmMakeCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563544) VC 上の関数をデータ準備ができたことを示すために転送します。 この呼び出しで、ミニポート ドライバーは、VC とテレフォニー呼び出しのパラメーターに加えられた変更にハンドルを渡す必要があります。

-   ミニポート ドライバーを変更する必要があります、 **CallMgrParameters** CO のメンバー\_呼び出す\_帯域幅などのパケットを転送するサービス (QoS) の品質を指定するパラメーターの構造体。 これを設定する**CallMgrParameters**メンバー、ミニポート ドライバーがのメンバー、 [ **CO\_呼び出す\_MANAGER\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff545381)構造体し、この構造体を指す**CallMgrParameters**します。 たとえば、送信し、(VC の 1 秒あたりのバイト単位) の速度が表示される、ミニポート ドライバー設定する必要があります、**数字再生 PeakBandwidth**のメンバー、**送信**と**受信**CO のメンバー\_呼び出す\_MANAGER\_パラメーター。 **送信**と**受信**メンバーは FLOWSPEC 構造体。 FLOWSPEC 構造の詳細については、Microsoft Windows SDK を参照してください。

-   ミニポート ドライバーがテレフォニー呼び出しのパラメーターを変更している場合に設定する必要があります、**フラグ**CO 内のメンバー\_呼び出す\_呼び出しでパラメーター構造体\_パラメーター\_変更しました。 結果として、 **NdisMCmMakeCallComplete** NDPROXY を呼び出し、NDIS ミニポート ドライバーによって行われた呼び出し*ProtocolClMakeCallComplete*関数が開始された非同期操作を完了するには**NdisClMakeCall**します。

-   ミニポート ドライバーには、送信呼び出しが完了したら後、NDPROXY は呼び出しが接続されている TAPI アプリケーションを通知します。 この TAPI アプリケーションは、呼び出し、TAPI **lineGetID** NDPROXY 適切ないる CoNDIS クライアントに通知する関数。 この**lineGetID**呼び出し、TAPI アプリケーションにはこれをアプリケーションにハンドルが必要です。 特定の TAPI デバイス クラスの文字列が指定されています。 NDPROXY では、この文字列を使用して、特定の TAPI デバイス クラスに対する SAP に登録されている CoNDIS クライアントを見つけます。 いる CoNDIS クライアントが NDISWAN の場合は、文字列は、NDIS です。 かどうか、NDPROXY を見つけて、TAPI アプリケーション NDPROXY 呼び出しで渡される文字列に一致する文字列での SAP [ **NdisMCmCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562812) NDISWAN をディスパッチできますと接続エンドポイントを設定するには実行された送信呼び出しの通知です。 NDIS 呼び出します NDISWAN の*ProtocolCoCreateVc*関数し、VC を表すハンドルを渡します。

-   呼び出す NDPROXY が NDISWAN と接続エンドポイントを設定した後、 [ **NdisCmDispatchIncomingCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561664)送信呼び出しについて NDISWAN を通知する関数。 この呼び出しでは、NDPROXY はカプセル化された CO を渡します。\_AF\_TAPI\_ように\_呼び出し\_パラメーター構造体を含む、送信呼び出しのパラメーター。 NDIS 呼び出します NDISWAN の*ProtocolClIncomingCall*関数を NDISWAN を受け入れるか、要求された接続を拒否します。 NDISWAN には渡された呼び出しのパラメーターが変更された場合に設定する必要があります、**フラグ**CO でメンバー\_呼び出す\_呼び出しでパラメーター構造体\_パラメーター\_変更されました。

-   接続を許可するかどうかを決定した後と、場合によって、呼び出しのパラメーターを変更した後に、NDISWAN の呼び出し、 [ **NdisClIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561632)関数。 NDIS ミニポート ドライバーに呼び出されます*ProtocolCmIncomingCallComplete*関数。 NDISWAN が発信通話を承諾したかどうかや、ミニポート ドライバーを受け入れるか NDISWAN の呼び出しのパラメーターに変更の提案を拒否するかどうか、によって、ミニポート ドライバーを呼び出すか[ **NdisCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff561661)または[ **NdisCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561670)関数。 **NdisCmDispatchCallConnected** NDISWAN VC NDPROXY 作成発信呼び出しでデータ転送を開始できることを通知します。 **NdisCmDispatchIncomingCloseCall** NDISWAN と NDPROXY 提案の送信呼び出しを壊さずに通知します。

-   発信通話を承諾した後 NDISWAN、NDPROXY を呼び出す、 [ **NdisCoGetTapiCallId** ](https://msdn.microsoft.com/library/windows/hardware/ff561700) VC の NDISWAN のコンテキストを識別する文字列を取得する関数。 NDPROXY は、TAPI アプリケーションにこの文字列を渡します。 TAPI アプリケーションでは、この VC コンテキストの文字列を使用して、呼び出しを完了する**lineGetID**します。

 

 





