---
title: 受信したカプセル化されたパケットのトランスポートヘッダーを検索する
description: 受信パス内のカプセル化されたパケットのトランスポート ヘッダーの検索
ms.assetid: D3BDE575-C9EB-49E3-9B61-FDB99B68ED8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0232f08a5b0a90990a94f60d79ba9b47ce49ecef
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210254"
---
# <a name="locating-the-transport-header-for-encapsulated-packets-in-the-receive-path"></a>受信パス内のカプセル化されたパケットのトランスポート ヘッダーの検索

パケットを受信する場合、[汎用ルーティングカプセル化 (NVGRE) を使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)をサポートする NIC では、まず、パケットがカプセル化されているかどうかを判断し、その場合はカプセル化の種類を決定する必要があります。

**注**  送信パスでは、 [**NDIS\_TCP\_送信\_\_追加\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)をオフロードすると、パケットがカプセル化されます。**IsEncapsulatedPacket**は**TRUE**です。
 

受信パスでは、NIC は、IPv4 トンネル (外側) ヘッダーの [**プロトコル**] フィールドのプロトコル番号、または IPv6 トンネル (外部) ヘッダーの**NextHeader**フィールドのプロトコル番号を調べて、パケットがカプセル化されているかどうかを判断する必要があります。 割り当てられたプロトコル番号の一覧については、<https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xml>を参照してください。

パケットがカプセル化されたパケットであると判断されると、NIC は、カプセル化されたパケットのプロトコルを解析することによって、トランスポート (内部) IP ヘッダーへのオフセットを決定する必要があります。

NDIS 6.30 (Windows Server 2012) 以降では、GRE IP カプセル化のみがサポートされています。 そのため、提供された機能に応じて、NIC は次のことを解析できる必要があります。

-   GRE ([RFC 2784: Generic Routing カプセル化 (GRE)](https://tools.ietf.org/html/rfc2784)) ヘッダー
-   [RFC 2890: GRE のキーおよびシーケンス番号の拡張機能](https://tools.ietf.org/html/rfc2890)
-   IPv4 ([RFC 791: Internet Protocol](https://tools.ietf.org/html/rfc791)) ヘッダー
-   IPv6 ([RFC 2460: Internet Protocol、Version 6 (IPv6)](https://tools.ietf.org/html/rfc2460)) ヘッダー

NIC が不明またはサポートされていないカプセル化プロトコルを検出した場合は、パケットを変更せずにホストスタックに渡す必要があります。

このため、受信パスでは、ミニポートはトランスポート (内部) IP ヘッダーを解析して IP バージョンを判断し、TCP または UDP ヘッダーを取得する必要があります。 これは、NDIS 6.30 (Windows Server 2012) 以降の新しい要件です。

 

 





