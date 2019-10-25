---
title: TCP/IP オフロード NET_BUFFER_LIST 情報へのアクセス
description: TCP/IP オフロード NET_BUFFER_LIST 情報へのアクセス
ms.assetid: 555c9533-ab3f-43f0-9139-b1de33a6b1a7
keywords:
- TCP/IP オフロード WDK ネットワーク、帯域外データ
- WDK TCP/IP トランスポートのオフロード、帯域外データの WDK TCP/IP オフロード
- OOB データ WDK TCP/IP オフロード
- NET_BUFFER_LIST
- タスクオフロード WDK TCP/IP トランスポート、帯域外データ
- 接続オフロード WDK TCP/IP トランスポート、帯域外データ
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4bb4574033e864b4a2bff593f087e32a89b63f5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838252"
---
# <a name="accessing-tcpip-offload-net_buffer_list-information"></a>TCP/IP オフロード NET\_バッファー\_一覧情報へのアクセス

NDIS バージョン6.0 以降では、net [ **\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**NETBUFFERLISTINFO**メンバーに tcp/ip オフロード帯域外 (OOB) データが提供されます。このデータは、 [**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造のリンクリストを指定します。 **NetBufferListInfo**メンバーは、リスト内のすべての NET\_バッファー構造に共通する情報を含む値の配列です。

次の識別子を[**NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロと共に使用して、 **NETBUFFERLISTINFO**配列の tcp/ip オフロード OOB データを設定して取得します。

<a href="" id="tcpipchecksumnetbufferlistinfo"></a>**TcpIpChecksumNetBufferListInfo**  
チェックサムタスクを TCP/IP プロトコルからミニポートドライバーにオフロードするときに使用するチェックサム情報を指定します。 **TcpIpChecksumNetBufferListInfo**、NET\_BUFFER\_list を指定すると\_情報は[**NDIS\_TCP\_IP\_チェックサム\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体を返します(構造体へのポインターではありません)。 この構造体には、チェックサム情報に1つの PVOID 値またはビットフィールドとしてアクセスできるようにする共用体が含まれています。

<a href="" id="ipsecoffloadv1netbufferlistinfo"></a>**IPsecOffloadV1NetBufferListInfo**  
TCP/IP プロトコルからミニポートドライバーへの IPsec タスクのオフロードに使用されるインターネットプロトコルセキュリティ (IPsec) オフロード情報を指定します。 **IPsecOffloadV1NetBufferListInfo**、NET\_BUFFER\_list を指定すると\_情報は[**NDIS\_IPSEC\_オフロード\_V1\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)を返します。データ.

<a href="" id="tcplargesendnetbufferlistinfo"></a>**TcpLargeSendNetBufferListInfo**  
TCP/IP プロトコルからミニポートドライバーへの、サイズの大きい TCP パケットのセグメント化をオフロードするために使用される情報を指定します。 **TcpLargeSendNetBufferListInfo**、NET\_BUFFER\_list を指定した場合、\_情報は、 [**NDIS\_TCP\_大きい\_送信\_オフロード\_NET\_BUFFER\_list を返し\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)構造体 (構造体へのポインターではありません)。 この構造体には、1つの PVOID 値またはビットフィールドとして情報にアクセスできるようにする共用体が含まれています。

<a href="" id="ieee8021qnetbufferlistinfo"></a>**Ieee8021QNetBufferListInfo**  
パケットに関する 802.1 Q 情報を指定します。 **Ieee8021QNetBufferListInfo**、NET\_BUFFER\_list を指定すると\_情報は、 [**NDIS\_NET\_buffer\_List\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)の**値**のメンバーを返します。 この構造では、802.1 p priority および仮想 LAN (VLAN) の識別子情報を指定できます。 802.1 p の優先順位情報は、共有メディア802ネットワークでパケットの優先順位を確立するために使用されます。

ミニポートドライバーが NDIS\_カプセル化のサポートを報告している場合\_IEEE\_802\_3\_P\_、および\_OOB カプセル化で Q\_を報告します。では、 **Ieee8021QNetBufferListInfo**データを large send offload version 1 (LSOV1) と large send offload version 2 (LSOV2) イーサネットパケットに挿入する必要があります。

<a href="" id="tcpoffloadbytestransferred"></a>**TcpOffloadBytesTransferred**  
TCP chimney オフロードの送信、受信、または切断の各操作で転送されたデータのバイト数を指定します。

<a href="" id="tcpreceivenopush"></a>**TcpReceiveNoPush**  
TCP chimney オフロード受信要求のプッシュモードを表すブール値を指定します。 **TRUE**の場合、受信要求は非プッシュモードになります。 それ以外の場合、受信要求はプッシュモードになります。

LSOV1、LSOV2、checksum、および IPsec オフロードの種類の場合、ミニポートドライバーは、OOB データの種類と、報告されたオフロード機能に基づいて、タスクのオフロードを実行します。 たとえば、プロトコルドライバーが IPv4 パケット用に LSOV1 services を必要とする場合、プロトコルドライバーによって提供される各送信要求には、NDIS の**LsoV1Transmit**メンバーからの情報が含まれます。これには[ **\_TCP\_LARGE\_send\_オフロード\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) OOB data。 プロトコルドライバーは、送信要求を行う前に、指定されたカプセル化の種類を使用して、ミニポートドライバーが IPv4 をサポートしていることを確認する必要があることに注意してください。

NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_BUFFER\_LIST\_INFO 構造体には、最大セグメントサイズ (MSS) が含まれています。 **Tcpheaderoffset**メンバーは、ミニポートドライバーが ip ヘッダー、ip オプション、または ip 拡張ヘッダーを解析する必要がないように、TCP ヘッダーの場所を指定します。

LSOV2 と LSOV1 をサポートする NDIS 6.0 およびそれ以降のミニポートドライバーでは、Ndis の**型**のメンバーを確認する必要があります[ **\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)を確認して、ドライバースタックが LSOV2 と LSOV1 のどちらを使用しているかを示し、適切なオフロードを実行する必要があります。

LSOv1 の場合、ポートドライバーは、LSO を使用して小さいパケットに分割されているサイズの大きい TCP パケットの送信を完了する前に、NDIS の**tcppayload**メンバーのセグメント化されたパケットで送信した tcp ペイロードのバイト数を書き込みます\_TCP\_LARGE\_\_オフロード\_NET\_バッファー\_一覧\_情報を送信します。

ミニポートドライバーによって、NDIS\_カプセル化\_IEEE\_802\_3\_P\_および\_Q フラグが指定されている場合、ドライバーは NET\_BUFFER のタスクオフロードサービスを実行でき[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)バッファーデータ内の VLAN ヘッダーを含む構造体を一覧表示します。 受信したデータの場合、このフラグはミニポートドライバーが受信チェックサムの計算を実行し、VLAN ヘッダーをイーサネットパケットに入れることを示します。

ミニポートドライバーによって NDIS\_カプセル化が指定されている場合\_IEEE\_802\_3\_P\_および\_の機能の OOB フラグで Q\_を指定します。では、ドライバーは、 **Ieee8021QnetBufferListInfo** OOB データ内の VLAN ヘッダーを含むネットワーク\_バッファー\_リスト構造のオフロードを実行できます。 受信チェックサムオフロードの場合、ミニポートは、VLAN ヘッダーを**Ieee8021QnetBufferListInfo** OOB データに挿入します。

 

 





