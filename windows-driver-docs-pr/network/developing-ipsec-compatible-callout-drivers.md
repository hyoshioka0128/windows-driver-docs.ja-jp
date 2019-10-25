---
title: IPsec と互換性のあるコールアウトドライバーの開発
description: IPsec と互換性のあるコールアウトドライバーの開発
ms.assetid: 5e4fad4e-a790-4294-b3ac-a796f76265ad
keywords:
- IPsec WDK Windows フィルタリングプラットフォーム、WFP コールアウトドライバーとの互換性
- Windows フィルタリングプラットフォームコールアウトドライバー WDK、IPsec 互換性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac7cf2c0144199f14a56afb37e55eb602ad3dec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838142"
---
# <a name="developing-ipsec-compatible-callout-drivers"></a>IPsec と互換性のあるコールアウトドライバーの開発


### <a name="layers-that-are-compatible-with-ipsec"></a>IPsec と互換性のあるレイヤー

Windows Vista および Windows Server 2008 で開始される IPsec の Windows 実装と完全に互換性を持たせるには、次のいずれかの実行時フィルターレイヤーでコールアウトドライバーを登録する必要があります。

<a href="" id="tcp-packet-filtering"></a>TCP パケットフィルター処理  
ストリームレイヤー:

-   FWPS\_レイヤー\_ストリーム\_V4

-   FWPS\_レイヤー\_ストリーム\_V6

<a href="" id="non-tcp-and-non-error-icmp-packet-filtering"></a>非 TCP および非エラーの ICMP パケットフィルター処理  
データグラムデータレイヤー:

-   FWPS\_レイヤー\_データグラム\_データ\_V4

-   FWPS\_レイヤー\_データグラム\_データ\_V6

-   FWPS\_レイヤー\_データグラム\_データ\_V4\_破棄

-   FWPS\_レイヤー\_データグラム\_データ\_V6\_破棄

受信パケットがデータグラムデータレイヤーから挿入される前に再構築する必要がある場合を除き、これらのデータ層に登録されているコールアウトドライバーは IPsec と互換性があります。

### <a name="layers-that-are-incompatible-with-ipsec"></a>IPsec と互換性のないレイヤー

これらのレイヤーは IPsec トラフィックがまだ暗号化解除または検証されていないため、ネットワーク層と転送層は IPsec と互換性がありません。 IPsec ポリシーは、ネットワーク層の分類操作の後に発生するトランスポート層で適用されます。

次の実行時フィルターレイヤーは IPsec と互換性がありません。これは、Windows での IPsec の処理が次の層の下に発生するためです。

FWPS\_レイヤー\_受信\_IPPACKET\_V4

FWPS\_レイヤー\_受信\_IPPACKET\_V6

FWPS\_レイヤー\_受信\_IPPACKET\_V4\_破棄

FWPS\_レイヤー\_受信\_IPPACKET\_V6\_破棄

FWPS\_レイヤー\_送信\_IPPACKET\_V4

FWPS\_レイヤー\_送信\_IPPACKET\_V6

FWPS\_レイヤー\_送信\_IPPACKET\_V4\_破棄

FWPS\_レイヤー\_送信\_IPPACKET\_V6\_破棄

### <a name="special-considerations-for-transport-layers"></a>トランスポート層に関する特別な考慮事項

トランスポート層 (FWPS\_レイヤー\_*XXX*\_Transport\_V4 または \_V6) に登録されているコールアウトドライバーを IPsec と互換性のあるものにするには、次のガイドラインに従ってください。

