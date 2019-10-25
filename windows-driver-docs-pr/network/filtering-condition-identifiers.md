---
title: フィルター条件識別子
description: このセクションでは、フィルター条件の識別子について説明します。
ms.assetid: 53321aea-6406-426a-a541-2626faad2232
keywords:
- 条件識別子ネットワークドライバーのフィルター処理
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ea3f46571580afaff1a6e6c4f2ad5b8af392495
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833763"
---
# <a name="filtering-condition-identifiers"></a>フィルター条件識別子

フィルター条件識別子は、それぞれ GUID で表されます。 これらの識別子については、次の表で説明します。

<table>
<tr>
<th>フィルター条件識別子</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙される到着ネットワークインターフェイスのインデックス。</p>
<p>WFP は、この条件に一致する到着インターフェイスを使用します。 到着インターフェイスは、弱いホストまたは転送が実行される前に、パケットがネットワークから受信する IP スタックを入力する前に見られる最初のインターフェイスです。</p>
<p>この条件は、本質的に受信条件であるため、再認証のために非対称です。 これは、応答の送信パケットで受信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 到着インターフェイス条件の場合、インターフェイス条件の次ホップクラスは、送信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_TYPE</p>
</td>
<td>
<p>インターネット割り当て番号機関 (IANA) によって定義された、到着ネットワークインターフェイスの種類。 詳細については、「 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType の定義</a>」を参照してください。</p>
<p>WFP は、この条件に一致する到着インターフェイスを使用します。 到着インターフェイスは、弱いホストまたは転送が実行される前に、パケットがネットワークから受信する IP スタックを入力する前に見られる最初のインターフェイスです。</p>
<p>この条件は、本質的に受信条件であるため、再認証のために非対称です。 これは、応答の送信パケットで受信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 到着インターフェイス条件の場合、インターフェイス条件の次ホップクラスは、送信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_TUNNEL_TYPE</p>
</td>
<td>
<p><a href="https://docs.microsoft.com/windows/desktop/api/iptypes/ns-iptypes-_ip_adapter_addresses_lh"><b>IP_ADAPTER_ADDRESSES</b></a>構造体の iftype メンバーが IF_TYPE_TUNNEL の場合にトンネルによって使用されるカプセル化メソッド。 トンネルの種類は IANA によって定義されます。 詳細については、「 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType の定義</a>」および Windows SDK <a href="https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper">IP ヘルパー</a>のドキュメントを参照してください。</p>
<p>WFP は、この条件に一致する到着インターフェイスを使用します。 到着インターフェイスは、弱いホストまたは転送が実行される前に、パケットがネットワークから受信する IP スタックを入力する前に見られる最初のインターフェイスです。</p>
<p>この条件は、本質的に受信条件であるため、再認証のために非対称です。 これは、応答の送信パケットで受信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 到着インターフェイス条件の場合、インターフェイス条件の次ホップクラスは、送信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_ARRIVAL_INTERFACE</p>
</td>
<td>
<p>到着 IP アドレスに関連付けられているネットワークインターフェイスの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid"><b>LUID</b></a> 。</p>
<p>WFP は、この条件に一致する到着インターフェイスを使用します。 到着インターフェイスは、弱いホストまたは転送が実行される前に、パケットがネットワークから受信する IP スタックを入力する前に見られる最初のインターフェイスです。</p>
<p>この条件は、本質的に受信条件であるため、再認証のために非対称です。 これは、応答の送信パケットで受信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 到着インターフェイス条件の場合、インターフェイス条件の次ホップクラスは、送信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙される到着ネットワークインターフェイスのインデックス。</p>
<p>WFP は、次ホップインターフェイスを使用して、この状態を照合します。 次ホップインターフェイスは、脆弱なホストまたは転送が実行された後、パケットがネットワークに対して IP スタックを送信する前に見られる最後のインターフェイスです。</p>
<p>この条件は、本質的に送信条件であるため、再認証のために非対称です。 これは、応答の受信パケットで送信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 次ホップインターフェイス条件の場合、インターフェイス条件の到着クラスは、受信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_TYPE</p>
</td>
<td>
<p>インターネット割り当て番号機関 (IANA) によって定義された、到着ネットワークインターフェイスの種類。 詳細については、「 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType の定義</a>」を参照してください。</p>
<p>WFP は、次ホップインターフェイスを使用して、この状態を照合します。 次ホップインターフェイスは、脆弱なホストまたは転送が実行された後、パケットがネットワークに対して IP スタックを送信する前に見られる最後のインターフェイスです。</p>
<p>この条件は、本質的に送信条件であるため、再認証のために非対称です。 これは、応答の受信パケットで送信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 次ホップインターフェイス条件の場合、インターフェイス条件の到着クラスは、受信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_TUNNEL_TYPE</p>
</td>
<td>
<p><a href="https://docs.microsoft.com/windows/desktop/api/iptypes/ns-iptypes-_ip_adapter_addresses_lh"><b>IP_ADAPTER_ADDRESSES</b></a>構造体の<b>IFTYPE</b>メンバーが IF_TYPE_TUNNEL の場合にトンネルによって使用されるカプセル化メソッド。 トンネルの種類は IANA によって定義されます。 詳細については、「 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType の定義</a>」および Windows SDK <a href="https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper">IP ヘルパー</a>のドキュメントを参照してください。</p>
<p>WFP は、次ホップインターフェイスを使用して、この状態を照合します。 次ホップインターフェイスは、脆弱なホストまたは転送が実行された後、パケットがネットワークに対して IP スタックを送信する前に見られる最後のインターフェイスです。</p>
<p>この条件は、本質的に送信条件であるため、再認証のために非対称です。 これは、応答の受信パケットで送信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 次ホップインターフェイス条件の場合、インターフェイス条件の到着クラスは、受信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_NEXTHOP_INTERFACE</p>
</td>
<td>
<p>到着 IP アドレスに関連付けられているネットワークインターフェイスの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid"><b>LUID</b></a>。</p>
<p>WFP は、次ホップインターフェイスを使用して、この状態を照合します。 次ホップインターフェイスは、脆弱なホストまたは転送が実行された後、パケットがネットワークに対して IP スタックを送信する前に見られる最後のインターフェイスです。</p>
<p>この条件は、本質的に送信条件であるため、再認証のために非対称です。 これは、応答の受信パケットで送信接続を再承認するときに、WFP がこの状態で空の値を使用することを意味します。</p>
<p>再認証を処理するには、2番目のフィルターを使用する必要があります。 この2番目のフィルターでは、空の値を許可またはブロックできます。また、このような状況に対して有効な値を持つ別の条件を使用することもできます。 次ホップインターフェイス条件の場合、インターフェイス条件の到着クラスは、受信パケットに有効なインターフェイスを持ちます。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、およびそれ以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
</td>
<td>
<p>ローカル IP アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
</td>
<td>
<p>リモート IP アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_SOURCE_ADDRESS</p>
</td>
<td>
<p>転送されたパケットの発信元 IP アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS</p>
</td>
<td>
<p>転送されたパケットの宛先 IP アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>ローカル IP アドレスの種類。 使用可能な条件値は次のとおりです。</p>
<p>
<dl>
<dd>
NlatUnspecified

