---
title: パケットをカプセル化したトランスポート ヘッダーを検索します。
description: 受信パス内のカプセル化されたパケットのトランスポート ヘッダーの検索
ms.assetid: D3BDE575-C9EB-49E3-9B61-FDB99B68ED8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 657ad67c7c7721ac8313d190dc4868555020947d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356206"
---
# <a name="locating-the-transport-header-for-encapsulated-packets-in-the-receive-path"></a>受信パス内のカプセル化されたパケットのトランスポート ヘッダーの検索

パケットを受信するには、NIC をサポートする[Network Virtualization using Generic Routing Encapsulation (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)そうである場合、パケットをカプセル化するかどうかを判断する必要があります最初にカプセル化の種類。

**注**  場合、送信パスでパケットがカプセル化[ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info).**IsEncapsulatedPacket**は**TRUE**します。
 

NIC で受信パスでは、プロトコル番号を確認して、パケットがカプセル化されたかどうかを決定する必要があります、**プロトコル**IPv4 トンネル (外側) のヘッダーのフィールドまたは**NextHeader** IPv6 のフィールドトンネル (外側) のヘッダー。 割り当てられたプロトコル番号の一覧をご覧<http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xml>します。

パケットをカプセル化されたパケットを決定すると、NIC は、カプセル化されたパケットのプロトコルを解析することによってトランスポート (内部) の IP ヘッダーにオフセットを決定する必要があります。

NDIS 6.30 (Windows Server 2012) 以降、GRE IP カプセル化のみがサポートされています。 したがって、NIC が提供された機能に応じて、次を解析することがあります。

-   GRE ([RFC 2784。Generic Routing Encapsulation (GRE)](https://tools.ietf.org/html/rfc2784)) ヘッダー
-   [RFC 2890:GRE をキーとシーケンス番号の拡張機能](https://tools.ietf.org/html/rfc2890)
-   IPv4 ([RFC 791。インターネット プロトコル](https://tools.ietf.org/html/rfc791)) ヘッダー
-   IPv6 ([RFC 2460。インターネット プロトコル バージョン 6 (IPv6)](https://tools.ietf.org/html/rfc2460)) ヘッダー

NIC には、不明なまたはサポート対象外のカプセル化プロトコルが検出されると、パケットを変更せず、ホストのスタックに渡すことが必要があります。

そのため、受信パス上ミニポート解析する必要があります (内部) の IP ヘッダーに、TCP を取得したり IP のバージョンを判断するトランスポートまたは UDP ヘッダー。 これは、NDIS 6.30 (Windows Server 2012) 以降、新しい要件です。

 

 





