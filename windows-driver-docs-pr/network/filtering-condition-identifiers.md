---
title: フィルター条件識別子
description: このセクションでは、フィルター条件の識別子について説明します。
ms.assetid: 53321aea-6406-426a-a541-2626faad2232
keywords:
- ネットワーク ドライバーのフィルター条件の識別子
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14db0a8be2eddeecca89292114554c37e81fd71c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347398"
---
# <a name="filtering-condition-identifiers"></a>フィルター条件識別子

フィルター条件の識別子は、各 GUID で表されます。 これらの識別子は、次の表で説明します。

<table>
<tr>
<th>条件の識別子をフィルター処理</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワーク スタックによって列挙されると、到着ネットワーク インターフェイスのインデックス。</p>
<p>WFP は到着インターフェイスを使用して、この条件に一致します。 到着インターフェイスは、弱いホストまたは転送を実行する前に、ネットワークからの受信が IP スタックに入る前に、パケットに表示される最初のインターフェイスです。</p>
<p>この条件は、受信の条件では本質的に再認証のために、非対称です。 これは、応答の送信パケットの受信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 到着インターフェイスの条件の場合は、送信パケットに有効なインターフェイスがインターフェイスの条件の次ホップ クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_TYPE</p>
</td>
<td>
<p>インターネット割り当て番号機関 (IANA) によって定義されている、到着ネットワーク インターフェイスの型。 詳細については、次を参照してください。 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定義</a>します。</p>
<p>WFP は到着インターフェイスを使用して、この条件に一致します。 到着インターフェイスは、弱いホストまたは転送を実行する前に、ネットワークからの受信が IP スタックに入る前に、パケットに表示される最初のインターフェイスです。</p>
<p>この条件は、受信の条件では本質的に再認証のために、非対称です。 これは、応答の送信パケットの受信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 到着インターフェイスの条件の場合は、送信パケットに有効なインターフェイスがインターフェイスの条件の次ホップ クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_TUNNEL_TYPE</p>
</td>
<td>
<p>場合に、トンネルで使用される、カプセル化メソッドの IfType メンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/aa366058"> <b>IP_ADAPTER_ADDRESSES</b> </a>構造体が IF_TYPE_TUNNEL します。 トンネルの種類は IANA によって定義されます。 詳細については、次を参照してください。 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定義</a>と Windows SDK <a href="https://msdn.microsoft.com/library/windows/hardware/ff557015">IP ヘルパー</a>ドキュメント。</p>
<p>WFP は到着インターフェイスを使用して、この条件に一致します。 到着インターフェイスは、弱いホストまたは転送を実行する前に、ネットワークからの受信が IP スタックに入る前に、パケットに表示される最初のインターフェイスです。</p>
<p>この条件は、受信の条件では本質的に再認証のために、非対称です。 これは、応答の送信パケットの受信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 到着インターフェイスの条件の場合は、送信パケットに有効なインターフェイスがインターフェイスの条件の次ホップ クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_ARRIVAL_INTERFACE</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557080"> <b>LUID</b> </a>到着の IP アドレスに関連付けられているネットワーク インターフェイス。</p>
<p>WFP は到着インターフェイスを使用して、この条件に一致します。 到着インターフェイスは、弱いホストまたは転送を実行する前に、ネットワークからの受信が IP スタックに入る前に、パケットに表示される最初のインターフェイスです。</p>
<p>この条件は、受信の条件では本質的に再認証のために、非対称です。 これは、応答の送信パケットの受信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 到着インターフェイスの条件の場合は、送信パケットに有効なインターフェイスがインターフェイスの条件の次ホップ クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワーク スタックによって列挙されると、到着ネットワーク インターフェイスのインデックス。</p>
<p>WFP は、この条件と一致するのに次ホップ インターフェイスを使用します。 次ホップ インターフェイスには、弱いホストまたは転送を実行した後、IP スタックのネットワークに対する送信を終了する前に、パケットが表示される最後のインターフェイスです。</p>
<p>この条件は、送信の条件では本質的に再認証のために、非対称です。 これは、応答の受信パケットの送信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 次のホップ インターフェイス条件の場合は、受信パケットの有効なインターフェイスがインターフェイスの条件の到着クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_TYPE</p>
</td>
<td>
<p>インターネット割り当て番号機関 (IANA) によって定義されている、到着ネットワーク インターフェイスの型。 詳細については、次を参照してください。 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定義</a>します。</p>
<p>WFP は、この条件と一致するのに次ホップ インターフェイスを使用します。 次ホップ インターフェイスには、弱いホストまたは転送を実行した後、IP スタックのネットワークに対する送信を終了する前に、パケットが表示される最後のインターフェイスです。</p>
<p>この条件は、送信の条件では本質的に再認証のために、非対称です。 これは、応答の受信パケットの送信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 次のホップ インターフェイス条件の場合は、受信パケットの有効なインターフェイスがインターフェイスの条件の到着クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_TUNNEL_TYPE</p>
</td>
<td>
<p>場合に、トンネルで使用されるカプセル化の方法、 <b>IfType</b>のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/aa366058"> <b>IP_ADAPTER_ADDRESSES</b> </a>構造体が IF_TYPE_TUNNEL します。 トンネルの種類は IANA によって定義されます。 詳細については、次を参照してください。 <a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定義</a>と Windows SDK <a href="https://msdn.microsoft.com/library/windows/hardware/ff557015">IP ヘルパー</a>ドキュメント。</p>
<p>WFP は、この条件と一致するのに次ホップ インターフェイスを使用します。 次ホップ インターフェイスには、弱いホストまたは転送を実行した後、IP スタックのネットワークに対する送信を終了する前に、パケットが表示される最後のインターフェイスです。</p>
<p>この条件は、送信の条件では本質的に再認証のために、非対称です。 これは、応答の受信パケットの送信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 次のホップ インターフェイス条件の場合は、受信パケットの有効なインターフェイスがインターフェイスの条件の到着クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_NEXTHOP_INTERFACE</p>
</td>
<td>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557080"> <b>LUID</b></a>到着の IP アドレスに関連付けられているネットワーク インターフェイス。</p>
<p>WFP は、この条件と一致するのに次ホップ インターフェイスを使用します。 次ホップ インターフェイスには、弱いホストまたは転送を実行した後、IP スタックのネットワークに対する送信を終了する前に、パケットが表示される最後のインターフェイスです。</p>
<p>この条件は、送信の条件では本質的に再認証のために、非対称です。 これは、応答の受信パケットの送信接続を再するときに、WFP がこの条件で空の値を使用することを意味します。</p>
<p>2 番目のフィルターを再認証を処理するために使用する必要があります。 この 2 番目のフィルターを許可または空の値をブロックするかをこのような状況の有効な値を持つ別の条件を使用します。 次のホップ インターフェイス条件の場合は、受信パケットの有効なインターフェイスがインターフェイスの条件の到着クラスになります。</p>
<div class="alert"><b>注:</b><br/>Windows Server 2008 R2、Windows 7、および以降のバージョンの Windows でのみ使用できます。
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
<p>転送されたパケットのソース IP アドレス。</p>
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
<p>ローカル IP アドレスの種類。 可能な条件の値は次のとおりです。</p>
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
<p>送信先の IP アドレスの種類。 可能な条件の値は次のとおりです。</p>
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
<p>ローカル IP アドレスに関連付けられているネットワーク インターフェイスの LUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_FORWARD_INTERFACE</p>
</td>
<td>
<p>転送されるパケット送信になっているネットワーク インターフェイスの LUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
</td>
<td>
<p>指定されている、IP プロトコル番号<a href="http://tools.ietf.org/html/rfc1700">RFC 1700</a>します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
</td>
<td>
<p>ローカル トランスポート プロトコルのポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
</td>
<td>
<p>リモートのトランスポート プロトコルのポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ICMP_TYPE</p>
</td>
<td>
<p>ICMP [種類] フィールドで指定されている<a href="http://tools.ietf.org/html/rfc792">RFC 792</a>します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ICMP_CODE</p>
</td>
<td>
<p>指定されている、ICMP コード フィールド<a href="http://tools.ietf.org/html/rfc792">RFC 792</a>します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>ICMP パケットに埋め込まれているローカル IP アドレス型。 可能な条件の値は次のとおりです。</p>
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
<p>ICMP パケットに埋め込まれているリモートの IP アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_PROTOCOL</p>
</td>
<td>
<p>IP プロトコル番号で指定されている、ICMP パケットに埋め込まれている<a href="http://tools.ietf.org/html/rfc1700">RFC 1700</a>します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_PORT</p>
</td>
<td>
<p>ICMP パケットに埋め込まれているローカル トランスポート プロトコル ポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_PORT</p>
</td>
<td>
<p>ICMP パケットに埋め込まれているリモートのトランスポート プロトコル ポート番号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_FLAGS</p>
</td>
<td>
<p>フィルター条件のフラグの組み合わせのビット演算 OR。 可能なフラグについては、次を参照してください。<a href="filtering-condition-flags.md">フィルタ リング条件フラグ</a>します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DIRECTION</p>
</td>
<td>
<p>データグラム トラフィックまたはデータ フローの方向。</p>
<p>可能な条件の値は次のとおりです。</p>
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
<p>データグラム データ レイヤー、およびストリーム パケットのレイヤーでは、この条件は、パケットの方向を指定します。</p>
<p>ストリーム レイヤーと ALE フローが確立されているレイヤーでは、この条件は、(たとえば、着信パケットの場合、接続が設定 FWP_DIRECTION_OUTBOUND FWPM_CONDITION_DIRECTION ローカル アプリケーション開始時に) 接続の方向を指定します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワーク スタックで列挙されている、ネットワーク インターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
</td>
<td>
<p>ネットワーク インターフェイスのバスの種類。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワーク スタックで列挙されている、論理ネットワーク インターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_INTERFACE_INDEX</p>
</td>
<td>
<p>転送されたパケットの場合、ネットワーク スタックによって列挙されたソース ネットワーク インターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>転送されたパケットの場合、ネットワーク スタックによって列挙されたソースの論理ネットワーク インターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワーク スタックによって列挙として、転送されたパケットの宛先のネットワーク インターフェイスのインデックス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>ネットワーク スタックによって列挙として、転送されたパケットの送信先の論理ネットワーク インターフェイスのインデックス。</p>
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
<p>ローカル ユーザーの id です。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_REMOTE_USER_ID</p>
</td>
<td>
<p>リモート ユーザーの id です。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_REMOTE_MACHINE_ID</p>
</td>
<td>
<p>リモート コンピューターの id です。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PROMISCUOUS_MODE</p>
</td>
<td>
<p>Raw ソケット モードの許可または拒否です。 可能な条件の値は次のとおりです。</p>
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
<p>これらの raw ソケット モードについては、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ms741621"> <b>WSAIoctl</b> </a> 、Microsoft Windows SDK ドキュメント。</p>
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
<p>リモート ユーザーの id です。</p>
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
<p>COM アプリケーションの id です。</p>
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
<p>RPC プロトコル。 可能な条件の値は次のとおりです。</p>
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
<p>認証サービスの種類。 認証サービスの種類に関する詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/aa373556"><b>認証サービス定数</b></a> Windows SDK のドキュメントの RPC のセクションでします。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_AUTH_LEVEL</p>
</td>
<td>
<p>認証サービスのレベル。 認証サービス レベルの詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/aa373553"><b>認証レベルの定数</b></a> Windows SDK のドキュメントの RPC のセクションでします。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_ENCRYPT_ALGORITHM</p>
</td>
<td>
<p>証明書ベースのセキュリティ サービス プロバイダー インターフェイス (SSPI) 暗号化アルゴリズム。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_KEY_SIZE</p>
</td>
<td>
<p>証明書ベースのセキュリティ サービス プロバイダー インターフェイス (SSPI) の暗号化キー サイズ。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V4</p>
</td>
<td>
<p>ローカルの IPv4 アドレスです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V6</p>
</td>
<td>
<p>ローカルの IPv6 アドレス。</p>
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
<p>リモートの IPv4 アドレスです。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V6</p>
</td>
<td>
<p>リモートの IPv6 アドレス。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_PROCESS_WITH_RPC_IF_UUID</p>
</td>
<td>
<p>RPC インターフェイスを使用して、プロセスの UUID。</p>
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
<p>RpcProxy を使用する場合、クライアントの id です。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_SERVER_NAME</p>
</td>
<td>
<p>RpcProxy を使用する場合は、RPC サーバーの名前。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_SERVER_PORT</p>
</td>
<td>
<p>RpcProxy を使用する場合は、RPC サーバー上のポート。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_PROXY_AUTH_TYPE</p>
</td>
<td>
<p>RPC プロキシ認証サービスの種類。 認証サービスの種類に関する詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/aa373556"><b>認証サービス定数</b></a> Windows SDK のドキュメントの RPC のセクションでします。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
<td>
<p>カプセル化メソッドは、トンネルで使用します。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_KEY_LENGTH</p>
</td>
<td>
<p>クライアント証明書でセキュリティで保護されたソケット レイヤー (SSL) キーの長さ</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_OID</p>
</td>
<td>
<p>クライアント証明書にオブジェクト識別子 (OID)。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_MAC_ADDRESS
</p>
</td>
<td>
<p>送信または受信ネットワーク インターフェイスの物理アドレス。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_LOCAL_ADDRESS
</p>
</td>
<td>
<p>ローカル ネットワーク インターフェイスの物理アドレス。
受信トラフィックの宛先 MAC アドレス フレームです。
送信トラフィックのソースのフレームの MAC アドレスになります。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS</p>
</td>
<td>
<p>リモートのネットワーク インターフェイスの物理アドレス。
着信トラフィックのソース MAC アドレスをフレームになります。
送信トラフィックのフレームの宛先 MAC アドレスになります。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ETHER_TYPE</p>
</td>
<td>
<p>MAC のフレームで、型が示されます。
この値は、IPv4 トラフィックは、0x800 IPv6 トラフィックの 0x86DD または 0x806 ARP トラフィック用です。
すべての可能な値は、ntddndis.h で NDIS_ETH_TYPE_Xxx として定義されます。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VLAN_ID</p>
</td>
<td>
<p>イーサネット スナップ ヘッダーで VLAN の識別子。
フレームがイーサネット II の場合は、この値は 0 です。
</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PORT</p>
</td>
<td>
<p>ミニポート アダプターのポートを識別するポート番号。 </p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_MEDIA_TYPE</p>
</td>
<td>
<p>いずれかとして指定する NDIS メディアの種類、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff565910"> <b>NDIS_MEDIUM</b> </a>列挙値。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PHYSICAL_MEDIA_TYPE</p>
</td>
<td>
<p>NDIS_PHYSICAL_MEDIUM 列挙値の 1 つとして指定された通信インターフェイスの物理メディアの種類。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_L2_FLAGS</p>
</td>
<td>
<p>MAC のレイヤーを条件フラグをフィルター処理の組み合わせのビット演算 OR。 可能なフラグについては、次を参照してください。<a href="filtering-condition-l2-flags.md">フィルタ リング条件 L2 フラグ</a>します。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>ローカルの MAC アドレスのデータ リンクの種類。 これで定義されている値の 1 つ、 <a href="https://msdn.microsoft.com/library/windows/hardware/dd744934"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h で列挙します。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS_TYPE</p>
</td>
<td>
<p>リモートの MAC アドレスのデータ リンクの種類。 これで定義されている値の 1 つ、 <a href="https://msdn.microsoft.com/library/windows/hardware/dd744934"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h で列挙します。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE</p>
</td>
<td>
<p>ローカルの MAC アドレスに関連付けられているネットワーク インターフェイスの LUID。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>AppContainer 制限されているパッケージのセキュリティ識別子 (SID) です。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS</p>
</td>
<td>
<p>MAC のフレームを作成するネットワーク インターフェイスの物理アドレス。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS</p>
</td>
<td>
<p>フレームの宛先のネットワーク インターフェイスの物理アドレス。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS_TYPE</p>
</td>
<td>
<p>フレームを作成するインターフェイスの MAC アドレスのデータ リンクの種類。 これで定義されている値の 1 つ、 <a href="https://msdn.microsoft.com/library/windows/hardware/dd744934"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h で列挙します。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS_TYPE</p>
</td>
<td>
<p>フレームの宛先をインターフェイスの MAC アドレスのデータ リンクの種類。 これで定義されている値の 1 つ、 <a href="https://msdn.microsoft.com/library/windows/hardware/dd744934"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h で列挙します。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_SOURCE_PORT</p>
</td>
<td>
<p>トランスポート プロトコルの発信元ポート番号。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_PORT</p>
</td>
<td>
<p>トランスポート プロトコルの宛先ポート番号。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_ID</p>
</td>
<td>
<p>仮想スイッチの GUID です。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_NETWORK_TYPE</p>
</td>
<td>
<p>仮想スイッチに関連付けられているネットワークの種類。 これで定義されている値の 1 つ、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh447394"> <b>FWP_VSWITCH_NETWORK_TYPE</b> </a> FwpTypes.h で列挙します。</p>
<div class="alert"><b>注</b>でサポートされている<i>Windows 8</i>と以降のバージョンの Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID</p>
</td>
<td>
<p>フレームを作成した仮想スイッチのインターフェイスの GUID です。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_ID</p>
</td>
<td>
<p>仮想インターフェイスの GUID、フレームの宛先に切り替えます。</p>
<div class="alert"><b>注</b>でサポートされている<i>Windows 8</i>と以降のバージョンの Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE</p>
</td>
<td>
<p>フレームを作成した仮想スイッチのインターフェイスの型。 これで定義されている値の 1 つ、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451589"> <b>NDIS_NIC_SWITCH_TYPE</b> </a> Ntddndis.h で列挙します。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_TYPE</p>
</td>
<td>
<p>フレームの宛先が仮想スイッチのインターフェイスの型。 これで定義されている値の 1 つ、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451589"> <b>NDIS_NIC_SWITCH_TYPE</b> </a> Ntddndis.h で列挙します。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
</td>
<td>
<p>VSwitch のソース仮想マシンの一意の識別子。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_VM_ID</p>
</td>
<td>
<p>VSwitch の送信先仮想マシンの一意の識別子。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
</td>
<td>
<p>VSwitch のネットワークの一意識別子。 VLAN_IDs と組み合わせて使用できません。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>アプリケーション コンテナーのセキュリティ識別子 (SID) です。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_ORIGINAL_APP_ID</p>
</td>
<td>
<p>プロキシから変更を加える前に、アプリケーションの元の完全パス。  プロキシ化が含まれていない場合、これは、同じであること、FWPM_CONDITION_ALE_APP_ID としてに注意してください。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_QM_MODE</p>
</td>
<td>
<p>クイック モード (QM) モード。</p>
<div class="alert"><b>注</b>Windows 8、Windows Server 2012、および以降のバージョンの Windows でサポートされています。</div>
<div> </div>
</td>
</tr>
</table>

