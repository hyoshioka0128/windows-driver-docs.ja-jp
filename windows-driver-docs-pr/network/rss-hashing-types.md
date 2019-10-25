---
title: RSS ハッシュの種類
description: RSS ハッシュの種類
ms.assetid: 21ea384c-5fe2-46c1-9e01-30513f505672
keywords:
- 受信側のスケーリング WDK ネットワーク、ハッシュ
- RSS WDK ネットワーク、ハッシュ
- ハッシュ WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac1912275961993c16575c25c09d398f11648d73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842005"
---
# <a name="rss-hashing-types"></a>RSS ハッシュの種類

## <a name="overview"></a>概要

RSS ハッシュの種類では、NIC が RSS ハッシュ値を計算するために使用する必要がある受信ネットワークデータの一部を指定します。

それ以降のドライバーは、ハッシュの種類、関数、および間接参照テーブルを設定します。 これまでのドライバーによって設定されるハッシュの種類は、ミニポートドライバーがサポートできる種類のサブセットにすることができます。 詳細については、「 [RSS の構成](rss-configuration.md)」を参照してください。

ハッシュの種類は、次のフラグの有効な組み合わせです。

- NDIS_HASH_IPV4
- NDIS_HASH_TCP_IPV4
- NDIS_HASH_UDP_IPV4
- NDIS_HASH_IPV6
- NDIS_HASH_TCP_IPV6
- NDIS_HASH_UDP_IPV6
- NDIS_HASH_IPV6_EX
- NDIS_HASH_TCP_IPV6_EX
- NDIS_HASH_UDP_IPV6_EX

有効なフラグの組み合わせのセットを次に示します。

- IPv4 (NDIS_HASH_IPV4、NDIS_HASH_TCP_IPV4、NDIS_HASH_UDP_IPV4 の組み合わせ)
- IPv6 (NDIS_HASH_IPV6、NDIS_HASH_TCP_IPV6、および NDIS_HASH_UDP_IPV6 の組み合わせ)
- IPv6 と拡張ヘッダー (NDIS_HASH_IPV6_EX、NDIS_HASH_TCP_IPV6_EX、NDIS_HASH_UDP_IPV6_EX の組み合わせ)

NIC は、IPv4 セットの組み合わせのいずれかをサポートしている必要があります。 その他のセットと組み合わせは省略可能です。 NIC は、一度に複数のセットをサポートできます。 この場合、受信したデータの種類によって、NIC で使用されるハッシュの種類が決まります。

一般に、受信したデータを NIC が正しく解釈できない場合、ハッシュ値を計算する必要はありません。 たとえば、NIC が IPv4 のみをサポートしていて、正しく解釈できない IPv6 パケットを受信する場合は、ハッシュ値を計算しないようにする必要があります。 NIC がサポートしていないトランスポートの種類のパケットを受信した場合、ハッシュ値を計算することはできません。 たとえば、NIC が TCP パケットのハッシュ値を計算することが想定されている場合に UDP パケットを受信すると、ハッシュ値を計算する必要がありません。 この場合、パケットは RSS 以外の場合と同様に処理されます。 RSS 以外の受信処理の詳細については、「 [Rss 以外の受信処理](non-rss-receive-processing.md)」を参照してください。

## <a name="ipv4-hash-type-combinations"></a>IPv4 ハッシュの種類の組み合わせ

IPv4 セットでの有効なハッシュの種類の組み合わせは次のとおりです。

