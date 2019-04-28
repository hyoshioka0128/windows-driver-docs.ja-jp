---
title: 管理フィルター レイヤー識別子
description: このセクションでは、レイヤーの識別子をフィルター処理の管理について説明します。
ms.assetid: 3287d763-9d73-4bf3-8a32-81acb27f0d36
keywords:
- ネットワーク ドライバーをフィルタ リング層識別子の管理
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: a97d54fdbf5f0b2f9ff8d51b5821e6b280bcac6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365778"
---
# <a name="management-filtering-layer-identifiers"></a>管理フィルター レイヤー識別子

管理のフィルタ リング層識別子は通常、ユーザー モード アプリケーションとは、128 ビット サイズでは、GUID によって表される各によって使用されます。 これらの識別子の定義は次のとおりです。

> [!NOTE]
> レイヤーの識別子の末尾に V4 および V6 サフィックスは、レイヤーは、IPv4 ネットワーク スタックまたは IPv6 のネットワーク スタックに配置されているかどうかを示します。

| フィルタ リング層識別子の管理 | レイヤーの説明をフィルター処理 |
| --- | --- |
| <p>FWPM_LAYER_INBOUND_IPPACKET_V4</p><p>FWPM_LAYER_INBOUND_IPPACKET_V6</p> | 受信パケットの IP ヘッダーが解析された後にだけこのフィルタ リング レイヤーが受信パス内にあるが、処理は任意の IP ヘッダーの前に配置します。 IPsec の暗号化解除または再構築が発生していません。 |
| <p>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</p><p>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</p> | このフィルター処理レイヤーは、ネットワーク層で破棄された受信パケットを処理するための受信パスにあります。 |
| <p>FWPM_LAYER_OUTBOUND_IPPACKET_V4</p><p>FWPM_LAYER_OUTBOUND_IPPACKET_V6</p> | このフィルター処理レイヤーは断片化の送信パケットを評価する前に、送信パスにあります。 すべての IP ヘッダーの処理が完了し、すべての拡張機能ヘッダーが存在します。 すべての IPsec 認証と暗号化が既に発生しました。 |
| <p>FWPM_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p><p>FWPM_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p> | このフィルター処理レイヤーは、ネットワーク層で破棄された送信パケットを処理するため、送信パスにあります。 |
| <p>FWPM_LAYER_IPFORWARD_V4</p><p>FWPM_LAYER_IPFORWARD_V6</p> | このフィルター処理レイヤーは受信パケットが転送先となる時点で、転送パスにあります。 |
| <p>FWPM_LAYER_IPFORWARD_V4_DISCARD</p><p>FWPM_LAYER_IPFORWARD_V6_DISCARD</p> | このフィルター処理レイヤーは、上位層で破棄された転送されたパケットを処理するため、転送パスにあります。 |
| <p>FWPM_LAYER_INBOUND_TRANSPORT_V4</p><p>FWPM_LAYER_INBOUND_TRANSPORT_V6</p> | このフィルター処理レイヤーは処理を行う任意のトランスポート層の前に受信したパケットのヘッダーが、トランスポート層でネットワーク スタックによって解析された後だけに受信パスにあります。 |
| <p>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p><p>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p> | このフィルター処理レイヤーは、トランスポート層で破棄された受信パケットを処理するための受信パスにあります。 |
| <p>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</p><p>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</p> | <p>処理のため、ネットワーク層に送信されたパケットが渡されましたが、任意のネットワークの前にレイヤーの処理を行う直後後、送信パス このフィルター処理レイヤーにあります。</p><p>このフィルター処理レイヤーはサード パーティのトランスポートまたは生パケットとして送信されるすべてのパケットがこのレイヤーでフィルター処理されるように、トランスポート層の下部の代わりに、ネットワーク層の一番上にあります。</p> |
| <p>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p><p>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p> | このフィルター処理レイヤーは、トランスポート層で破棄された送信パケットを処理するため、送信パスにあります。 |
| <p>FWPM_LAYER_STREAM_V4</p><p>FWPM_LAYER_STREAM_V6</p> | このフィルター処理レイヤーは、ストリームのデータ パスにあります。 このレイヤーは、ネットワーク ストリームごとにデータを処理できます。 ストリーム レイヤーでは、ネットワーク データは、双方向です。 |
| <p>FWPM_LAYER_STREAM_V4_DISCARD</p><p>FWPM_LAYER_STREAM_V6_DISCARD</p> | このフィルター処理レイヤーは、将来使用するために予約されています。 |
| <p>FWPM_LAYER_DATAGRAM_DATA_V4</p><p>FWPM_LAYER_DATAGRAM_DATA_V6</p> | このフィルター処理レイヤーは、データグラム データ パスにあります。 このレイヤーあたりデータグラム単位でネットワーク データを処理をできます。 データグラム レイヤーでは、ネットワーク データは、双方向です。 |
| <p>FWPM_LAYER_DATAGRAM_DATA_V4_DISCARD</p><p>FWPM_LAYER_DATAGRAM_DATA_V6_DISCARD</p> | このフィルター処理レイヤーは、破棄されたデータグラムを処理するため、データグラム データ パスにあります。 |
| <p>FWPM_LAYER_INBOUND_ICMP_ERROR_V4</p><p>FWPM_LAYER_INBOUND_ICMP_ERROR_V6</p> | このフィルター処理レイヤーは、トランスポート プロトコルを受信した ICMP メッセージを処理するための受信パスにあります。 |
| <p>FWPM_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPM_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p> | このフィルター処理レイヤーは破棄された受信処理の ICMP メッセージの受信パスにあります。 |
| <p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4</p><p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6</p> | このフィルター処理レイヤーは、トランスポート プロトコルの ICMP メッセージの送信処理のため、送信パスにあります。 |
| <p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p> | このフィルター処理レイヤーは破棄された ICMP メッセージの送信処理のため、送信パスにあります。 |
| <p>FWPM_LAYER_ALE_AUTH_CONNECT_V4</p><p>FWPM_LAYER_ALE_AUTH_CONNECT_V6</p> | このフィルター処理レイヤーは、接続送信 TCP 接続の要求として送信される最初のパケットに基づく非 TCP トラフィックの送信を承認、承認するためできます。 |
| <p>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p><p>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p> | このフィルター処理レイヤーでは、接続の破棄された出力方向の非 TCP トラフィックの承認を処理するほか、破棄された TCP 接続の送信要求の処理をできるようにします。 |
| <p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</p><p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</p> | このフィルター処理レイヤーは、TCP 接続が確立された場合または非 TCP トラフィックが承認されたときの通知できます。 |
| <p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p><p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p> | このフィルター処理の層は、非 TCP トラフィックが、フローが確立されているレイヤーで破棄されたフローが確立されているレイヤーで確立された TCP 接続が破棄されたときにだけでなく承認されると処理によりできます。 |
| <p>FWPM_LAYER_ALE_AUTH_LISTEN_V4</p><p>FWPM_LAYER_ALE_AUTH_LISTEN_V6</p> | このフィルター処理レイヤーにより、TCP リッスン要求を承認するためです。 |
| <p>FWPM_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p><p>FWPM_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p> | このフィルター処理レイヤーは、処理によって、TCP が破棄された要求をリッスンできます。 |
| <p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p><p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p> | このフィルター処理レイヤーでは、最初に受信したパケットに基づく受信 TCP 以外のトラフィックの承認と、着信 TCP 接続では、要求を受け入れるよう承認をできるようにします。 |
| <p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p><p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p> | このフィルター処理レイヤーは、処理が破棄された受信非 TCP トラフィックの承認を処理すると、破棄された受信 TCP 接続要求を受け入れるようにできます。 |
| <p>FWPM_LAYER_ALE_AUTH_ROUTE_V4</p><p>FWPM_LAYER_ALE_AUTH_ROUTE_V6</p> | このフィルター処理レイヤーは検査およびバインドのルートとパスのパラメーターをフィルター処理するため、接続要求。 |
| <p>FWPM_LAYER_ALE_ENDPOINT_CLOSURE_V4</p><p>FWPM_LAYER_ALE_ENDPOINT_CLOSURE_V6</p> | このフィルター処理レイヤーは、ALE_AUTH_CONNECT または ALE_AUTH_RECV_ACCEPT 層のいずれかでコールアウト ドライバーによって割り当てられたリソースを解放する機会として使用されます。 |
| <p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p><p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p> | このフィルタ リング層であるトランスポート ポートの割り当て、バインド要求、無作為検出モードの要求、および raw モード要求を承認するため。 |
| <p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p><p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p> | このフィルター処理レイヤーにより処理のため、次の項目を破棄する: ポートの割り当てをトランスポート、要求、無作為検出モードの要求、および raw モードの要求にバインドします。 |
| <p>FWPM_LAYER_ALE_RESOURCE_RELEASE_V4</p><p>FWPM_LAYER_ALE_RESOURCE_RELEASE_V6</p> | このフィルター処理レイヤーは、ALE_RESOURCE_ASSIGNMENT 層のいずれかでコールアウト ドライバーによって割り当てられたリソースを解放する機会として使用されます。 |
| <p>FWPM_LAYER_IPSEC_KM_DEMUX_V4</p><p>FWPM_LAYER_IPSEC_KM_DEMUX_V6</p> | このフィルター処理レイヤーを使用して、ローカル システムが、発信側では、キー モジュールが呼び出されるを決定します。 これは、ユーザー モードのフィルタ リング層です。 |
| <p>FWPM_LAYER_IPSEC_V4</p><p>FWPM_LAYER_IPSEC_V6</p> | このフィルター処理レイヤーには、クイック モード セキュリティ アソシエーションをネゴシエートするときに、クイック モード ポリシー情報を検索するキー モジュールができます。 これは、ユーザー モードのフィルタ リング層です。 |
| <p>FWPM_LAYER_IKEEXT_V4</p><p>FWPM_LAYER_IKEEXT_V6</p> | このフィルター処理レイヤーには、IKE ができ、メイン モード セキュリティ アソシエーションをネゴシエートするときに、メイン モード ポリシー情報を検索する IP モジュールの認証。 これは、ユーザー モードのフィルタ リング層です。 |
| FWPM_LAYER_RPC_UM | このフィルター処理レイヤーは、ユーザー モードで使用できる RPC データ フィールドを検査できます。 これは、ユーザー モードのフィルタ リング層です。 |
| FWPM_LAYER_RPC_EPMAP | このフィルタ リング層であるエンドポイントの解決中にユーザー モードで使用できる RPC データ フィールドを検査できます。 これは、ユーザー モードのフィルタ リング層です。 |
| FWPM_LAYER_RPC_EP_ADD | このフィルタ リング層である新しいエンドポイントが追加されたときに、ユーザー モードで使用できる RPC データ フィールドを検査できます。 これは、ユーザー モードのフィルタ リング層です。 |
| FWPM_LAYER_RPC_PROXY_CONN | このフィルター処理レイヤーは、RpcProxy 接続要求を検査できます。 これは、ユーザー モードのフィルタ リング層です。 |
| FWPM_LAYER_RPC_PROXY_IF | このフィルター処理レイヤーは、RpcProxy 接続に使用されるインターフェイスを検査できます。 これは、ユーザー モードのフィルタ リング層です。 |
| FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET | このフィルター処理レイヤーは、受信 (NDIS プロトコル ドライバー) を下位の層で MAC フレーム データを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |
| FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET | このフィルター処理レイヤー (NDIS プロトコル ドライバー) する上位層の送信で MAC フレーム データを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |
| FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE | このフィルター処理レイヤーは、受信 (NDIS ミニポート ドライバー) を下位の層で MAC フレーム データを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |
| FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE | このフィルター処理レイヤーは、送信 (NDIS ミニポート ドライバー) を下位の層で MAC フレーム データを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |
| FWPM_LAYER_INGRESS_VSWITCH_ETHERNET | このフィルター処理レイヤーは、HYPER-V 拡張可能スイッチのイングレス 802.3 データを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |
| FWPM_LAYER_EGRESS_VSWITCH_ETHERNET | このフィルター処理レイヤーは、HYPER-V 拡張可能スイッチのエグレス 802.3 データを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |
| <p>FWPM_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPM_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p> | このフィルター処理レイヤーは、HYPER-V 拡張可能スイッチの受信トランスポートのデータを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |
| <p>FWPM_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPM_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p> | このフィルター処理レイヤーは、HYPER-V 拡張可能スイッチのエグレス トランスポートのデータを検査できます。 **注意**:以降では、Windows 8 のみ利用できます。 |