</dd>
<dd>
NlatUnicast

</dd>
<dd>
NlatAnycast

</dd>
<dd>
NlatMulticast

</dd>
<dd>
NlatBroadcast
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE</p>
</td>
<td>
<p>宛先 IP アドレスの種類。 使用可能な条件値は次のとおりです。</p>
<p>
<dl>
<dd>
NlatUnspecified

</dd>
<dd>
NlatUnicast

</dd>
<dd>
NlatAnycast

</dd>
<dd>
NlatMulticast

</dd>
<dd>
NlatBroadcast
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
</td>
<td>
<p>ローカル IP アドレスに関連付けられているネットワークインターフェイスの LUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_FORWARD_INTERFACE</p>
</td>
<td>
<p>転送されるパケットが送信されるネットワークインターフェイスの LUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
</td>
<td>
<p><a href="https://tools.ietf.org/html/rfc1700">RFC 1700</a>で指定されている IP プロトコル番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
</td>
<td>
<p>ローカルトランスポートプロトコルのポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
</td>
<td>
<p>リモートトランスポートプロトコルのポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ICMP_TYPE</p>
</td>
<td>
<p><a href="https://tools.ietf.org/html/rfc792">RFC 792</a>で指定されているように、ICMP の種類フィールド。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ICMP_CODE</p>
</td>
<td>
<p><a href="https://tools.ietf.org/html/rfc792">RFC 792</a>で指定されているように、ICMP コードフィールド。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>ICMP パケットに埋め込まれているローカル IP アドレスの種類。 使用可能な条件値は次のとおりです。</p>
<p>
<dl>
<dd>
NlatUnspecified

