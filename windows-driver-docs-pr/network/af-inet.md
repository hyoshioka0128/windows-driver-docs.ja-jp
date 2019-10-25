---
title: AF_INET
description: AF_INET
ms.assetid: 59e12f8d-02eb-413c-bc04-6b9b6e4adde6
ms.date: 08/08/2017
keywords: -Windows Vista 以降の AF_INET ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d4d1293dde037e87d2c5f5c010f7fd911c199314
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835396"
---
# <a name="af_inet"></a>AF\_INET


AF\_INET アドレスファミリは IPv4 のアドレスファミリです。

### <a name="socket-address-structure"></a>ソケットアドレスの構造

IPv4 トランスポートアドレスは、構造[**内の SOCKADDR\_** ](https://docs.microsoft.com/windows/desktop/api/ws2def/ns-ws2def-sockaddr_in)と共に指定されます。

### <a name="socket-types"></a>ソケットの種類

IPv4 では、次のソケットの種類がサポートされています。

<a href="" id="sock-stream"></a>SOCK\_ストリーム  
信頼できる接続指向のバイトストリーム通信をサポートします。

<a href="" id="sock-dgram"></a>SOCK\_DGRAM  
信頼性の低いコネクションレスのデータグラム通信をサポートします。

<a href="" id="sock-raw"></a>SOCK\_生  
は、トランスポートプロトコルへの未加工のアクセスをサポートしています。

WSK アプリケーションは、 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)関数または[**Wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数を呼び出して新しいソケットを作成するときに、ソケットの種類を指定します。

### <a name="protocols"></a>プロトコル

IPPROTO 列挙の次の IPv4 IPPROTO\_*XXX*プロトコル値は wsk ヘッダーファイルで定義されています。

<a href="" id="ipproto-ip"></a>IPPROTO\_IP  
インターネットプロトコルのオプション

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

IPv4 でサポートされているソケットの種類とプロトコルの組み合わせは、各 WSK [socket カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)に対して次のようになります。

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

 

 




