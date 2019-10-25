---
title: IPsec Offload Version 2 によるネットワーク データの送信
description: IPsec Offload Version 2 によるネットワーク データの送信
ms.assetid: d3580313-a98b-4150-b344-e3e395ce68e9
keywords:
- IPsecOV2 WDK TCP/IP transport, データの送信
- データの送信 (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6fe7ef224f6ccc3e99b00f0a48e91cc164ed86c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841964"
---
# <a name="sending-network-data-with-ipsec-offload-version-2"></a>IPsec Offload Version 2 によるネットワーク データの送信

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




TCP/IP トランスポートでは、1つまたは複数の SAs に対して IPsec オフロードバージョン 2 (IPsecOV2) の情報が表示されます。この情報は、 [ipsec\_オフロード\_V2\_\_SA OID を追加する\_タスク\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) 、1つまたは複数の SAs に\_ます。 ミニポートドライバーが OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA を追加した結果を返す前に、ミニポートドライバーはオフロードハンドルを初期化します。 TCP/IP トランスポートは、NDIS\_IPSEC\_オフロード\_V2\_NET に IPsecOV2 情報を指定することによって、ミニポートドライバーに対して、 [**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の処理をオフロードするように要求し[ **\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)と[**NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)構造体 (net に含まれる)\_帯域外 (OOB) 情報を一覧表示\_バッファー。

TCP/IP トランスポートでは、NDIS の**Offloadhandle**メンバーにオフロードハンドルが指定されています[ **\_IPSEC\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)を指定して送信するハンドルを指定します。送信パケットのトランスポート (エンドツーエンド接続) 部分のセキュリティアソシエーション (SA)。

TCP/IP トランスポートでは、 [**NDIS\_IPSEC\_OFFLOAD\_V2\_ヘッダー\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)構造体に次のヘッダー情報が提供されます。

-   AH ヘッダー、ESP ヘッダー、またはその両方のヘッダーオフセット。

-   次のプロトコル値 (ESP トレーラーに含まれるものと同じ)。

-   結合された large send offload (LSO) と IPsec オフロードに使用されるパッドの長さ。

また、送信パケットがトンネル経由で送信される場合、TCP/IP トランスポートは[**NDIS\_IPSEC\_オフロード\_V2\_トンネル\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)構造体を提供します。 この構造体は、送信パケットのトンネル部分の送信 SA へのオフロードハンドルを指定します。 OOB 情報へのアクセスの詳細については、「 [IPsec オフロードバージョン2での NET\_BUFFER\_LIST 情報へのアクセス](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)」を参照してください。

ミニポートドライバーは、oid セットの Oid 要求に応じてオフロードハンドルを提供し[\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA を追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)します。 SAs の詳細については、「 [IPsec オフロードバージョン2でのセキュリティアソシエーションの管理](managing-security-associations-in-ipsec-offload-version-2.md)」を参照してください。

ミニポートドライバーが[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数の送信要求を処理するとき、ミニポートドライバーは次のようになります。

-   ハードウェアが IPsec オフロードサービスを処理するように構成されていることを確認します。 ハードウェアが IPsec オフロードサービスを処理するように構成されていない場合、ミニポートドライバーは、オフロードサービスを提供せずに送信要求を処理する必要があります。

-   [**Ndis\_ipsec\_オフロード\_v2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)および[**NDIS\_IPSEC\_オフロード\_v2\_トンネルのハンドルを確認\_NET\_BUFFER\_\_情報構造を一覧表示し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)て、IPsec 暗号化処理が必要かどうかを判断します。 オフロードハンドルの値が0の場合は、 [**NET\_BUFFER\_の一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)に対して IPsec タスクオフロードを実行する必要がないことを示します。 指定したオフロードハンドルに対応するオフロード SA がミニポートドライバーで見つからない場合、送信パケットは、 **NDIS\_STATUS\_のエラー**値で失敗します。

-   [**NDIS\_TCP\_LARGE\_送信\_オフロード\_net\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)構造体のハンドルを検証して、ネットに対してセグメンテーションオフロードを実行するかどうかを決定し @no__t_ [**12_ バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)。

-   [**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)内のすべての送信パケットに対して、必要な AH および ESP 処理を完了します。 NIC が送信パケットで IPsec 処理を実行すると、パケットデータに対して暗号化操作が実行されます。 TCP/IP トランスポートは既にパケットのフレームを作成し、必要に応じて埋め込み、シーケンス番号とセキュリティパラメーターインデックス (SPI) を割り当てています。 LSO と IPsec オフロードの組み合わせでは、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)には、NIC が大きなパケットをセグメントに分割している間に破棄されるパディングが含まれる場合があります。 埋め込みの量は、 [**NDIS\_IPSEC\_OFFLOAD\_V2\_ヘッダー\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)構造体の**padlength**メンバーに指定されています。 セグメント化されたパケットには、IPsec 操作をサポートするための埋め込みが必要になる場合

LSO と IPsecOV2 の両方を要求するパケットがプロトコルドライバーによって送信されると、ESP トレーラーはフレームされません。 これは、ESP トレーラーの情報 (パディングの長さなど) が NIC によって生成された最後のセグメントに対して正確ではないためです。

 

 





