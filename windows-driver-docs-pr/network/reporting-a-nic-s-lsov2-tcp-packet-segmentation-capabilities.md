---
title: NIC の LSOV2 TCP パケット セグメンテーション機能のレポート
description: NIC の LSOV2 TCP パケット セグメンテーション機能のレポート
ms.assetid: 2894c1a8-503f-4b53-8eb3-5c5eaea150db
keywords:
- LSOV2 WDK ネットワーク
- 大きな TCP パケットのセグメント化 WDK ネットワーク
- 大きな TCP パケットの WDK ネットワー キングのセグメント化
- タスクのオフロード LSOV1 と LSOV2 の WDK TCP/IP トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5150d267a568552ce7c5813abd52853039cdf74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373280"
---
# <a name="reporting-a-nics-lsov2-tcp-packet-segmentation-capabilities"></a>NIC の LSOV2 TCP パケット セグメンテーション機能のレポート





NDIS ミニポート ドライバーが現在大量送信オフロード バージョン 2 (LSOV2) を指定では、NIC の構成を TCP パケットのセグメンテーションを[ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)構造体。ミニポート ドライバーでは、現在の LSOV2 構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数を[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

ミニポート ドライバーが存在する場合に LSOV2 構成では、変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態を示す値。

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)、NDIS には、NDIS が含まれています\_TCP\_LARGE\_送信\_オフロード\_V2 構造、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS を表す構造体、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

LSOV2 ハードウェアをサポートしているミニポート ドライバーが LSOV1 をサポートする必要がありますもことをお勧めします。 このサポートは、NDIS 5 の場合は、LSOV1 を使用する TCP/IP トランスポートを有効になります。*x*ミニポート アダプタ上で中間ドライバーがインストールされています。 LSOV1 機能に関する詳細については、次を参照してください。[レポート NIC の LSOV1 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)します。

LSOV2 には、IPv4 と IPv6 パケットがサポートされています。 ミニポート ドライバーは、IPv4 と IPv6 の両方に対して、次の情報を指定する必要があります、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)構造体。

-   カプセル化の設定で、**カプセル化**メンバー。 このメンバーの詳細については、「解説」セクションを参照してください。 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)します。

-   TCP/IP トランスポートは大きな TCP パケットの場合に、ミニポート ドライバーで渡すことができるユーザー データの最大バイト数、 **MaxOffLoadSize**メンバー。

-   TCP/IP トランスポート オフロードできますが、セグメント化の NIC にで前に、大きな TCP パケットがで割り切れるする必要があるセグメントの最小数、 **MinSegmentCount**メンバー。

## <a name="related-topics"></a>関連トピック


[タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)

 

 






