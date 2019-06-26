---
title: フィルター条件フラグ
description: このセクションでは、フィルター処理条件フラグについて説明します。
ms.assetid: a2493fc5-614f-47df-a818-cdec06dc9f4a
keywords:
- ネットワーク ドライバーをフィルター処理条件フラグ
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8ddf1285144d5cedf1f2503708cd9248eb7a7768
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353351"
---
# <a name="filtering-condition-flags"></a>フィルター条件フラグ

フィルター条件のフラグは、各ビット フィールドで表されます。 これらのフラグの定義は次のとおりです。

> [!NOTE]
> このトピックでには、カーネル モード WFP コールアウト ドライバーのフィルター条件のフラグが含まれています。 フィルター選択については、ユーザー モードとカーネル モードの間で共有されているフラグを条件またはここに記載されていないフラグに関する情報を探している場合は、次を参照してください、[フィルタ リング条件フラグ](https://docs.microsoft.com/windows/desktop/FWP/filtering-condition-flags-)Windows SDK のトピック。ドキュメントです。

<table>
<tr>
<th>条件のフラグをフィルター処理</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_LOOPBACK</p>
<p>0x00000001</p>
</td>
<td>
<p>ネットワーク トラフィックがループバック トラフィックであることを示します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_IPSEC_SECURED</p>
<p>0x00000002</p>
</td>
<td>
<p>ネットワーク トラフィックが IPsec によって保護されていることを示します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_REAUTHORIZE</p>
<p>0x00000004</p>
</td>
<td>
<p>(新しい接続) ではなく、ポリシーの変更を示します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
<p>このフラグは、Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows で次のフィルター処理レイヤーで該当するもです。<dl>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V6</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_WILDCARD_BIND</p>
<p>0x00000008</p>
</td>
<td>
<p>ローカル ネットワーク アドレスにバインドする場合、アプリケーションがワイルドカード アドレスを指定することを示します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_RAW_ENDPOINT</p>
<p>0x00000010</p>
</td>
<td>
<p>トラフィックの送受信は、ローカル エンドポイントが、生のエンドポイントであることを示します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V4_DISCARD</dd>
<dd>FWPM_LAYER_DATAGRAM_DATA_V6_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
<p>このフラグは、Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V6</dd>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_BIND_REDIRECT_V6</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_FRAGMENT</p>
<p>0x00000020</p>
</td>
<td>
<p>示します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list"> <b>NET_BUFFER_LIST</b> </a>コールアウト ドライバーに渡された構造体は、IP パケットのフラグメント。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_FRAGMENT_GROUP</p>
<p>0x00000040</p>
</td>
<td>
<p>示します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list"> <b>NET_BUFFER_LIST</b> </a>コールアウト ドライバーに渡された構造体には、パケットのフラグメントのリンク リストがについて説明します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_IPSEC_NATT_RECLASSIFY</p>
<p>0x00000080</p>
</td>
<td>
<p>このフラグは、NAT トラバーサル (UDP ポート 4500) パケットが示されたときに設定されます。  カプセル化解除が発生した場合、カプセル化されたパケットから情報を使用して再分類のフラグが設定されます。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_REQUIRES_ALE_CLASSIFY</p>
<p>0x00000100</p>
</td>
<td>
<p>パケットがまだに達していないこと、ALE 受信受け入れるレイヤー (FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4 または FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6) の接続状態を追跡することを示します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_IMPLICIT_BIND</p>
<p>0x00000200</p>
</td>
<td>
<p>ソケットを明示的にバインドしていないことを示します。 送信者の呼び出しは、最初の呼び出し元のバインドせずに送信、Windows ソケットは、暗黙的なバインドを実行します。<div class="alert"><b>注</b>  このフラグは、Windows Server 2008 および Windows Vista でのみサポートされます。 以降の Windows バージョンでは非推奨とされます。</div>
<div> </div>
</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_REASSEMBLED</p>
<p>0x00000400</p>
</td>
<td>
<p>フラグメントのグループからパケットが再構成されていることを示します。</p>
<p>このフラグは、Windows Server 2008、Windows Vista Service Pack 1 (SP1)、以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</dd>
<dd>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_NAME_APP_SPECIFIED</p>
<p>0x00004000</p>
</td>
<td>
<p>接続するアプリケーションが予期しているピア コンピューターの名前がなどの関数を呼び出すことによって取得されていることを示します<a href="https://docs.microsoft.com/windows/desktop/api/ws2tcpip/nf-ws2tcpip-wsasetsocketpeertargetname"> <b>WSASetSocketPeerTargetName</b> </a>キャッシュを使用してではなく、ヒューリスティックです。</p>
<p>このフラグは、Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_PROMISCUOUS</p>
<p>0x00008000</p>
</td>
<td>
<p>将来使用するために予約されています。</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_AUTH_FW</p>
<p>0x00010000</p>
</td>
<td>
<p>パケットが認証済みファイアウォール ポリシーと一致していることを示します。 ファイアウォール ルールの「セキュリティで保護された場合は、接続を許可する」オプションに一致する接続だけでは、このフラグが設定があります。 詳細については、次を参照してください。<a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753463(v=ws.10)">ファイアウォールのバイパスの認証を有効にする方法</a>します。</p>
<p>このフラグは、Windows Server 2008、Windows Vista SP1 と以降のバージョンの Windows で次のフィルター処理レイヤーで該当するもです。<dl>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
</dl>
</p>
<p>このフラグは、Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows で次のフィルター処理レイヤーで該当するもです。<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_RECLASSIFY</p>
<p>0x00020000</p>
</td>
<td>
<p>場合、このフラグが設定、 <a href="https://docs.microsoft.com/windows/desktop/WinSock/ipv6-protection-level">IPV6_PROTECTION_LEVEL</a>既に承認済みのソケットに対してソケット オプションを設定します。</p>
<p>このフラグは、次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</dd>
<dd>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_LISTEN_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_OUTBOUND_PASS_THRU</p>
<p>0x00040000</p>
</td>
<td>
<p>示しますパケットは弱いホストの送信、つまり、このネットワーク インターフェイスを離れることはありませんし、そのため、別のインターフェイスに転送する必要があります。</p>
<p>このフラグは、Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_IPFORWARD_V4</dd>
<dd>FWPM_LAYER_IPFORWARD_V6</dd>
<dd>FWPM_LAYER_IPFORWARD_V4_DISCARD</dd>
<dd>FWPM_LAYER_IPFORWARD_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_INBOUND_PASS_THRU</p>
<p>0x00080000</p>
</td>
<td>
<p>示します、パケットは弱いホストの受信されると、つまり、受信側のネットワーク インターフェイスの宛先はありませんし、そのため、別のインターフェイスに転送する必要があります。</p>
<p>このフラグは、Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_IPFORWARD_V4</dd>
<dd>FWPM_LAYER_IPFORWARD_V6</dd>
<dd>FWPM_LAYER_IPFORWARD_V4_DISCARD</dd>
<dd>FWPM_LAYER_IPFORWARD_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_CONNECTION_REDIRECTED</p>
<p>0x00100000</p>
</td>
<td>
<p>ALE_CONNECT_REDIRECT コールアウト関数によって、接続がリダイレクトされたことを示します。</p>
<p>このフラグは、Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_PROXY_CONNECTION</p>
<p>0x00200000</p>
</td>
<td>
<p>リダイレクトの前のレコードが存在するため、接続されている、プロキシされたことを示します。</p>
<p>このフラグは、Windows Server 2012、Windows 8、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V4</dd>
<dd>FWPM_LAYER_ALE_CONNECT_REDIRECT_V6</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_APPCONTAINER_LOOPBACK</p>
<p>0x00400000</p>
</td>
<td>
<p>トラフィックがしようループバックを使用している、AppContainer からことを示します。</p>
<p>このフラグは、Windows Server 2012、Windows 8、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_NON_APPCONTAINER_LOOPBACK</p>
<p>0x00800000</p>
</td>
<td>
<p>ループバックを使用している標準的なアプリ (AppContainer ではありません) との間のトラフィックは、ということを示します。</p>
<p>このフラグは、Windows Server 2012、Windows 8、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_RESERVED</p>
<p>0x01000000</p>
</td>
<td>
<p>将来使用するために予約されています。</p>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_FLAG_IS_HONORING_POLICY_AUTHORIZE</p>
<p>0x02000000</p>
</td>
<td>
<p>指定したホストへの接続にリダイレクトされたユニバーサル Windows アプリの意図を優先する現在の分類が実行されることを示します。 このような分類と場合、アプリにリダイレクトされたことはありません同じ分類可能なフィールドの値が含まれます。 フラグは、将来の分類が有効なリダイレクトされる宛先に一致する呼び出されることを示します。 場合は、アプリが検査用のプロキシ サービスにリダイレクトされると、また、将来の分類がプロキシ接続で呼び出されます。 コールアウト ドライバーは、この分類を許可する一般にする必要があります。</p>
<p>このフラグは、Windows Server 2012、Windows 8、および以降のバージョンの Windows で次のフィルター処理の層に適用。<dl>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</dd>
<dd>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</dd>
</dl>
</p>
</td>
</tr>
</table>