</dd>
<dd>
NlatUnicast

</dd>
<dd>
NlatAnycast

</dd>
<dd>
NlatMulticast

</dd>
<dd>
NlatBroadcast
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_ADDRESS</p>
</td>
<td>
<p>ICMP パケットに埋め込まれているリモート IP アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_PROTOCOL</p>
</td>
<td>
<p><a href="https://tools.ietf.org/html/rfc1700">RFC 1700</a>で指定されているように、ICMP パケットに埋め込まれている IP プロトコル番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_PORT</p>
</td>
<td>
<p>ICMP パケットに埋め込まれているローカルトランスポートプロトコルのポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_PORT</p>
</td>
<td>
<p>ICMP パケットに埋め込まれているリモートトランスポートプロトコルのポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_FLAGS</p>
</td>
<td>
<p>フィルター条件フラグの組み合わせのビットごとの OR。 使用可能なフラグの詳細については、「<a href="filtering-condition-flags.md">フィルター条件フラグ</a>」を参照してください。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DIRECTION</p>
</td>
<td>
<p>データグラムトラフィックまたはデータフローの方向。</p>
<p>使用可能な条件値は次のとおりです。</p>
<p>
<dl>
<dd>
FWP_DIRECTION_INBOUND

</dd>
<dd>
FWP_DIRECTION_OUTBOUND
</dd>
</dl>
</p>
<p>データグラムデータレイヤーおよびストリームパケットレイヤーでは、この条件によってパケットの方向が指定されます。</p>
<p>ストリームレイヤーと ALE フローによって確立されたレイヤーでは、この条件は接続の方向を指定します (たとえば、ローカルアプリケーションが接続を開始すると、受信パケットの FWPM_CONDITION_DIRECTION が FWP_DIRECTION_OUTBOUND に設定されます)。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙されたネットワークインターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
</td>
<td>
<p>ネットワークインターフェイスのバスの種類。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙された論理ネットワークインターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙された、転送されたパケットのソースネットワークインターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙された、転送されたパケットのソース論理ネットワークインターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙された、転送されたパケットの宛先ネットワークインターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワークスタックによって列挙された、転送されたパケットの宛先論理ネットワークインターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_APP_ID</p>
</td>
<td>
<p>アプリケーションの完全パス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_USER_ID</p>
</td>
<td>
<p>ローカルユーザーの id。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_REMOTE_USER_ID</p>
</td>
<td>
<p>リモートユーザーの id。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_REMOTE_MACHINE_ID</p>
</td>
<td>
<p>リモートコンピューターの id。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PROMISCUOUS_MODE</p>
</td>
<td>
<p>許可または拒否される未加工のソケットモード。 使用可能な条件値は次のとおりです。</p>
<p>
<dl>
<dd>
SIO_RCVALL

</dd>
<dd>
SIO_RCVALL_IGMPMCAST

</dd>
<dd>
SIO_RCVALL_MCAST

</dd>
</dl>
</p>
<p>これらの未加工ソケットモードの詳細については、Microsoft Windows SDK のドキュメントの「 <a href="https://docs.microsoft.com/windows/desktop/api/winsock2/nf-winsock2-wsaioctl"><b>Wsaioctl</b></a> 」を参照してください。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_SIO_FIREWALL_SYSTEM_PORT</p>
</td>
<td>
<p>内部使用のために予約済みです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_NAP_CONTEXT</p>
</td>
<td>
<p>内部使用のために予約済みです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_REMOTE_USER_TOKEN</p>
</td>
<td>
<p>リモートユーザーの id。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_IF_UUID</p>
</td>
<td>
<p>RPC インターフェイスの UUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_IF_VERSION</p>
</td>
<td>
<p>RPC インターフェイスのバージョン。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RCP_IF_FLAG</p>
</td>
<td>
<p>内部使用のために予約済みです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DCOM_APP_ID</p>
</td>
<td>
<p>COM アプリケーションの id。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IMAGE_NAME</p>
</td>
<td>
<p>アプリケーションの名前。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_PROTOCOL</p>
</td>
<td>
<p>RPC プロトコル。 使用可能な条件値は次のとおりです。</p>
<p>
<dl>
<dd>
RPC_PROTSEQ_TCP

