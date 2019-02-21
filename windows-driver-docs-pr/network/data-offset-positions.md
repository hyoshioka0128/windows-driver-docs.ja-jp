---
title: データのオフセット位置
description: このセクションでは、Windows Filtering Platform コールアウト ドライバーのデータ オフセット位置について説明します。
ms.assetid: cf4656cf-b978-4539-9fff-8f0aa5de1b5e
keywords:
- データのオフセット位置ネットワーク ドライバー
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 568d5f786aef4c385d5637babf6ff9741284d73a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548874"
---
# <a name="data-offset-positions"></a>データのオフセット位置

フィルター エンジンがコールアウト ドライバーを呼び出すときに[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウトの関数に構造体へのポインターを渡しますが、*データ*パラメーター。 パケット データをフィルター処理のレイヤーのポインターの参照を[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 フィルター処理レイヤーによって、 *classifyFn*コールアウト関数が呼び出されると、フィルター エンジンのデータのパラメーターで、次の構造のいずれかにポインターを渡します。

- ストリーム レイヤーについて、*データ*パラメーターにはへのポインターが含まれています、 [FWPS_STREAM_CALLOUT_IO_PACKET0](https://msdn.microsoft.com/library/windows/hardware/ff552417)構造体。 この構造体の streamData メンバーにはへのポインターが含まれています、 [FWPS_STREAM_DATA0](https://msdn.microsoft.com/library/windows/hardware/ff552419)構造体。 

    **NetBufferListChain**のメンバー、 [FWPS_STREAM_DATA0](https://msdn.microsoft.com/library/windows/hardware/ff552419)構造体にはへのポインターが含まれています、 [NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 

- 他のすべてのレイヤー、*データ*パラメーターにはへのポインターが含まれています、 [NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

> [!NOTE]
> *データ*パラメーターに null の場合、フィルター選択されているレイヤーを状況に応じて可能性があります、ドライバーの[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウト関数が呼び出されます。
 
[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造のリンク リストに含まれる[NET_BUFFER](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。 内で、 [NET_BUFFER_DATA](https://msdn.microsoft.com/library/windows/hardware/ff568381)の各構造**NET_BUFFER**構造、 **DataOffset**パケット データ内の特定の位置へのポインターします。 位置を**DataOffset**へのポインターのメンバーは、位置フィルター エンジンを呼び出す、コールアウト ドライバーのフィルター処理レイヤーによって異なります。 *classifyFn*コールアウト関数。 

各フィルターのレイヤーで指定されたパケット データ内の位置の**DataOffset**メンバーが次のように定義されています。

<table>
<tr>
<th>レイヤー (Windows Vista 以降) の識別子の実行時にフィルター処理</th>
<th>パケット データ内の位置</th>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_IPPACKET_V4</p>
<p>FWPS_LAYER_INBOUND_IPPACKET_V6</p>
</td>
<td>
<p>トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_IPPACKET_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p>TCP/IP スタックの場所のオフセットには、処理が停止しました。</p>
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
<p>TCP/IP スタックの場所のオフセットには、処理が停止しました。</p>
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
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
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
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4</p>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6</p>
</td>
<td>
<p>トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPS_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_V4</p>
<p>FWPS_LAYER_STREAM_V6</p>
</td>
<td>
<p>データの先頭。</p>
<div class="alert"><b>注</b>  パケット データ内の位置が含まれていない IP、IPv6、およびトランスポート ヘッダー。</div>
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
<div class="alert"><b>注</b>  パケット データ内の位置が含まれていない IP、IPv6、またはトランスポート ヘッダー。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6</p>
</td>
<td>
<p>受信データグラムは。データの先頭。</p>
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
<div> </div>
<p>発信データグラムは。トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_DATAGRAM_DATA_V4_DISCARD</p>
<p>FWPS_LAYER_DATAGRAM_DATA_V6_DISCARD</p>
</td>
<td>
<p>受信データグラムは。データの先頭。</p>
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
<div> </div>
<p>発信データグラムは。トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4</p>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6</p>
</td>
<td>
<p>内部の IP ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p>
<p>FWPS_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p>内部の IP ヘッダーの先頭。</p>
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
<p>着信パケットの方向を指定します。データの先頭。</p>
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
<div> </div>
<p>発信パケットの方向を指定します。トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p>
</td>
<td>
<p>着信パケットの方向を指定します。データの先頭。</p>
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
<div> </div>
<p>発信パケットの方向を指定します。トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6</p>
</td>
<td>
<p>非 TCP トラフィックの場合。トランスポート ヘッダーの先頭。</p>
<p>TCP トラフィックの場合。適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p>
</td>
<td>
<p>非 TCP トラフィックの場合。トランスポート ヘッダーの先頭。</p>
<p>TCP トラフィックの場合。適用できません。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6</p>
</td>
<td>
<p>着信パケットの方向を指定します。データの先頭。</p>
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
<div> </div>
<p>発信パケットの方向を指定します。トランスポート ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p>
<p>FWPS_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p>
</td>
<td>
<p>着信パケットの方向を指定します。データの先頭。</p>
<div class="alert"><b>注</b>  TCP/IP スタックの ICMP ソケットで受信した受信パケットをオフセットは ICMP ヘッダーの先頭。</div>
<div> </div>
<p>発信パケットの方向を指定します。トランスポート ヘッダーの先頭。
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
<th>レイヤー (Windows 7 以降) の識別子の実行時にフィルター処理</th>
<th>パケット データ内の位置</th>
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
<div class="alert"><b>注</b>これらのレイヤーをフィルター処理、 <i><em>データ</em></i>パラメーターにはへのポインターが含まれています、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551231"> <b>FWPS_CONNECT_REQUEST0</b> </a>構造体。 この構造体を参照していません、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568388"> <b>NET_BUFFER_LIST</b> </a>パケット データを記述する構造体。</div>
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
<div class="alert"><b>注</b>これらのレイヤーをフィルター処理、 <i><em>データ</em></i>パラメーターにはへのポインターが含まれています、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551221"> <b>FWPS_BIND_REQUEST0</b> </a>構造体。 この構造体を参照していません、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568388"> <b>NET_BUFFER_LIST</b> </a>パケット データを記述する構造体。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_STREAM_PACKET_V4</p>
<p>FWPS_LAYER_STREAM_PACKET_V6</p>
</td>
<td>
<p>着信パケットの方向を指定します。データの先頭。</p>
<p>発信パケットの方向を指定します。トランスポート ヘッダーの先頭。</p>
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
<th>レイヤー (Windows 8 以降) の識別子の実行時にフィルター処理</th>
<th>パケット データ内の位置</th>
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
<p>イーサネット ヘッダーの先頭。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_LAYER_EGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p>イーサネット ヘッダーの先頭。</p>
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

