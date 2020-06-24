---
title: AF_INET6
description: AF_INET6
ms.assetid: 58d36a1e-cda2-42aa-9563-96df2f7319b2
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの AF_INET6
ms.localizationpriority: medium
ms.openlocfilehash: 142902974f1210337bfb57df62206c1aff404e24
ms.sourcegitcommit: 57b649e59a2be2055413982035d89bc85e3e425d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85133282"
---
# <a name="af_inet6"></a>AF \_ INET6


AF \_ INET6 address ファミリは、IPv6 のアドレスファミリです。

### <a name="socket-address-structure"></a>ソケットアドレスの構造

IPv6 トランスポートアドレスは、 [**SOCKADDR \_ IN6**](https://docs.microsoft.com/windows/win32/api/ws2ipdef/ns-ws2ipdef-sockaddr_in6_lh)構造体で指定されます。

### <a name="socket-types"></a>ソケットの種類

IPv6 は、次のソケットの種類をサポートしています。

<a href="" id="sock-stream"></a>SOCK \_ ストリーム  
信頼できる接続指向のバイトストリーム通信をサポートします。

<a href="" id="sock-dgram"></a>SOCK \_ DGRAM  
信頼性の低いコネクションレスのデータグラム通信をサポートします。

<a href="" id="sock-raw"></a>SOCK \_ 生  
は、トランスポートプロトコルへの未加工のアクセスをサポートしています。

WSK アプリケーションは、 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)関数または[**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して新しいソケットを作成するときに、ソケットの種類を指定します。

### <a name="protocols"></a>プロトコル

IPPROTO 列挙の次の IPv6 IPPROTO \_ *XXX*プロトコル値は wsk ヘッダーファイルで定義されています。

<a href="" id="ipproto-hopopts"></a>IPPROTO \_ HOPOPTS  
IPv6 ホップバイホップオプション

<a href="" id="ipproto-icmp"></a>IPPROTO \_ ICMP  
インターネット制御メッセージプロトコル

<a href="" id="ipproto-igmp"></a>IPPROTO \_ IGMP  
インターネットグループ管理プロトコル

<a href="" id="ipproto-ggp"></a>IPPROTO \_ GGP  
ゲートウェイからゲートウェイへのプロトコル

<a href="" id="ipproto-ipv4"></a>IPPROTO \_ IPV4  
IPv4 カプセル化

<a href="" id="ipproto-st"></a>IPPROTO \_ ST  
ストリームプロトコル

<a href="" id="ipproto-tcp"></a>IPPROTO \_ TCP  
伝送制御プロトコル

<a href="" id="ipproto-cbt"></a>IPPROTO \_ CBT  
コアベースのツリープロトコル

<a href="" id="ipproto-egp"></a>IPPROTO \_ EGP  
外部ゲートウェイプロトコル

<a href="" id="ipproto-igp"></a>IPPROTO \_ IGP  
プライベート内部ゲートウェイプロトコル

<a href="" id="ipproto-pup"></a>IPPROTO \_ PUP  
PARC ユニバーサルパケットプロトコル

<a href="" id="ipproto-udp"></a>IPPROTO \_ UDP  
ユーザーデータグラムプロトコル

<a href="" id="ipproto-idp"></a>IPPROTO \_ IDP  
インターネットデータグラムプロトコル

<a href="" id="ipproto-rdp"></a>IPPROTO \_ RDP  
Reliable data プロトコル

<a href="" id="ipproto-ipv6"></a>IPPROTO \_ IPV6  
IPv6 ヘッダー

<a href="" id="ipproto-routing"></a>IPPROTO \_ ROUTING  
IPv6 ルーティングヘッダー

<a href="" id="ipproto-fragment"></a>IPPROTO \_ フラグメント  
IPv6 の断片化のヘッダー

<a href="" id="ipproto-esp"></a>IPPROTO \_ ESP  
セキュリティペイロードのカプセル化

<a href="" id="ipproto-ah"></a>IPPROTO \_ AH  
認証ヘッダー

<a href="" id="ipproto-icmpv6"></a>IPPROTO \_ ICMPV6  
IPv6 インターネット制御メッセージプロトコル

<a href="" id="ipproto-none"></a>IPPROTO \_ NONE  
IPv6 の次のヘッダーなし

<a href="" id="ipproto-dstopts"></a>IPPROTO \_ DSTOPTS  
IPv6 送信先オプション

<a href="" id="ipproto-nd"></a>IPPROTO \_ ND  
Net disk プロトコル

<a href="" id="ipproto-iclfxbm"></a>IPPROTO \_ ICLFXBM  
広域デルファイ法の監視

<a href="" id="ipproto-pim"></a>IPPROTO \_ PIM  
プロトコルに依存しないマルチキャスト

<a href="" id="ipproto-pgm"></a>IPPROTO \_ PGM  
実用的な汎用マルチキャスト

<a href="" id="ipproto-l2tp"></a>IPPROTO \_ L2TP  
レベル2トンネリングプロトコル

<a href="" id="ipproto-sctp"></a>IPPROTO \_ SCTP  
ストリーム制御転送プロトコル

<a href="" id="ipproto-raw"></a>IPPROTO \_ RAW  
生の IP パケット

未加工のソケットを使用することにより、追加のプロトコルがサポートされます。

WSK アプリケーションは、 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)関数または[**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して新しいソケットを作成するときに、プロトコルを指定します。

また、WSK アプリケーションは、 [**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出してトランスポートプロトコルレベルまたはネットワークプロトコルレベルのソケットオプションを設定または取得するときに、プロトコルを*レベル*パラメーターとして指定します。

### <a name="combinations"></a>組み合わせ

IPv6 でサポートされているソケットの種類とプロトコルの組み合わせは、各 WSK [socket カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)に対して次のようになります。

基本ソケット SOCK \_ ストリーム + ipproto \_ TCP sock \_ DGRAM + ipproto \_ UDP SOCK \_ RAW + IPPROTO \_ *XXX*リスニングソケット SOCK \_ ストリーム + ipproto \_ TCP

データグラムソケット SOCK \_ dgram + ipproto \_ UDP SOCK \_ RAW + ipproto \_ *Xxx*接続指向ソケット SOCK \_ ストリーム + ipproto \_ TCP

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>ヘッダー</p></td>
<td>Ws2def (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




