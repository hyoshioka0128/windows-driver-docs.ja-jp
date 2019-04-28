---
title: RSS ハッシュの種類
description: RSS ハッシュの種類
ms.assetid: 21ea384c-5fe2-46c1-9e01-30513f505672
keywords:
- 受信側スケーリング WDK ネットワーク、ハッシュ
- RSS の WDK にネットワーク接続、ハッシュ
- WDK RSS ハッシュ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 268a3e52cd8185554b1b151fa871413d9b406a77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372186"
---
# <a name="rss-hashing-types"></a>RSS ハッシュの種類

## <a name="overview"></a>概要

型のハッシュ RSS には、NIC が RSS ハッシュ値を計算するために使用する必要があります、受信したネットワーク データの部分を指定します。

ドライバーの重なってハッシュ型、関数、および間接指定テーブルを設定します。 上にあるドライバーを設定するハッシュ型は、ミニポート ドライバーをサポートする型のサブセットを指定できます。 詳細については、次を参照してください。 [RSS 構成](rss-configuration.md)します。

ハッシュの種類は、次のフラグの有効な組み合わせの OR は。

- NDIS_HASH_IPV4
- NDIS_HASH_TCP_IPV4
- NDIS_HASH_UDP_IPV4
- NDIS_HASH_IPV6
- NDIS_HASH_TCP_IPV6
- NDIS_HASH_UDP_IPV6
- NDIS_HASH_IPV6_EX
- NDIS_HASH_TCP_IPV6_EX
- NDIS_HASH_UDP_IPV6_EX

これらには有効なフラグの組み合わせのセットです。

- IPv4 (NDIS_HASH_IPV4、NDIS_HASH_TCP_IPV4、NDIS_HASH_UDP_IPV4 の組み合わせ)
- IPv6 (NDIS_HASH_IPV6、NDIS_HASH_TCP_IPV6、NDIS_HASH_UDP_IPV6 の組み合わせ)
- IPv6 拡張ヘッダー (NDIS_HASH_IPV6_EX、NDIS_HASH_TCP_IPV6_EX、NDIS_HASH_UDP_IPV6_EX の組み合わせ) を

NIC には、IPv4 のセットからの組み合わせのいずれかをサポートする必要があります。 その他のセットとの組み合わせは、省略可能です。 NIC は、一度に 1 つ以上のセットをサポートできます。 この場合、どのハッシュ入力 NIC は受信したデータの種類を決定します。

一般に、NIC は、受信したデータを正しく解釈できない場合は、いないハッシュ値を計算する必要がありますに。 など、NIC には、IPv4 のみがサポートされ、正しく解釈できません、IPv6 パケットを受信する場合は、いないハッシュ値を計算する必要がありますに。 NIC は、トランスポートの種類がサポートされていないパケットを受信するハッシュ値を計算する必要があります。 たとえば、NIC は、TCP パケットのハッシュ値を計算することで、UDP パケットを受信する場合は、いないハッシュ値を計算する必要があります。 この場合、RSS 以外の場合と同様、パケットが処理されます。 非-RSS の詳細については、処理を受信を参照してください。[非 RSS 受信処理](non-rss-receive-processing.md)します。

## <a name="ipv4-hash-type-combinations"></a>IPv4 ハッシュ タイプの組み合わせ

IPv4 設定で有効なハッシュの種類の組み合わせは次のとおりです。

