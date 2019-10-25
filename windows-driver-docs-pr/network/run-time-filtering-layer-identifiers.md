---
title: 実行時フィルター レイヤー識別子
description: ここでは、ランタイムフィルターレイヤー識別子について説明します。
ms.assetid: 21c466a3-cdfc-4e94-83d3-1c2c7a58a2ca
keywords:
- 実行時フィルタリングレイヤー識別子ネットワークドライバ
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d98acb6b657525316fab19450fcc875b6c80925
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841993"
---
# <a name="run-time-filtering-layer-identifiers"></a>実行時フィルター レイヤー識別子

実行時のフィルター処理レイヤー識別子は、カーネルモードのコールアウトドライバーによって使用され、それぞれのサイズが64ビットのローカル一意識別子 ([LUID](https://docs.microsoft.com/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid)) で表されます。 これらの識別子は、Fwpsk で定義されている FWPS_BUILTIN_LAYERS 列挙の定数値です。 これらの識別子は次のように定義されます。

> [!NOTE]
> 実行時レイヤー識別子の最後にある V4 および V6 サフィックスは、レイヤーが IPv4 ネットワークスタックと IPv6 ネットワークスタックのどちらにあるかを示します。

| 実行時フィルタリングレイヤー識別子 | フィルターレイヤーの説明 |
| --- | --- |
| <p>FWPS_LAYER_INBOUND_IPPACKET_V4</p><p>FWPS_LAYER_INBOUND_IPPACKET_V6</p> | このフィルターレイヤーは、受信パケットの IP ヘッダーが解析された直後に、IP ヘッダー処理が行われる前に、受信パスに配置されます。 IPsec の暗号化解除または再構築は行われませんでした。 |
| <p>FWPS_LAYER_INBOUND_IPPACKET_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_IPPACKET_V6_DISCARD</p> | このフィルターレイヤーは、ネットワーク層で破棄された受信パケットを処理するための受信パスに配置されます。 |
| <p>FWPS_LAYER_OUTBOUND_IPPACKET_V4</p><p>FWPS_LAYER_OUTBOUND_IPPACKET_V6</p> | このフィルターレイヤーは、送信パケットが断片化のために評価される直前に送信パスに配置されます。 すべての IP ヘッダー処理が完了し、すべての拡張ヘッダーが配置されます。 すべての IPsec 認証と暗号化が既に行われています。 |
| <p>FWPS_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p> | このフィルターレイヤーは、ネットワーク層で破棄された送信パケットを処理するための送信パスに配置されます。 |
| <p>FWPS_LAYER_IPFORWARD_V4</p><p>FWPS_LAYER_IPFORWARD_V6</p> | このフィルターレイヤーは、受信パケットが転送された時点の転送パスに配置されます。 |
| <p>FWPS_LAYER_IPFORWARD_V4_DISCARD</p><p>FWPS_LAYER_IPFORWARD_V6_DISCARD</p> | このフィルターレイヤーは転送パスに配置され、転送レイヤーで破棄された転送パケットを処理します。 |
| <p>FWPS_LAYER_INBOUND_TRANSPORT_V4</p><p>FWPS_LAYER_INBOUND_TRANSPORT_V6</p> | このフィルターレイヤーは、受信パケットのヘッダーがトランスポート層のネットワークスタックによって解析された直後に、トランスポート層の処理が行われる前に受信パスに配置されます。 |
| <p>FWPS_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p> | このフィルターレイヤーは、トランスポート層で破棄された受信パケットを処理するための受信パスに配置されます。 |
| <p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4</p><p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6</p> | <p>このフィルターレイヤーは、送信されたパケットが処理のためにネットワーク層に渡された直後に、ネットワーク層の処理が行われる前に、送信パスに配置されます。</p><p>このフィルターレイヤーは、トランスポート層の下部ではなく、ネットワーク層の一番上に配置されます。これにより、サードパーティのトランスポートまたは未加工のパケットで送信されるすべてのパケットが、このレイヤーでフィルター処理されます。</p> |
| <p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p> | このフィルターレイヤーは、トランスポート層で破棄された送信パケットを処理するための送信パスに配置されます。 |
| <p>FWPS_LAYER_STREAM_V4</p><p>FWPS_LAYER_STREAM_V6</p> | このフィルターレイヤーは、ストリームのデータパスにあります。 このレイヤーを使用すると、ストリームごとにネットワークデータを処理できます。 ストリームレイヤーでは、ネットワークデータは双方向です。 |
| <p>FWPS_LAYER_STREAM_V4_DISCARD</p><p>FWPS_LAYER_STREAM_V6_DISCARD</p> | このフィルターレイヤーは将来使用するために予約されています。 |
| <p>FWPS_LAYER_DATAGRAM_DATA_V4</p><p>FWPS_LAYER_DATAGRAM_DATA_V6</p> | このフィルターレイヤーは、データグラムデータパスにあります。 このレイヤーを使用すると、データグラムごとにネットワークデータを処理できます。 データグラムレイヤーでは、ネットワークデータは双方向です。 |
| <p>FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p><p>FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p> | このフィルターレイヤーは、破棄されたすべてのデータグラムを処理するためのデータグラムデータパスに配置されます。 |
| <p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4</p><p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6</p> | このフィルターレイヤーは、トランスポートプロトコルの受信した ICMP メッセージを処理するための受信パスに配置されます。 |
| <p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p> | このフィルターレイヤーは、破棄された受信 ICMP メッセージを処理するための受信パスに配置されます。 |
| <p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4</p><p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6</p> | このフィルターレイヤーは、トランスポートプロトコルの送信 ICMP メッセージを処理するための送信パスにあります。 |
| <p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p> | このフィルターレイヤーは、破棄された送信 ICMP メッセージを処理するための送信パスにあります。 |
| <p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p><p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p> | このフィルターレイヤーを使用すると、トランスポートポートの割り当て、バインド要求、プロミスカスモード要求、および raw モード要求を承認できます。 |
| <p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p><p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p> | このフィルターレイヤーを使用すると、トランスポートポートの割り当て、バインド要求、無作為検出モードの要求、および raw モードの要求の破棄された項目を処理できます。 |
| <p>FWPS_LAYER_ALE_AUTH_LISTEN_V4</p><p>FWPS_LAYER_ALE_AUTH_LISTEN_V6</p> | このフィルターレイヤーを使用すると、TCP リッスン要求を承認できます。 |
| <p>FWPS_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p> | このフィルターレイヤーを使用すると、破棄された TCP リッスン要求を処理できます。 |
| <p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p><p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p> | このフィルターレイヤーを使用すると、受信した TCP 接続の受け入れ要求を承認したり、受信した最初のパケットに基づいて受信する非 TCP トラフィックを承認したりすることができます。 |
| <p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p> | このフィルターレイヤーを使用すると、破棄された着信 TCP 接続の受け入れ要求を処理することができます。また、破棄された TCP 以外の着信トラフィックに対する承認を処理することもできます。 |
| <p>FWPS_LAYER_ALE_AUTH_CONNECT_V4</p><p>FWPS_LAYER_ALE_AUTH_CONNECT_V6</p> | このフィルターレイヤーを使用すると、送信 TCP 接続に対する接続要求を承認するだけでなく、送信された最初のパケットに基づいて、送信される TCP 以外のトラフィックを承認することができます。 |
| <p>FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p><p>FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p> | このフィルターレイヤーを使用すると、破棄された送信 TCP 接続に対する接続要求を処理したり、破棄された TCP 以外の送信トラフィックに対する承認を処理したりできます。 |
| <p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4</p><p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6</p> | このフィルターレイヤーを使用すると、TCP 接続が確立されたとき、または TCP 以外のトラフィックが承認されたときに通知を受け取ることができます。 |
| <p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p><p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p> | このフィルターレイヤーを使用すると、確立された TCP 接続がフローによって確立されたレイヤーで破棄された場合や、承認された TCP 以外のトラフィックがフローによって確立されたレイヤーで破棄された場合に、処理を行うことができます。 |
| <p>FWPS_LAYER_RESERVED1_V4</p><p>FWPS_LAYER_RESERVED1_V6</p> | このフィルターレイヤーはサポートされていません。 |
| <p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V4</p><p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V6</p> | このフィルターレイヤーを使用すると、システムによって最近解決された名前に対してクエリを実行できます。 |
| <p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V4</p><p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V6</p> | このフィルターレイヤーは、ALE_RESOURCE_ASSIGNMENT の任意のレイヤーで、コールアウトドライバーによって割り当てられたリソースを再利用する機会として使用されます。 |
| <p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V4</p><p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V6</p> | このフィルターレイヤーは、ALE_AUTH_CONNECT または ALE_AUTH_RECV_ACCEPT のいずれかのレイヤーで、コールアウトドライバーによって割り当てられたリソースを再利用する機会として使用されます。 |
| <p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V4</p><p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V6</p> | このフィルターレイヤーを使用すると、接続要求を別の IPV4/IPV6 アドレスと TCP/UDP ポートにリダイレクトすることができます。 |
| <p>FWPS_LAYER_ALE_BIND_REDIRECT_V4</p><p>FWPS_LAYER_ALE_BIND_REDIRECT_V6</p> | このフィルターレイヤーを使用すると、別のローカル IPV4/IPV6 アドレスまたはローカル TCP/UDP ポートにバインド要求をリダイレクトできます。 |
| FWPS_LAYER_INBOUND_MAC_FRAME_ETHERNET | このフィルターレイヤーを使用すると、(NDIS プロトコルドライバーに対する) 受信層で MAC フレームデータを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| FWPS_LAYER_OUTBOUND_MAC_FRAME_ETHERNET | このフィルターレイヤーを使用すると、送信の上限 (NDIS プロトコルドライバー) レイヤーで MAC フレームデータを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| FWPS_LAYER_INBOUND_MAC_FRAME_NATIVE | このフィルターレイヤーを使用すると、受信側 (NDIS ミニポートドライバー) レイヤーに MAC フレームデータを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| FWPS_LAYER_OUTBOUND_MAC_FRAME_NATIVE | このフィルターレイヤーでは、(NDIS ミニポートドライバーに対する) 送信の下位にある MAC フレームデータを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| FWPS_LAYER_INGRESS_VSWITCH_ETHERNET | このフィルターレイヤーを使用すると、Hyper-v 拡張可能スイッチの受信802.3 データを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| FWPS_LAYER_EGRESS_VSWITCH_ETHERNET | このフィルターレイヤーを使用すると、Hyper-v 拡張可能スイッチの送信802.3 データを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| <p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p> | このフィルターレイヤーを使用すると、Hyper-v 拡張可能スイッチの受信トランスポートデータを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| <p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p> | このフィルターレイヤーを使用すると、Hyper-v 拡張可能スイッチの送信トランスポートデータを検査できます。 **注**: Windows 8 以降でのみ使用できます。 |
| <p>FWPS_LAYER_STREAM_PACKET_V4</p><p>FWPS_LAYER_STREAM_PACKET_V6</p> | このフィルターレイヤーを使用すると、ハンドシェイクやフロー制御交換など、TCP パケット単位でネットワークデータを検査できます。 ストリームパケットレイヤーでは、ネットワークデータは双方向です。 |
| <p>FWPS_LAYER_IPSEC_KM_DEMUX_V4</p><p>FWPS_LAYER_IPSEC_KM_DEMUX_V6</p> | このフィルターレイヤーは、ローカルシステムがイニシエーターであるときにどのキーモジュールが呼び出されるかを決定するために使用されます。 これは、ユーザーモードのフィルターレイヤーです。 |
| <p>FWPS_LAYER_IPSEC_V4</p><p>FWPS_LAYER_IPSEC_V6</p> | このフィルターレイヤーを使用すると、クイックモードのセキュリティアソシエーションをネゴシエートするときに、キーモジュールでクイックモードのポリシー情報を検索できます。 これは、ユーザーモードのフィルターレイヤーです。 |
| <p>FWPS_LAYER_IKEEXT_V4</p><p>FWPS_LAYER_IKEEXT_V6</p> | このフィルターレイヤーを使用すると、メインモードのセキュリティアソシエーションをネゴシエートするときに、IKE と認証された IP モジュールがメインモードのポリシー情報を参照できます。 これは、ユーザーモードのフィルターレイヤーです。 |
| FWPS_LAYER_RPC_UM | このフィルターレイヤーを使用すると、ユーザーモードで使用できる RPC データフィールドを調べることができます。 これは、ユーザーモードのフィルターレイヤーです。 |
| FWPS_LAYER_RPC_EPMAP | このフィルターレイヤーを使用すると、エンドポイントの解決中にユーザーモードで使用できる RPC データフィールドを検査できます。 これは、ユーザーモードのフィルターレイヤーです。 |
| FWPS_LAYER_RPC_EP_ADD | このフィルターレイヤーを使用すると、新しいエンドポイントが追加されたときにユーザーモードで使用できる RPC データフィールドを調べることができます。 これは、ユーザーモードのフィルターレイヤーです。 |
| FWPS_LAYER_RPC_PROXY_CONN | このフィルター処理レイヤーでは、RpcProxy 接続要求を検査できます。 これは、ユーザーモードのフィルターレイヤーです。 |
| FWPS_LAYER_RPC_PROXY_IF | このフィルターレイヤーでは、RpcProxy 接続に使用されるインターフェイスを調べることができます。 これは、ユーザーモードのフィルターレイヤーです。 |
| FWPS_LAYER_KM_AUTHORIZATION | このフィルターレイヤーを使用すると、セキュリティアソシエーションの確立を承認できます。 |

各ランタイムレイヤー識別子には、一連の定数値を表す実行時データフィールド識別子が関連付けられています。 これらのデータフィールド識別子は、Fwpsk で FWPS_FIELDS_XXX 列挙として宣言されます。 詳細については、「[データフィールド識別子](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)」を参照してください。

