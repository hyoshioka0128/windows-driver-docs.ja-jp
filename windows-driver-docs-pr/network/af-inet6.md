---
title: AF_INET6
description: AF_INET6
ms.assetid: 58d36a1e-cda2-42aa-9563-96df2f7319b2
ms.date: 08/08/2017
keywords: -Windows Vista 以降の AF_INET6 ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 901d63d6320f09c67376018fbfe0058dca2bf4fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838237"
---
# <a name="af_inet6"></a>AF\_INET6


AF\_INET6 address ファミリは、IPv6 のアドレスファミリです。

### <a name="socket-address-structure"></a>ソケットアドレスの構造

IPv6 トランスポートアドレスは、 [**SOCKADDR\_IN6**](https://docs.microsoft.com/windows/desktop/api/ws2ipdef/ns-ws2ipdef-sockaddr_in6)構造体で指定されます。

### <a name="socket-types"></a>ソケットの種類

IPv6 は、次のソケットの種類をサポートしています。

<a href="" id="sock-stream"></a>SOCK\_ストリーム  
信頼できる接続指向のバイトストリーム通信をサポートします。

<a href="" id="sock-dgram"></a>SOCK\_DGRAM  
信頼性の低いコネクションレスのデータグラム通信をサポートします。

<a href="" id="sock-raw"></a>SOCK\_生  
は、トランスポートプロトコルへの未加工のアクセスをサポートしています。

WSK アプリケーションは、 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)関数または[**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して新しいソケットを作成するときに、ソケットの種類を指定します。

### <a name="protocols"></a>プロトコル

IPPROTO 列挙の次の IPv6 IPPROTO\_*XXX*プロトコル値は wsk ヘッダーファイルで定義されています。

<a href="" id="ipproto-hopopts"></a>IPPROTO\_HOPOPTS  
IPv6 ホップバイホップオプション

<a href="" id="ipproto-icmp"></a>IPPROTO\_ICMP  
インターネット制御メッセージプロトコル

<a href="" id="ipproto-igmp"></a>IPPROTO\_IGMP  
インターネットグループ管理プロトコル

<a href="" id="ipproto-ggp"></a>IPPROTO\_GGP  
ゲートウェイからゲートウェイへのプロトコル

<a href="" id="ipproto-ipv4"></a>IPPROTO\_IPV4  
IPv4 カプセル化

<a href="" id="ipproto-st"></a>IPPROTO\_ST  
ストリームプロトコル

<a href="" id="ipproto-tcp"></a>IPPROTO\_TCP  
伝送制御プロトコル

<a href="" id="ipproto-cbt"></a>IPPROTO\_CBT  
コアベースのツリープロトコル

<a href="" id="ipproto-egp"></a>IPPROTO\_EGP  
外部ゲートウェイプロトコル

<a href="" id="ipproto-igp"></a>IPPROTO\_IGP  
プライベート内部ゲートウェイプロトコル

<a href="" id="ipproto-pup"></a>IPPROTO\_PUP  
PARC ユニバーサルパケットプロトコル

<a href="" id="ipproto-udp"></a>IPPROTO\_UDP  
ユーザーデータグラムプロトコル

<a href="" id="ipproto-idp"></a>IPPROTO\_IDP  
インターネットデータグラムプロトコル

<a href="" id="ipproto-rdp"></a>IPPROTO\_RDP  
Reliable data プロトコル

<a href="" id="ipproto-ipv6"></a>IPPROTO\_IPV6  
IPv6 ヘッダー

<a href="" id="ipproto-routing"></a>IPPROTO\_ルーティング  
IPv6 ルーティングヘッダー

<a href="" id="ipproto-fragment"></a>IPPROTO\_フラグメント  
IPv6 の断片化のヘッダー

<a href="" id="ipproto-esp"></a>IPPROTO\_ESP  
セキュリティペイロードのカプセル化

<a href="" id="ipproto-ah"></a>IPPROTO\_AH  
認証ヘッダー

<a href="" id="ipproto-icmpv6"></a>IPPROTO\_ICMPV6  
IPv6 インターネット制御メッセージプロトコル

<a href="" id="ipproto-none"></a>IPPROTO\_なし  
IPv6 の次のヘッダーなし

<a href="" id="ipproto-dstopts"></a>IPPROTO\_DSTOPTS  
IPv6 送信先オプション

<a href="" id="ipproto-nd"></a>IPPROTO\_ND  
Net disk プロトコル

<a href="" id="ipproto-iclfxbm"></a>IPPROTO\_ICLFXBM  
広域デルファイ法の監視

<a href="" id="ipproto-pim"></a>IPPROTO\_PIM  
プロトコルに依存しないマルチキャスト

<a href="" id="ipproto-pgm"></a>IPPROTO\_PGM  
実用的な汎用マルチキャスト

<a href="" id="ipproto-l2tp"></a>IPPROTO\_L2TP  
レベル2トンネリングプロトコル

<a href="" id="ipproto-sctp"></a>IPPROTO\_SCTP  
ストリーム制御転送プロトコル

<a href="" id="ipproto-raw"></a>IPPROTO\_RAW  
生の IP パケット

未加工のソケットを使用することにより、追加のプロトコルがサポートされます。

WSK アプリケーションは、 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)関数または[**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して新しいソケットを作成するときに、プロトコルを指定します。

また、WSK アプリケーションは、 [**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出してトランスポートプロトコルレベルまたはネットワークプロトコルレベルのソケットオプションを設定または取得するときに、プロトコルを*レベル*パラメーターとして指定します。

### <a name="combinations"></a>組み合わせ

IPv6 でサポートされているソケットの種類とプロトコルの組み合わせは、各 WSK [socket カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)に対して次のようになります。

基本ソケット SOCK\_STREAM + IPPROTO\_TCP SOCK\_DGRAM + IPPROTO\_UDP SOCK\_RAW + IPPROTO\_*Xxx*リスニングソケット SOCK\_STREAM + IPPROTO\_TCP

データグラムソケット SOCK\_DGRAM + IPPROTO\_UDP SOCK\_RAW + IPPROTO\_*Xxx*接続指向ソケット SOCK\_STREAM + IPPROTO\_TCP

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