</dd>
<dd>
RPC_PROTSEQ_HTTP

</dd>
<dd>
RPC_PROTSEQ_NMP
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_AUTH_TYPE</p>
</td>
<td>
<p>認証サービスの種類。 認証サービスの種類の詳細については、Windows SDK のドキュメントの RPC セクションにある<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-service-constants"><b>認証サービス定数</b></a>に関するセクションを参照してください。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_AUTH_LEVEL</p>
</td>
<td>
<p>認証サービスレベル。 認証サービスレベルの詳細については、Windows SDK のドキュメントの RPC セクションにある<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-level-constants"><b>認証レベルの定数</b></a>に関するセクションを参照してください。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_ENCRYPT_ALGORITHM</p>
</td>
<td>
<p>証明書ベースのセキュリティサービスプロバイダーインターフェイス (SSPI) 暗号化アルゴリズム。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_KEY_SIZE</p>
</td>
<td>
<p>証明書ベースのセキュリティサービスプロバイダーインターフェイス (SSPI) 暗号化キーのサイズ。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V4</p>
</td>
<td>
<p>ローカル IPv4 アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V6</p>
</td>
<td>
<p>ローカル IPv6 アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_PIPE</p>
</td>
<td>
<p>リモートの名前付きパイプの名前。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V4</p>
</td>
<td>
<p>リモート IPv4 アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V6</p>
</td>
<td>
<p>リモート IPv6 アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_PROCESS_WITH_RPC_IF_UUID</p>
</td>
<td>
<p>RPC インターフェイスを持つプロセスの UUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_EP_VALUE</p>
</td>
<td>
<p>内部使用のために予約済みです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_EP_FLAGS</p>
</td>
<td>
<p>内部使用のために予約済みです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_TOKEN</p>
</td>
<td>
<p>RpcProxy を使用する場合のクライアントの id。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_SERVER_NAME</p>
</td>
<td>
<p>RpcProxy を使用する場合の RPC サーバーの名前。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_SERVER_PORT</p>
</td>
<td>
<p>RpcProxy を使用する場合の RPC サーバー上のポート。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_PROXY_AUTH_TYPE</p>
</td>
<td>
<p>RPC プロキシ認証サービスの種類。 認証サービスの種類の詳細については、Windows SDK のドキュメントの RPC セクションにある<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-service-constants"><b>認証サービス定数</b></a>に関するセクションを参照してください。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
<td>
<p>トンネルによって使用されるカプセル化メソッド。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_KEY_LENGTH</p>
</td>
<td>
<p>クライアント証明書の secure socket layer (SSL) キー長。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_OID</p>
</td>
<td>
<p>クライアント証明書のオブジェクト識別子 (OID)。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_MAC_ADDRESS
</p>
</td>
<td>
<p>送信または受信ネットワークインターフェイスの物理アドレス。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_LOCAL_ADDRESS
</p>
</td>
<td>
<p>ローカルネットワークインターフェイスの物理アドレス。
受信トラフィックの場合、これはフレーム内の宛先 MAC アドレスです。
送信トラフィックの場合、これはフレームの送信元 MAC アドレスです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS</p>
</td>
<td>
<p>リモートネットワークインターフェイスの物理アドレス。
受信トラフィックの場合、これはフレーム内のソース MAC アドレスです。
送信トラフィックの場合、これはフレームの宛先 MAC アドレスです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ETHER_TYPE</p>
</td>
<td>
<p>MAC フレームに示されている型。
この値は、IPv4 トラフィックの場合は0x800、IPv6 トラフィックの場合は0x86DD、ARP トラフィックの場合は0x806 です。
使用可能なすべての値は、ntddndis で NDIS_ETH_TYPE_Xxx として定義されています。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VLAN_ID</p>
</td>
<td>
<p>イーサネットスナップヘッダー内の VLAN の識別子。
フレームがイーサネット II の場合、この値は0です。
</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PORT</p>
</td>
<td>
<p>ミニポートアダプターポートを識別するポート番号。 </p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_MEDIA_TYPE</p>
</td>
<td>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_medium"><b>NDIS_MEDIUM</b></a>列挙値の1つとして指定された NDIS メディアの種類。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PHYSICAL_MEDIA_TYPE</p>
</td>
<td>
<p>NDIS_PHYSICAL_MEDIUM 列挙値の1つとして指定された通信インターフェイスの物理メディアの種類。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_L2_FLAGS</p>
</td>
<td>
<p>MAC レイヤーのフィルター条件フラグの組み合わせのビットごとの OR。 使用可能なフラグの詳細については、「<a href="filtering-condition-l2-flags.md">フィルター条件 L2 フラグ</a>」を参照してください。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>ローカル MAC アドレスのリンクの種類。 これは、FwpmTypes. h の<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>列挙で定義されている値の1つです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS_TYPE</p>
</td>
<td>
<p>リモート MAC アドレスのリンクの種類。 これは、FwpmTypes. h の<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>列挙で定義されている値の1つです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE</p>
</td>
<td>
<p>ローカル MAC アドレスに関連付けられているネットワークインターフェイスの LUID。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>AppContainer 制限付きパッケージのセキュリティ識別子 (SID)。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS</p>
</td>
<td>
<p>MAC フレームを作成したネットワークインターフェイスの物理アドレス。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS</p>
</td>
<td>
<p>フレームの送信先となるネットワークインターフェイスの物理アドレス。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS_TYPE</p>
</td>
<td>
<p>フレームを作成したインターフェイスの MAC アドレスのリンクの種類。 これは、FwpmTypes. h の<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>列挙で定義されている値の1つです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS_TYPE</p>
</td>
<td>
<p>フレームの送信先であるインターフェイスの MAC アドレスのリンクの種類。 これは、FwpmTypes. h の<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>列挙で定義されている値の1つです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_SOURCE_PORT</p>
</td>
<td>
<p>トランスポートプロトコルの発信元ポート番号。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_PORT</p>
</td>
<td>
<p>トランスポートプロトコルの宛先ポート番号。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_ID</p>
</td>
<td>
<p>仮想スイッチの GUID。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_NETWORK_TYPE</p>
</td>
<td>
<p>仮想スイッチに関連付けられているネットワークの種類。 これは、FwpTypes. h の<a href="https://docs.microsoft.com/windows/desktop/api/fwptypes/ne-fwptypes-fwp_vswitch_network_type_"><b>FWP_VSWITCH_NETWORK_TYPE</b></a>列挙で定義されている値の1つです。</p>
<div class="alert"><b>メモ</b> Windows <i>8</i>以降のバージョンの windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID</p>
</td>
<td>
<p>フレームを作成した仮想スイッチのインターフェイスの GUID。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_ID</p>
</td>
<td>
<p>フレームの送信先となる仮想スイッチのインターフェイスの GUID。</p>
<div class="alert"><b>メモ</b> Windows <i>8</i>以降のバージョンの windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE</p>
</td>
<td>
<p>フレームを作成した仮想スイッチインターフェイスの型。 これは、Ntddndis の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_nic_switch_type"><b>NDIS_NIC_SWITCH_TYPE</b></a>列挙で定義されている値の1つです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_TYPE</p>
</td>
<td>
<p>フレームの送信先となる仮想スイッチインターフェイスの型。 これは、Ntddndis の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_nic_switch_type"><b>NDIS_NIC_SWITCH_TYPE</b></a>列挙で定義されている値の1つです。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
</td>
<td>
<p>VSwitch ソース仮想マシンの一意の識別子。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_VM_ID</p>
</td>
<td>
<p>VSwitch ターゲット仮想マシンの一意の識別子。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
</td>
<td>
<p>VSwitch ネットワークの一意の識別子。 VLAN_IDs と組み合わせて使用することはできません。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>アプリコンテナーのセキュリティ識別子 (SID)。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_ORIGINAL_APP_ID</p>
</td>
<td>
<p>プロキシ化を変更する前の、アプリケーションの元の完全パス。  プロキシが関係していない場合、これは FWPM_CONDITION_ALE_APP_ID と同じになることに注意してください。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_QM_MODE</p>
</td>
<td>
<p>クイックモード (QM) モード。</p>
<div class="alert"><b>メモ</b> Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
</table>

