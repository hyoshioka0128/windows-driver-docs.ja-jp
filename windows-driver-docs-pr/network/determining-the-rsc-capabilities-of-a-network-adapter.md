---
title: ネットワークアダプターの RSC 機能の決定
description: 受信セグメント合体 (RSC) 対応のミニポートドライバーは、NdisMSetMiniportAttributes に渡す NDIS_OFFLOAD 構造体を介して RSC 機能を報告します。
ms.assetid: 043A09F9-7D5D-4401-9645-19FDBD614659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5b63cf8a3fdd22fe4aa13e9afef078cd09a42f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838145"
---
# <a name="determining-the-rsc-capabilities-of-a-network-adapter"></a>ネットワークアダプターの RSC 機能の決定


受信セグメント合体 (RSC) 対応のミニポートドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)に渡す[**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造を通じて RSC 機能を報告します。

## <a name="reporting-rsc-capability"></a>RSC 機能のレポート


[**NDIS\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体では、次のように**ヘッダー**メンバーを設定する必要があります。

-   **リビジョン**メンバーを**NDIS\_OFFLOAD\_revision\_3**に設定する必要があります。
-   **Size**メンバーは、 **ndis\_SIZEOF\_ndis\_OFFLOAD\_REVISION\_3**に設定する必要があります。

RSC のサポートをレポートするために、ミニポートドライバーでは、ndis の**rsc**メンバーに格納されている、 [**ndis\_TCP\_RECV\_SEG\_合体\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_recv_seg_coalesce_offload)構造体に、次のメンバーを設定でき[ **\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)の構造:

-   Ipv4 の RSC のサポートを示すには、 **ipv4 の Enabled**メンバーを**TRUE**に設定します。

-   Ipv6 の RSC のサポートを示すには、 **ipv6 の有効な**メンバーを**TRUE**に設定します。

ミニポートドライバーは、少なくとも IEEE 802.3 カプセル化に対して RSC をサポートする必要があります。 また、他のすべてのカプセル化に対して RSC をサポートすることもできます。 一部のカプセル化に対して RSC がサポートされておらず、そのカプセル化のパケットを受信する場合、ドライバーはパケットが正常にスタックしていることを示す必要があります。

## <a name="querying-rsc-capability"></a>RSC 機能のクエリ


ミニポートドライバーで RSC がサポートされているかどうかを判断するために、プロトコルドライバーやその他のドライバーは、 [\_TCP\_オフロード\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)の oid 要求を発行できます。これにより、 [**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)が返されます。データ.

 

 