- [NDIS_HASH_IPV4](#ndis_hash_ipv4)
- [NDIS_HASH_TCP_IPV4](#ndis_hash_tcp_ipv4)
- [NDIS_HASH_UDP_IPV4](#ndis_hash_udp_ipv4)
- [NDIS_HASH_TCP_IPV4 |NDIS_HASH_IPV4](#ndis_hash_tcp_ipv4--ndis_hash_ipv4)
- [NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4](#ndis_hash_udp_ipv4--ndis_hash_ipv4)
- [NDIS_HASH_TCP_IPV4 |NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4](#ndis_hash_tcp_ipv4--ndis_hash_udp_ipv4--ndis_hash_ipv4)

### <a name="ndis_hash_ipv4"></a>NDIS_HASH_IPV4  

このフラグだけが設定されている場合、NIC は次の IPv4 ヘッダーフィールドに対してハッシュ値を計算する必要があります。

- 送信元-IPv4 アドレス
- 宛先-IPv4 アドレス

>[!NOTE]
> NIC が IP ヘッダーと TCP ヘッダーの両方を持つパケットを受信した場合、NDIS_HASH_TCP_IPV4 は常に使用することはできません。 フラグメント化された IP パケットの場合は、NDIS_HASH_IPV4 を使用する必要があります。 これには、IP ヘッダーと TCP ヘッダーの両方を含む最初のフラグメントが含まれます。

### <a name="ndis_hash_tcp_ipv4"></a>NDIS_HASH_TCP_IPV4

このフラグだけが設定されている場合、NIC は、受信したデータを解析して、TCP セグメントを含む IPv4 パケットを識別する必要があります。

NIC は、存在する任意の IP オプションを識別してスキップする必要があります。 NIC が IP オプションをスキップできない場合、ハッシュ値は計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- 送信元-IPv4 アドレス
- 宛先-IPv4 アドレス
- 発信元 TCP ポート
- 宛先 TCP ポート

### <a name= "ndis_hash_udp_ipv4"></a>NDIS_HASH_UDP_IPV4

このフラグだけが設定されている場合、NIC は、受信したデータを解析して、UDP データグラムを含む IPv4 パケットを識別する必要があります。

NIC は、存在する任意の IP オプションを識別してスキップする必要があります。 NIC が IP オプションをスキップできない場合、ハッシュ値は計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- 送信元-IPv4 アドレス
- 宛先-IPv4 アドレス
- ソース UDP ポート
- 宛先の UDP ポート

### <a name="ndis_hash_tcp_ipv4--ndis_hash_ipv4"></a>NDIS_HASH_TCP_IPV4 |NDIS_HASH_IPV4

このフラグの組み合わせが設定されている場合、NIC は NDIS_HASH_TCP_IPV4 ケースに対して指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV4 ケースに対して指定されているハッシュ値を計算する必要があります。

### <a name="ndis_hash_udp_ipv4--ndis_hash_ipv4"></a>NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4

このフラグの組み合わせが設定されている場合、NIC は NDIS_HASH_UDP_IPV4 ケースに対して指定されたハッシュ計算を実行する必要があります。 ただし、パケットに UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV4 ケースに対して指定されているハッシュ値を計算する必要があります。

### <a name="ndis_hash_tcp_ipv4--ndis_hash_udp_ipv4--ndis_hash_ipv4"></a>NDIS_HASH_TCP_IPV4 |NDIS_HASH_UDP_IPV4 |NDIS_HASH_IPV4

このフラグの組み合わせが設定されている場合、NIC はパケット内のトランスポートによって指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーまたは UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV4 ケースに指定されているハッシュ値を計算する必要があります。

## <a name="ipv6-hash-type-combinations"></a>IPv6 ハッシュの種類の組み合わせ

IPv6 セットでの有効なハッシュの種類の組み合わせは次のとおりです。

- [NDIS_HASH_IPV6](#ndis-hash-ipv6)
- [NDIS_HASH_TCP_IPV6](#ndis_hash_tcp_ipv6)
- [NDIS_HASH_UDP_IPV6](#ndis_hash_udp_ipv6)
- [NDIS_HASH_TCP_IPV6 |NDIS_HASH_IPV6](#ndis_hash_tcp_ipv6--ndis_hash_ipv6)
- [NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6](#ndis_hash_udp_ipv6--ndis_hash_ipv6)
- [NDIS_HASH_TCP_IPV6 |NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6](#ndis_hash_tcp_ipv6--ndis_hash_udp_ipv6--ndis_hash_ipv6)

### <a name="ndis-hash-ipv6"></a>NDIS\_HASH\_IPV6

このフラグだけが設定されている場合、NIC は次のフィールドに対してハッシュを計算する必要があります。

- 送信元-IPv6 アドレス
- 宛先-IPv6 アドレス

### <a name="ndis_hash_tcp_ipv6"></a>NDIS_HASH_TCP_IPV6

このフラグだけが設定されている場合、NIC は、受信したデータを解析して、TCP セグメントを含む IPv6 パケットを識別する必要があります。 NIC は、パケット内に存在する IPv6 拡張ヘッダーを識別してスキップする必要があります。 NIC が IPv6 拡張ヘッダーをスキップできない場合、ハッシュ値は計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- 送信元-IPv6 アドレス
- 宛先-IPv6 アドレス
- 発信元 TCP ポート
- 宛先 TCP ポート

### <a name="ndis_hash_udp_ipv6"></a>NDIS_HASH_UDP_IPV6

このフラグだけが設定されている場合、NIC は、受信したデータを解析して、UDP データグラムを含む IPv6 パケットを識別する必要があります。 NIC は、パケット内に存在する IPv6 拡張ヘッダーを識別してスキップする必要があります。 NIC が IPv6 拡張ヘッダーをスキップできない場合、ハッシュ値は計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- 送信元-IPv6 アドレス
- 宛先-IPv6 アドレス
- ソース UDP ポート
- 宛先の UDP ポート

### <a name="ndis_hash_tcp_ipv6--ndis_hash_ipv6"></a>NDIS_HASH_TCP_IPV6 |NDIS_HASH_IPV6

このフラグの組み合わせが設定されている場合、NIC は NDIS_HASH_TCP_IPV6 ケースに対して指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV6 ケースに対して指定されているハッシュを計算する必要があります。

### <a name="ndis_hash_udp_ipv6--ndis_hash_ipv6"></a>NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6

このフラグの組み合わせが設定されている場合、NIC は NDIS_HASH_UDP_IPV6 ケースに対して指定されたハッシュ計算を実行する必要があります。 ただし、パケットに UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV6 ケースに対して指定されているハッシュを計算する必要があります。

### <a name="ndis_hash_tcp_ipv6--ndis_hash_udp_ipv6--ndis_hash_ipv6"></a>NDIS_HASH_TCP_IPV6 |NDIS_HASH_UDP_IPV6 |NDIS_HASH_IPV6

このフラグの組み合わせが設定されている場合、NIC はパケット内のトランスポートによって指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーまたは UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV6 の場合に指定されたハッシュ値を計算する必要があります。

## <a name="ipv6-with-extension-headers-hash-type-combinations"></a>IPv6 と拡張ヘッダーのハッシュの種類の組み合わせ

IPv6 と拡張ヘッダーの有効な組み合わせは、次のとおりです。

- [NDIS_HASH_IPV6_EX](#ndis_hash_ipv6_ex)
- [NDIS_HASH_TCP_IPV6_EX](#ndis_hash_tcp_ipv6_ex)
- [NDIS_HASH_UDP_IPV6_EX](#ndis_hash_udp_ipv6_ex)
- [NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_IPV6_EX](#ndis_hash_tcp_ipv6_ex--ndis_hash_ipv6_ex)
- [NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX](#ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex)
- [NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX](#ndis_hash_tcp_ipv6_ex--ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex)

### <a name="ndis_hash_ipv6_ex"></a>NDIS_HASH_IPV6_EX  

このフラグだけが設定されている場合、NIC は次のフィールドに対してハッシュを計算する必要があります。

- IPv6 送信先オプションヘッダーの [ホームアドレス] オプションの [ホームアドレス]。 拡張ヘッダーが存在しない場合は、送信元の IPv6 アドレスを使用します。
- 関連付けられている拡張ヘッダーから、ルーティングヘッダーの種類2に含まれる IPv6 アドレス。 拡張ヘッダーが存在しない場合は、送信先の IPv6 アドレスを使用します。

### <a name="ndis_hash_tcp_ipv6_ex"></a>NDIS_HASH_TCP_IPV6_EX

このフラグだけが設定されている場合、NIC は次のフィールドに対してハッシュを計算する必要があります。

- IPv6 送信先オプションヘッダーの [ホームアドレス] オプションの [ホームアドレス]。 拡張ヘッダーが存在しない場合は、送信元の IPv6 アドレスを使用します。
- 関連付けられている拡張ヘッダーから、ルーティングヘッダーの種類2に含まれる IPv6 アドレス。 拡張ヘッダーが存在しない場合は、送信先の IPv6 アドレスを使用します。
- 発信元 TCP ポート
- 宛先 TCP ポート

### <a name="ndis_hash_udp_ipv6_ex"></a>NDIS_HASH_UDP_IPV6_EX

このフラグだけが設定されている場合、NIC は次のフィールドに対してハッシュを計算する必要があります。

- IPv6 送信先オプションヘッダーの [ホームアドレス] オプションの [ホームアドレス]。 拡張ヘッダーが存在しない場合は、送信元の IPv6 アドレスを使用します。
- 関連付けられている拡張ヘッダーから、ルーティングヘッダーの種類2に含まれる IPv6 アドレス。 拡張ヘッダーが存在しない場合は、送信先の IPv6 アドレスを使用します。
- ソース UDP ポート
- 宛先の UDP ポート

### <a name="ndis_hash_tcp_ipv6_ex--ndis_hash_ipv6_ex"></a>NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_IPV6_EX

このフラグの組み合わせが設定されている場合、NIC は NDIS_HASH_TCP_IPV6_EX ケースに対して指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV6_EX ケースに対して指定されているハッシュを計算する必要があります。

### <a name="ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex"></a>NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX

このフラグの組み合わせが設定されている場合、NIC は NDIS_HASH_UDP_IPV6_EX ケースに対して指定されたハッシュ計算を実行する必要があります。 ただし、パケットに UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV6_EX ケースに対して指定されているハッシュを計算する必要があります。

### <a name="ndis_hash_tcp_ipv6_ex--ndis_hash_udp_ipv6_ex--ndis_hash_ipv6_ex"></a>NDIS_HASH_TCP_IPV6_EX |NDIS_HASH_UDP_IPV6_EX |NDIS_HASH_IPV6_EX

このフラグの組み合わせが設定されている場合、NIC はパケットトランスポートによって指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーまたは UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV6_EX ケースに対して指定されているハッシュを計算する必要があります。

> [!NOTE]
> ミニポートドライバーが NIC の NDIS_RSS_CAPS_HASH_TYPE_TCP_IPV6_EX または NDIS_RSS_CAPS_HASH_TYPE_UDP_IPV6_EX 機能を報告する場合、NIC は IPv6 拡張ハッシュの種類に従ってハッシュ値 (IPv6 拡張ヘッダーのフィールド) を計算する必要があります。プロトコルドライバーによって設定されます。 NIC は、ハッシュ値を計算する IPv6 パケットの NET_BUFFER_LIST 構造に、拡張ハッシュの種類または通常のハッシュの種類のいずれかを格納できます。

ミニポートドライバーは、受信したデータを示す前に、 [**NET_BUFFER_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体にハッシュの種類を設定します。 詳細については、「 [RSS 受信データの表示](indicating-rss-receive-data.md)」を参照してください。
