---
title: ネットワーク アダプターの RSC 機能の判断
description: セグメント coalescing (RSC) を持つ"、受信-対応ミニポート ドライバーが NdisMSetMiniportAttributes に渡される NDIS_OFFLOAD 構造体を使用して、RSC 機能を報告します。
ms.assetid: 043A09F9-7D5D-4401-9645-19FDBD614659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 196cbecacfe3b18f64849a3b7bfa2a0e96a271c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381413"
---
# <a name="determining-the-rsc-capabilities-of-a-network-adapter"></a>ネットワーク アダプターの RSC 機能の判断


セグメント coalescing (RSC) を持つ"、受信-対応ミニポート ドライバーで、RSC 機能の報告、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)に渡される構造[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。

## <a name="reporting-rsc-capability"></a>RSC 機能の報告


[ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造、**ヘッダー**メンバーを次のように設定する必要があります。

-   **リビジョン**にメンバーを設定する必要があります**NDIS\_オフロード\_リビジョン\_3**します。
-   **サイズ**にメンバーを設定する必要があります**NDIS\_SIZEOF\_NDIS\_オフロード\_リビジョン\_3**します。

RSC のサポートを報告するミニポート ドライバーで、次のメンバーを設定できる、 [ **NDIS\_TCP\_RECV\_SEG\_COALESCE\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_recv_seg_coalesce_offload) 、構造体に格納されている、 **Rsc**のメンバー、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。

-   設定、 **IPv4.Enabled**メンバー **TRUE** IPv4 の RSC のサポートを示すためです。

-   設定、 **IPv6.Enabled**メンバー **TRUE** RSC の ipv6 のサポートを示すためです。

ミニポート ドライバーが少なくともの RSC をサポートする必要があります IEEE 802.3 カプセル化します。 さらに、RSC の他のすべてをカプセル化をサポートできます。 RSC はいくつかのカプセル化をサポートしません、受信パケットをカプセル化の場合は、ドライバーでは通常、スタックのパケットを示す必要があります。

## <a name="querying-rsc-capability"></a>RSC 機能のクエリを実行します。


プロトコルおよびその他のドライバーを発行できますミニポート ドライバーが RSC をサポートしているかどうかを判断する、 [OID\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID を要求返されます、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。

 

 