- [NDIS_HASH_IPV4](#ndishashipv4)
- [NDIS_HASH_TCP_IPV4](#ndishashtcpipv4)
- [NDIS_HASH_UDP_IPV4](#ndishashudpipv4)
- [NDIS_HASH_TCP_IPV4 | NDIS_HASH_IPV4](#ndishashtcpipv4--ndishashipv4)
- [NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4](#ndishashudpipv4--ndishashipv4)
- [NDIS_HASH_TCP_IPV4 | NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4](#ndishashtcpipv4--ndishashudpipv4--ndishashipv4)

### <a name="ndishashipv4"></a>NDIS_HASH_IPV4  

だけでこのフラグが設定されている場合、NIC は、次の IPv4 ヘッダー フィールドに対してハッシュ値を計算する必要があります。

- ソースから IPv4 アドレス
- 送信先 IPv4 アドレス

>[!NOTE]
> NIC は、IP と TCP の両方のヘッダーを含むパケットを受信する場合 NDIS_HASH_TCP_IPV4 いない常に使用してください。 断片化されたパケットの場合は、NDIS_HASH_IPV4 を使用する必要があります。 これには、IP と TCP の両方のヘッダーを含む最初のフラグメントが含まれます。

### <a name="ndishashtcpipv4"></a>NDIS_HASH_TCP_IPV4

だけでこのフラグが設定されている場合、NIC は、TCP セグメントを含む IPv4 パケットを識別するために、受信したデータを解析する必要があります。

NIC は、識別し、存在する任意の IP オプションをスキップする必要があります。 NIC は、IP オプションをスキップできません、ハッシュ値には計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- ソースから IPv4 アドレス
- 送信先 IPv4 アドレス
- ソース TCP ポート
- 接続先 TCP ポート

### <a name="ndishashudpipv4"></a>NDIS_HASH_UDP_IPV4

単独でこのフラグが設定されている場合、NIC は UDP データグラムを含む IPv4 パケットを識別するために、受信したデータを解析する必要があります。

NIC は、識別し、存在する任意の IP オプションをスキップする必要があります。 NIC は、IP オプションをスキップできません、ハッシュ値には計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- ソースから IPv4 アドレス
- 送信先 IPv4 アドレス
- 送信元 UDP ポート
- 宛先の UDP ポート

### <a name="ndishashtcpipv4--ndishashipv4"></a>NDIS_HASH_TCP_IPV4 | NDIS_HASH_IPV4

このフラグの組み合わせが設定されている場合、NIC は、NDIS_HASH_TCP_IPV4 ケースの指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV4 大文字と小文字の指定されたハッシュ値を計算する必要があります。

### <a name="ndishashudpipv4--ndishashipv4"></a>NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4

このフラグの組み合わせが設定されている場合、NIC は、NDIS_HASH_UDP_IPV4 ケースの指定されたハッシュ計算を実行する必要があります。 ただし、パケットに UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV4 大文字と小文字の指定されたハッシュ値を計算する必要があります。

### <a name="ndishashtcpipv4--ndishashudpipv4--ndishashipv4"></a>NDIS_HASH_TCP_IPV4 | NDIS_HASH_UDP_IPV4 | NDIS_HASH_IPV4

このフラグの組み合わせを設定すると、NIC はパケットのトランスポートによって指定されたハッシュの計算を実行する必要があります。 ただし、パケットに TCP または UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV4 大文字と小文字の指定されたハッシュ値を計算する必要があります。

## <a name="ipv6-hash-type-combinations"></a>IPv6 ハッシュ タイプの組み合わせ

IPv6 設定の有効なハッシュ タイプの組み合わせは次のとおりです。

- [NDIS_HASH_IPV6](#ndishashipv6)
- [NDIS_HASH_TCP_IPV6](#ndishashtcpipv6)
- [NDIS_HASH_UDP_IPV6](#ndishashudpipv6)
- [NDIS_HASH_TCP_IPV6 | NDIS_HASH_IPV6](#ndishashtcpipv6--ndishashipv6)
- [NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6](#ndishashudpipv6--ndishashipv6)
- [NDIS_HASH_TCP_IPV6 | NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6](#ndishashtcpipv6--ndishashudpipv6--ndishashipv6)

### <a name="ndishashipv6"></a>NDIS_HASH_IPV6

だけでこのフラグが設定されている場合、NIC は、次のフィールドに対してハッシュを計算する必要があります。

- ソースから IPv6 アドレス
- 変換先の IPv6 アドレス

### <a name="ndishashtcpipv6"></a>NDIS_HASH_TCP_IPV6

だけでこのフラグが設定されている場合、NIC は、TCP セグメントを含む IPv6 パケットを識別するために、受信したデータを解析する必要があります。 NIC は、識別し、パケットに存在するすべての IPv6 拡張ヘッダーをスキップする必要があります。 NIC は、すべての IPv6 拡張ヘッダーをスキップできません、ハッシュ値には計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- ソース IPv6 のアドレス
- 宛先 IPv6 のアドレス
- ソース TCP ポート
- 接続先 TCP ポート

### <a name="ndishashudpipv6"></a>NDIS_HASH_UDP_IPV6

単独でこのフラグが設定されている場合、NIC は UDP データグラムを含む IPv6 パケットを識別するために、受信したデータを解析する必要があります。 NIC は、識別し、パケットに存在するすべての IPv6 拡張ヘッダーをスキップする必要があります。 NIC は、すべての IPv6 拡張ヘッダーをスキップできません、ハッシュ値には計算されません。

NIC は、次のフィールドに対してハッシュ値を計算する必要があります。

- ソースから IPv6 アドレス
- 変換先の IPv6 アドレス
- 送信元 UDP ポート
- 宛先の UDP ポート

### <a name="ndishashtcpipv6--ndishashipv6"></a>NDIS_HASH_TCP_IPV6 | NDIS_HASH_IPV6

このフラグの組み合わせが設定されている場合、NIC は、NDIS_HASH_TCP_IPV6 ケースの指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーが含まれていない場合に、NIC は NDIS_HASH_IPV6 大文字と小文字の指定されたハッシュを計算する必要があります。

### <a name="ndishashudpipv6--ndishashipv6"></a>NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6

このフラグの組み合わせが設定されている場合、NIC は、NDIS_HASH_UDP_IPV6 ケースの指定されたハッシュ計算を実行する必要があります。 ただし、パケットに UDP ヘッダーが含まれていない場合に、NIC は NDIS_HASH_IPV6 大文字と小文字の指定されたハッシュを計算する必要があります。

### <a name="ndishashtcpipv6--ndishashudpipv6--ndishashipv6"></a>NDIS_HASH_TCP_IPV6 | NDIS_HASH_UDP_IPV6 | NDIS_HASH_IPV6

このフラグの組み合わせを設定すると、NIC はパケットのトランスポートによって指定されたハッシュの計算を実行する必要があります。 ただし、パケットに TCP または UDP ヘッダーが含まれていない場合、NIC は NDIS_HASH_IPV6 場合は、指定されたハッシュ値を計算する必要があります。

## <a name="ipv6-with-extension-headers-hash-type-combinations"></a>IPv6 ヘッダー ハッシュ タイプの拡張機能の組み合わせを

拡張機能ヘッダーのセットを IPv6 では有効な組み合わせは次のとおりです。

- [NDIS_HASH_IPV6_EX](#ndishashipv6ex)
- [NDIS_HASH_TCP_IPV6_EX](#ndishashtcpipv6ex)
- [NDIS_HASH_UDP_IPV6_EX](#ndishashudpipv6ex)
- [NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_IPV6_EX](#ndishashtcpipv6ex--ndishashipv6ex)
- [NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX](#ndishashudpipv6ex--ndishashipv6ex)
- [NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX](#ndishashtcpipv6ex--ndishashudpipv6ex--ndishashipv6ex)

### <a name="ndishashipv6ex"></a>NDIS_HASH_IPV6_EX  

だけでこのフラグが設定されている場合、NIC は、次のフィールドに対してハッシュを計算する必要があります。

- IPv6 の宛先オプション ヘッダーのホーム アドレス オプションから自宅の住所。 拡張機能ヘッダーが存在しない場合は、送信元 IPv6 アドレスを使用します。
- ルーティング-ヘッダー-型-2、関連付けられている拡張機能ヘッダーからに含まれている IPv6 アドレス。 拡張機能ヘッダーが存在しない場合は、宛先 IPv6 アドレスを使用します。

### <a name="ndishashtcpipv6ex"></a>NDIS_HASH_TCP_IPV6_EX

だけでこのフラグが設定されている場合、NIC は、次のフィールドに対してハッシュを計算する必要があります。

- IPv6 の宛先オプション ヘッダーのホーム アドレス オプションから自宅の住所。 拡張機能ヘッダーが存在しない場合は、送信元 IPv6 アドレスを使用します。
- ルーティング-ヘッダー-型-2、関連付けられている拡張機能ヘッダーからに含まれている IPv6 アドレス。 拡張機能ヘッダーが存在しない場合は、宛先 IPv6 アドレスを使用します。
- ソース TCP ポート
- 接続先 TCP ポート

### <a name="ndishashudpipv6ex"></a>NDIS_HASH_UDP_IPV6_EX

だけでこのフラグが設定されている場合、NIC は、次のフィールドに対してハッシュを計算する必要があります。

- IPv6 の宛先オプション ヘッダーのホーム アドレス オプションから自宅の住所。 拡張機能ヘッダーが存在しない場合は、送信元 IPv6 アドレスを使用します。
- ルーティング-ヘッダー-型-2、関連付けられている拡張機能ヘッダーからに含まれている IPv6 アドレス。 拡張機能ヘッダーが存在しない場合は、宛先 IPv6 アドレスを使用します。
- 送信元 UDP ポート
- 宛先の UDP ポート

### <a name="ndishashtcpipv6ex--ndishashipv6ex"></a>NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_IPV6_EX

このフラグの組み合わせが設定されている場合、NIC は、NDIS_HASH_TCP_IPV6_EX ケースの指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP ヘッダーが含まれていない場合に、NIC は NDIS_HASH_IPV6_EX 大文字と小文字の指定されたハッシュを計算する必要があります。

### <a name="ndishashudpipv6ex--ndishashipv6ex"></a>NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX

このフラグの組み合わせが設定されている場合、NIC は、NDIS_HASH_UDP_IPV6_EX ケースの指定されたハッシュ計算を実行する必要があります。 ただし、パケットに UDP ヘッダーが含まれていない場合に、NIC は NDIS_HASH_IPV6_EX 大文字と小文字の指定されたハッシュを計算する必要があります。

### <a name="ndishashtcpipv6ex--ndishashudpipv6ex--ndishashipv6ex"></a>NDIS_HASH_TCP_IPV6_EX | NDIS_HASH_UDP_IPV6_EX | NDIS_HASH_IPV6_EX

このフラグの組み合わせが設定されている場合、NIC は、パケットのトランスポートで指定されたハッシュ計算を実行する必要があります。 ただし、パケットに TCP または UDP ヘッダーが含まれていない場合に、NIC は NDIS_HASH_IPV6_EX 大文字と小文字の指定されたハッシュを計算する必要があります。

> [!NOTE]
> NIC が IPv6 拡張機能のハッシュの種類に従って、(IPv6 拡張ヘッダー フィールド) のハッシュ値を計算する必要がありますミニポート ドライバーでは、NIC の NDIS_RSS_CAPS_HASH_TYPE_TCP_IPV6_EX や NDIS_RSS_CAPS_HASH_TYPE_UDP_IPV6_EX の機能を報告する場合プロトコル ドライバーに設定します。 NIC は、拡張機能のハッシュの種類または通常のハッシュの種類のいずれかをハッシュ値の計算対象の IPv6 パケットの NET_BUFFER_LIST 構造に格納できます。 

ミニポート ドライバーのハッシュの種類の設定、 [ **NET_BUFFER_LIST** ](https://msdn.microsoft.com/library/windows/hardware/ff568388)する前に、受信したデータ構造体。 詳細については、次を参照してください。 [RSS の受信データのことを示す](indicating-rss-receive-data.md)します。

 

 





