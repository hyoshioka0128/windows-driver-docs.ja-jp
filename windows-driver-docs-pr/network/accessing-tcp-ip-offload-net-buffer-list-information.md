---
title: TCP/IP オフロード NET_BUFFER_LIST 情報へのアクセス
description: TCP/IP オフロード NET_BUFFER_LIST 情報へのアクセス
ms.assetid: 555c9533-ab3f-43f0-9139-b1de33a6b1a7
keywords:
- TCP/IP は、WDK のネットワークの帯域外のデータをオフロードします。
- WDK TCP/IP トランスポート、WDK TCP/IP offload 帯域外のデータをオフロードします。
- OOB データ WDK TCP/IP の負荷を軽減します。
- NET_BUFFER_LIST
- タスクは、WDK TCP/IP トランスポート、帯域外のデータをオフロードします。
- 接続は、WDK TCP/IP トランスポート、帯域外のデータをオフロードします。
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 48c2eacd25e671b5d43203ecefd8ccf432fa5c67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384423"
---
# <a name="accessing-tcpip-offload-netbufferlist-information"></a>NET TCP/IP にアクセスする負荷を軽減\_バッファー\_情報を一覧表示

NDIS 6.0 以降のバージョンで TCP/IP オフロード アウト オブ バンド (OOB) データを提供する、 **NetBufferListInfo**のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)のリンクされたリストを指定する構造体[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。 **NetBufferListInfo**メンバーは、NET のすべてに共通する情報が含まれている値の配列\_リスト内のバッファーの構造体。

次の識別子を使用して、 [ **NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)設定 TCP/IP のオフロード OOB のデータを取得するマクロ、 **NetBufferListInfo**配列。

<a href="" id="tcpipchecksumnetbufferlistinfo"></a>**TcpIpChecksumNetBufferListInfo**  
ミニポート ドライバーに TCP/IP プロトコルからチェックサム タスクをオフロードで使用されるチェックサム情報を指定します。 指定すると**TcpIpChecksumNetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体 (構造体をポインターではなく)。 この構造体には、1 つの PVOID 値、またはビット フィールドとして、アクセスするチェックサム情報をできるようにする共用体が含まれています。

<a href="" id="ipsecoffloadv1netbufferlistinfo"></a>**IPsecOffloadV1NetBufferListInfo**  
インターネット プロトコル セキュリティ (IPsec) オフロード、ミニポート ドライバーに TCP/IP プロトコルからの IPsec タスク オフロードで使用されている情報を指定します。 指定すると**IPsecOffloadV1NetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)構造体。

<a href="" id="tcplargesendnetbufferlistinfo"></a>**TcpLargeSendNetBufferListInfo**  
ミニポート ドライバーに TCP/IP プロトコルから大きな TCP パケットのセグメント化オフロードで使用される情報を指定します。 指定すると**TcpLargeSendNetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)構造体 (構造体をポインターではなく)。 この構造体には、1 つの PVOID 値、またはビット フィールドとしてアクセスする情報をできるようにする共用体が含まれています。

<a href="" id="ieee8021qnetbufferlistinfo"></a>**Ieee8021QNetBufferListInfo**  
802.1 q を指定します、パケットに関する情報。 指定すると**Ieee8021QNetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、**値**のメンバー、 [ **NDIS\_NET\_バッファー\_一覧\_8021Q\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)構造体。 この構造体には、802.1 p の優先度の仮想 LAN (VLAN) id 情報を指定できます。 802.1p の優先順位情報は、共有メディア 802 ネットワーク パケットの優先順位を確立するために使用されます。

ミニポート ドライバーは、NDIS のサポートを報告する場合\_カプセル化\_IEEE\_802\_3\_P\_AND\_Q\_IN\_OOB カプセル化挿入する必要がありますが、 **Ieee8021QNetBufferListInfo**にデータを大量送信オフロード バージョン 1 (LSOV1) および大量送信オフロード バージョン 2 (LSOV2) イーサネットのパケットです。

<a href="" id="tcpoffloadbytestransferred"></a>**TcpOffloadBytesTransferred**  
TCP chimney で転送されたバイトが送信の負荷を軽減し、受信、または切断操作のデータの数を指定します。

<a href="" id="tcpreceivenopush"></a>**TcpReceiveNoPush**  
プッシュ モードの TCP chimney オフロードを表しますが、要求を受信するブール値を指定します。 場合**TRUE**、受信要求が非プッシュ モードでします。 それ以外の場合、受信要求はプッシュ モードです。

LSOV1、LSOV2、チェックサム、および IPsec オフロードの種類、ミニポート ドライバーが OOB データと、報告されたオフロード機能の種類に基づくタスク オフロードを実行します。 たとえば、プロトコル ドライバーには、IPv4 パケット LSOV1 サービスが必要とする場合、プロトコルのドライバーを提供する各送信要求には情報が含まれますから、 **LsoV1Transmit**内のメンバー、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) OOB データ。 ミニポート ドライバーが、送信要求を行う前の指定のカプセル化の種類、IPv4 をサポートしているプロトコルのドライバーを確認する必要があることに注意してください。

NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報構造体には、最大セグメント サイズ (MSS) が含まれています。 **TcpHeaderOffset**ミニポート ドライバーが IP ヘッダー、IP オプション、または IP 拡張ヘッダーを解析する必要があるないように、メンバーは、TCP ヘッダーの場所を指定します。

NDIS 6.0 と LSOV2 と LSOV1 をサポートする以降のバージョンのミニポート ドライバーを確認する必要があります、**型**のメンバー [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)ドライバー スタックが LSOV2 または LSOV1 を使用して、適切なオフロードを実行する必要があり、かどうかを決定します。

LSOv1 のミニポートする前にドライバーには、LSO を使用して、小さなパケットにセグメント化した大きな TCP パケットの送信が完了すると、ドライバー書き込みますでセグメント化されたパケットで送信された TCP ペイロードのバイト数、 **TcpPayload**NDIS のメンバー\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報。

NDIS ミニポート ドライバー場合\_カプセル化\_IEEE\_802\_3\_P\_AND\_タスク オフロード サービスを実行する機能、ドライバーは、Q フラグ[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) VLAN のヘッダーのバッファーのデータを含む構造体。 受信したデータの場合は、このフラグは、ミニポート ドライバー受信チェックサムの計算を実行し、イーサネットのパケットで VLAN のヘッダーを配置することを示します。

NDIS ミニポート ドライバー場合\_カプセル化\_IEEE\_802\_3\_P\_AND\_Q\_IN\_OOB、機能フラグドライバーは、NET のオフロードを実行できる\_バッファー\_リスト構造で VLAN ヘッダーが含まれる、 **Ieee8021QnetBufferListInfo** OOB データ。 受信チェックサムでオフロード ケース、ミニポートに VLAN ヘッダーの挿入、 **Ieee8021QnetBufferListInfo** OOB データ。

 

 