1.  [ALE で受信/受け入れレイヤーを承認する] (**Fwps\_レイヤー\_ale\_認証\_受信\_V4**または**FWPS\_レイヤー\_ale\_AUTH\_RECV\_を承認します。** トランスポート層 (FWPS\_レイヤー\_*XXX*\_transport\_V4 または \_V6) に加えて\_V6 も受け入れます。\_

2.  Windows IPsec の内部処理による干渉を防ぐために、 **FWPM\_サブレイヤー\_UNIVERSAL**と比べて重みが低いサブレイヤーにコールアウトを登録します。 [**FwpmSubLayerEnum0**](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerenum0)関数を使用して、サブレイヤーの重みを検索します。 この関数の詳細については、Microsoft Windows SDK の[Windows フィルタリングプラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=90220)のドキュメントを参照してください。

3.  Ale 分類を必要とする着信トランスポートパケットは、ALE 承認受信/受け入れレイヤー (**Fwps\_レイヤー\_ale\_AUTH\_receive\_accept\_V4**または FWPS\_レイヤーで検査する必要があり **@no__ t9_ ALE\_AUTH\_RECV\_\_V6 に受け入れ**ます)。\_ このようなパケットは、受信トランスポート層から許可されている必要があります。 Windows Vista Service Pack 1 (SP1) および Windows Server 2008 以降では、 **Fwps の\_メタデータ\_フィールド\_ALE\_分類\_必要な**メタデータフラグを使用して、着信パケットを示すかどうかを判断します。**FWPM\_レイヤー\_ale\_AUTH\_RECV\_accept\_V4**および**FWPM\_LAYER\_ale\_AUTH\_RECV\_V6**フィルターレイヤーを受け入れます。\_ このメタデータフラグは、Windows Vista で使用されていた **\_ALE\_分類条件フラグを必要と\_\_フラグの\_条件**を置き換えます。

4.  Windows IPsec の内部処理による干渉を防ぐため、IPsec トラフィックがまだ detunneled されていない場合は、トランスポート層で IPsec トンネルモードトラフィックをインターセプトしないでください。 次のコード例は、このようなパケットをバイパスする方法を示しています。
    ```C++
    FWPS_PACKET_LIST_INFORMATION0 packetInfo = {0};
    FwpsGetPacketListSecurityInformation0(
     layerData,
        FWPS_PACKET_LIST_INFORMATION_QUERY_IPSEC |
        FWPS_PACKET_LIST_INFORMATION_QUERY_INBOUND,
        &packetInfo
        );

    if (packetInfo.ipsecInformation.inbound.isTunnelMode &&
        !packetInfo.ipsecInformation.inbound.isDeTunneled)
    {
     classifyOut->actionType = FWP_ACTION_PERMIT;
     goto Exit;
    }
    ```

5.  IPsec で保護されたパケットの暗号化が解除され、トランスポート層で検証されると、AH/ESP ヘッダーは IP ヘッダーに残ります。 このようなパケットを TCP/IP スタックに再挿入に戻す必要がある場合は、IP ヘッダーを再構築して AH/ESP ヘッダーを削除する必要があります。 Windows Vista SP1 および Windows Server 2008 以降では、パケットを複製し、 *Headerincludeheadersize*パラメーターが IP ヘッダーサイズに設定されている[**FwpsConstructIpHeaderForTransportPacket0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0)関数を呼び出すことで、これを行うことができます。複製されたパケットの。

6.  ALE 受信/受け入れレイヤーでは、コールアウトは IPsec で保護されたトラフィックを検出できます。これを行うには、ipsec で保護されている **\_条件\_フラグ\_\_ipsec\_セキュリティで保護**されたフラグが設定されていることを確認します トランスポート層では、コールアウトは[**FwpsGetPacketListSecurityInformation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsgetpacketlistsecurityinformation0)関数を呼び出して、 **FWPS\_PACKET\_LIST\_INFORMATION0**フラグがに設定されているかどうかを確認することにより、 *IPsec で保護されたトラフィックを検出できます。queryFlags*パラメーター。

### <a name="working-with-ipsec-esp-packets"></a>IPsec ESP パケットの使用

エンジンは、復号化されたカプセル化セキュリティペイロード (ESP) パケットを示すときに、それを切り捨てて、末尾の ESP データを除外します。 エンジンがこのようなパケットを処理する方法により、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造内の MDL データに正しいパケット長が反映されません。 [**Net\_buffer\_data\_length**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-data-length)マクロを使用して、 **net\_バッファー**構造のデータ長を取得することで、正しい長さを取得できます。

 

 





