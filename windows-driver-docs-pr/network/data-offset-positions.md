---
title: データ オフセット位置
description: このセクションでは、Windows フィルタリングプラットフォームのコールアウトドライバーのデータオフセット位置について説明します。
ms.assetid: cf4656cf-b978-4539-9fff-8f0aa5de1b5e
keywords:
- データオフセット位置ネットワークドライバー
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5585ea707800c47b3f4fc3c3b10e770fcb7eeb37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838162"
---
# <a name="data-offset-positions"></a>データ オフセット位置

フィルターエンジンは、コールアウトドライバーの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数を呼び出すと、*レイヤーデータ*パラメーターの構造体へのポインターを渡します。 パケットデータをフィルター処理するレイヤーの場合、ポインターは[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を参照します。 *Classid*が使用されているフィルター処理レイヤーに応じて、レイヤーデータ * パラメーターには、次のいずれかの構造体へのポインターが渡されます。

- ストリームレイヤーでは、レイヤー*データ*パラメーターに[FWPS_STREAM_CALLOUT_IO_PACKET0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_callout_io_packet0_)構造体へのポインターが含まれています。 この構造体の streamData メンバーには、 [FWPS_STREAM_DATA0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_data0_)構造体へのポインターが含まれています。 

    [FWPS_STREAM_DATA0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_stream_data0_)構造体の**netBufferListChain**メンバーには、 [NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体へのポインターが含まれています。 

- 他のすべてのレイヤーについては、レイヤー*データ*パラメーターに[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体へのポインターが含まれています。

> [!NOTE]
> レイヤー*データ*パラメーターは、フィルター処理されているレイヤーによっては NULL になる場合があります。また、ドライバーの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)に使用される、コールアウト関数が呼び出される条件も異なります。
 
[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体には、 [NET_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体のリンクリストが含まれています。 各**NET_BUFFER**構造の[NET_BUFFER_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)構造内では、 **DataOffset**メンバーはパケットデータ内の特定の位置を指します。 **DataOffset**メンバーが指す位置は、フィルターエンジンがコールアウトドライバーの*classid*関数を呼び出すフィルターレイヤーに依存します。 

各フィルターレイヤーに対して、 **DataOffset**メンバーによって指定されたパケットデータ内の位置は、次のように定義されます。

<table>
<tr>
<th>実行時フィルタリングレイヤー識別子 (Windows Vista 以降)</th>
<th>パケットデータ内の位置</th>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_IPPACKET_V4</p>
<p>FWPS_LAYER_INBOUND_IPPACKET_V6</p>
</td>
<td>
<p>トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_IPPACKET_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p>TCP/IP スタックが処理を停止したオフセット。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V4</p>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V6</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p>
<p>FWPS_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p>TCP/IP スタックが処理を停止したオフセット。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPFORWARD_V4</p>
<p>FWPS_LAYER_IPFORWARD_V6</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPFORWARD_V4_DISCARD</p>
<p>FWPS_LAYER_IPFORWARD_V6_DISCARD</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V4</p>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V6</p>
</td>
<td>
<p>データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4</p>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6</p>
</td>
<td>
<p>トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_V4</p>
<p>FWPS_LAYER_STREAM_V6</p>
</td>
<td>
<p>データの先頭。</p>
<div class="alert">パケットデータ内の位置に IP、IPv6、およびトランスポートヘッダーが含まれていない   に<b>注意</b>してください。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_V4_DISCARD</p>
<p>FWPS_LAYER_STREAM_V6_DISCARD</p>
</td>
<td>
<p>データの先頭。</p>
<div class="alert">パケットデータ内の位置に IP、IPv6、またはトランスポートヘッダーが含まれていない   に<b>注意</b>してください。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6</p>
</td>
<td>
<p>受信データグラムの場合: データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
<p>送信データグラムの場合: トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p>
</td>
<td>
<p>受信データグラムの場合: データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
<p>送信データグラムの場合: トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4</p>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6</p>
</td>
<td>
<p>内部 IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p>内部 IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4</p>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6</p>
</td>
<td>
<p>ICMP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p>
<p>FWPS_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p>ICMP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V4</p>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p>
</td>
<td>
<p>受信パケットの方向: データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
<p>送信パケットの方向: トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p>
</td>
<td>
<p>受信パケットの方向: データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
<p>送信パケットの方向: トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6</p>
</td>
<td>
<p>TCP 以外のトラフィックの場合: トランスポートヘッダーの先頭。</p>
<p>TCP トラフィックの場合: 該当なし。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p>
</td>
<td>
<p>TCP 以外のトラフィックの場合: トランスポートヘッダーの先頭。</p>
<p>TCP トラフィックの場合: 該当なし。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6</p>
</td>
<td>
<p>受信パケットの方向: データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
<p>送信パケットの方向: トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p>
</td>
<td>
<p>受信パケットの方向: データの先頭。</p>
<div class="alert"><b>注:</b> tcp/ip スタックの icmp ソケットで受信した受信パケットについては、icmp ヘッダーの先頭がオフセットとして  ます。</div>
<div> </div>
<p>送信パケットの方向: トランスポートヘッダーの先頭。
      </p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPSEC_KM_DEMUX_V4</p>
<p>FWPS_LAYER_IPSEC_KM_DEMUX_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IPSEC_V4</p>
<p>FWPS_LAYER_IPSEC_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_IKEEXT_V4</p>
<p>FWPS_LAYER_IKEEXT_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_UM</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_EPMAP</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_EP_ADD</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_PROXY_CONN</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_RPC_PROXY_IF</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<th>実行時フィルタリングレイヤー識別子 (Windows 7 以降)</th>
<th>パケットデータ内の位置</th>
</tr>
<tr>
<td>
<p>FWPS_LAYER_NAME_RESOLUTION_CACHE_V4</p>
<p>
FWPS_LAYER_NAME_RESOLUTION_CACHE_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V4</p>
<p>FWPS_LAYER_ALE_RESOURCE_RELEASE_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V4</p>
<p>FWPS_LAYER_ALE_ENDPOINT_CLOSURE_V6</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V4</p>
<p>FWPS_LAYER_ALE_CONNECT_REDIRECT_V6</p>
</td>
<td>
<p>適用できません。</p>
<div class="alert"><b>メモ</b> これらのフィルターレイヤーでは、レイヤー<i><em>データ</em></i>パラメーターに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0"><b>FWPS_CONNECT_REQUEST0</b></a>構造体へのポインターが含まれています。 この構造体は、パケットデータを記述する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list"><b>NET_BUFFER_LIST</b></a>構造体を参照しません。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_BIND_REDIRECT_V4</p>
<p>FWPS_LAYER_ALE_BIND_REDIRECT_V6</p>
</td>
<td>
<p>適用できません。</p>
<div class="alert"><b>メモ</b> これらのフィルターレイヤーでは、レイヤー<i><em>データ</em></i>パラメーターに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0"><b>FWPS_BIND_REQUEST0</b></a>構造体へのポインターが含まれています。 この構造体は、パケットデータを記述する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list"><b>NET_BUFFER_LIST</b></a>構造体を参照しません。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_PACKET_V4</p>
<p>FWPS_LAYER_STREAM_PACKET_V6</p>
</td>
<td>
<p>受信パケットの方向: データの先頭。</p>
<p>送信パケットの方向: トランスポートヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_KM_AUTHORIZATION</p>
</td>
<td>
<p>適用できません。</p>
</td>
</tr>
<tr>
<th>実行時フィルタリングレイヤー識別子 (Windows 8 以降)</th>
<th>パケットデータ内の位置</th>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_MAC_FRAME_ETHERNET</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_MAC_FRAME_ETHERNET</p>
</td>
<td>
<p>MAC ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_MAC_FRAME_NATIVE</p>
</td>
<td>
<p>MAC ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_MAC_FRAME_NATIVE</p>
</td>
<td>
<p>MAC ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p>イーサネットヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p>イーサネットヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p>IP ヘッダーの先頭。</p>
</td>
</tr>
</table>

