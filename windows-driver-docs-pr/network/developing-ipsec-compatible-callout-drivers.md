---
title: IPsec と互換性のあるコールアウト ドライバーの開発
description: IPsec と互換性のあるコールアウト ドライバーの開発
ms.assetid: 5e4fad4e-a790-4294-b3ac-a796f76265ad
keywords:
- IPsec WDK Windows フィルタ リング プラットフォーム、WFP コールアウト ドライバーとの互換性
- Windows Filtering Platform コールアウト ドライバー WDK、IPsec との互換性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4df4238dce5f8e40169e09c891e33fdc42a4ea0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529421"
---
# <a name="developing-ipsec-compatible-callout-drivers"></a>IPsec と互換性のあるコールアウト ドライバーの開発


### <a name="layers-that-are-compatible-with-ipsec"></a>IPsec と互換性があるレイヤー

Windows Vista および Windows Server 2008 で始まる IPsec の Windows 実装と完全に互換性がある、次の実行時のフィルタ リング層のいずれかのコールアウト ドライバーを登録する必要があります。

<a href="" id="tcp-packet-filtering"></a>TCP パケットのフィルター処理  
Stream レイヤー:

-   FWPS\_レイヤー\_ストリーム\_V4

-   FWPS\_レイヤー\_ストリーム\_V6

<a href="" id="non-tcp-and-non-error-icmp-packet-filtering"></a>TCP 以外とエラー以外の ICMP パケットがフィルター処理  
データグラム データ層:

-   FWPS\_レイヤー\_データグラム\_データ\_V4

-   FWPS\_レイヤー\_データグラム\_データ\_V6

-   FWPS\_レイヤー\_データグラム\_データ\_V4\_破棄

-   FWPS\_レイヤー\_データグラム\_データ\_V6\_破棄

場合を除き、データグラム データ層から受け取る挿入される前に、受信パケットを再構築しなければならないときに、これらのデータ層に登録されているコールアウト ドライバーは IPsec との互換性には。

### <a name="layers-that-are-incompatible-with-ipsec"></a>IPsec と互換性があるレイヤー

ネットワークと転送のレイヤーは、IPsec は、これらの層でトラフィックがまだ暗号化を解除または検証のため、IPsec と互換性がないです。 IPsec ポリシーは、ネットワーク層の分類操作後に発生するトランスポート層で適用されます。

次の実行時のフィルター処理レイヤーは、次のレイヤーの下に IPsec の Windows での処理が発生したため、IPsec と互換性がありません。

FWPS\_レイヤー\_受信\_IPPACKET\_V4

FWPS\_レイヤー\_受信\_IPPACKET\_V6

FWPS\_レイヤー\_受信\_IPPACKET\_V4\_破棄

FWPS\_レイヤー\_受信\_IPPACKET\_V6\_破棄

FWPS\_レイヤー\_送信\_IPPACKET\_V4

FWPS\_レイヤー\_送信\_IPPACKET\_V6

FWPS\_レイヤー\_送信\_IPPACKET\_V4\_破棄

FWPS\_レイヤー\_送信\_IPPACKET\_V6\_破棄

### <a name="special-considerations-for-transport-layers"></a>トランスポート層に関する注意事項

トランスポート層に登録されているコールアウト ドライバーを作成する (FWPS\_レイヤー\_*XXX*\_トランスポート\_V4 または\_V6)、IPsec と互換性がある手順に従います。ガイドライン:

1.  登録のコールアウトの ALE で承認レイヤーの表示と同意 (**FWPS\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_V4**または**FWPS\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_V6**) トランスポート レイヤーだけでなく (FWPS\_レイヤー\_ *XXX*\_トランスポート\_V4 または\_V6)。

2.  内部 Windows IPsec 処理への干渉を防ぐためには、登録よりも低い、重みが副層に吹き出し**FWPM\_副層\_ユニバーサル**します。 使用して、 [ **FwpmSubLayerEnum0** ](https://msdn.microsoft.com/library/windows/desktop/aa364211)副層の重量を検索します。 この関数については、次を参照してください。、 [Windows フィルタ リング プラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK のドキュメント。

3.  ALE で ALE 分類を検査する必要がある必要がありますトランスポート パケットを受信承認レイヤーの表示と同意 (**FWPS\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT。\_V4**または**FWPS\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_V6**)。 このようなパケットは、受信トランスポート レイヤーから許可する必要があります。 Windows Vista Service Pack 1 (SP1)、Windows Server 2008 以降、使用して、 **FWPS\_メタデータ\_フィールド\_ALE\_分類\_REQUIRED**メタデータ フラグ着信パケットに指定されるかどうかを判断する、 **FWPM\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_V4**と**FWPM\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_V6**レイヤーをフィルター処理します。 このメタデータ フラグが置き換えられます、 **FWP\_条件\_フラグ\_REQUIRES\_ALE\_分類**Windows Vista で使用されているフラグの条件します。

4.  Windows IPsec の内部処理への干渉を防ぐためは IPsec トラフィックの detunneled がまだない場合にいないトランスポート層での IPsec トンネル モードのトラフィックをインターセプトします。 次のコード例では、このようなパケットをバイパスする方法を示します。
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

5.  IPsec で保護されたパケットが暗号化を解除し、トランスポート層で確認した後、AH または ESP ヘッダーは、IP ヘッダーに残ります。 このようなパケットが TCP/IP スタックに返される場合、AH または ESP ヘッダーを削除する IP ヘッダーをリビルドしてください。 Windows Vista SP1 および Windows Server 2008 以降、これを行う、パケットを複製し、呼び出すことによって、 [ **FwpsConstructIpHeaderForTransportPacket0** ](https://msdn.microsoft.com/library/windows/hardware/ff551154)関数を持つ、 *headerIncludeHeaderSize*パラメーターは、複製されたパケットの IP ヘッダーのサイズに設定します。

6.  ALE 受信受け入れる層でコールアウトをチェックして IPsec で保護されたトラフィックを検出できるかどうか、 **FWP\_条件\_フラグ\_IS\_IPSEC\_セキュリティで保護された**フラグ設定されています。 トランスポート層では、コールアウトは、呼び出すことで IPsec で保護されたトラフィックを検出できる、 [ **FwpsGetPacketListSecurityInformation0** ](https://msdn.microsoft.com/library/windows/hardware/ff551174)関数とチェックするかどうか、 **FWPS\_パケット\_一覧\_INFORMATION0**フラグに設定されて、 *queryFlags*パラメーター。

### <a name="working-with-ipsec-esp-packets"></a>IPsec ESP パケットの使用

エンジンに復号化セキュリティ ペイロード (ESP) パケットのカプセル化することが示されている場合は、ESP の末尾のデータを除外するに切り捨てます。 エンジンが MDL のデータは、このようなパケットを処理する方法により、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体に適切なパケット長は反映されません。 使用して、正しい長さを取得できます、 [ **NET\_バッファー\_データ\_長さ**](https://msdn.microsoft.com/library/windows/hardware/ff568382)のデータ長を取得するマクロ、 **NET\_バッファー**構造体。

 

 





