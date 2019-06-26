---
title: NIC の LSOV1 TCP パケット セグメンテーション機能のレポート
description: NIC の LSOV1 TCP パケット セグメンテーション機能のレポート
ms.assetid: 976f5943-a50e-413b-8520-e280b04122f9
keywords:
- LSOV1 WDK ネットワーク
- 大きな TCP パケットのセグメント化 WDK ネットワーク
- 大きな TCP パケットの WDK ネットワー キングのセグメント化
- タスクのオフロード LSOV1 と LSOV2 の WDK TCP/IP トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08b54c9f2255bde987d219c91b21b51eda685aa0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373273"
---
# <a name="reporting-a-nics-lsov1-tcp-packet-segmentation-capabilities"></a>NIC の LSOV1 TCP パケット セグメンテーション機能のレポート





NDIS ミニポート ドライバーが現在の大量送信オフロード バージョン 1 (LSOV1) を指定します - TCP パケットのセグメント化の構成では、NIC の[ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)構造体。ミニポート ドライバーで現在 LSOV1 オフロードの構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数を[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

ミニポート ドライバーが存在する場合に LSOV1 構成では、変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態を示す値。

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)、NDIS には、NDIS が含まれています\_TCP\_LARGE\_送信\_オフロード\_V1 構造、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS を表す構造体、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

NDIS サポートする多数の送信は、LSO の拡張のバージョンは、バージョン 2 (LSOV2) をオフロードします。 LSOV2 機能に関する詳細については、次を参照してください。[レポート NIC の LSOV2 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)します。

ミニポート ドライバーは、NDIS で、次の情報を指定する必要があります\_TCP\_LARGE\_送信\_オフロード\_V1 構造体。

-   カプセル化の設定で、**カプセル化**メンバー。 このメンバーの詳細については、「解説」セクションを参照してください。 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)します。

-   TCP/IP トランスポートは大きな TCP パケットの場合に、ミニポート ドライバーで渡すことができるユーザー データの最大バイト数、 **MaxOffLoadSize**メンバー。 最大サイズは 64 K バイトを超えることはできません。

-   TCP/IP トランスポート オフロードできますが、セグメント化の NIC にで前に、大きな TCP パケットがで割り切れるする必要があるセグメントの最小数、 **MinSegmentCount**メンバー。

-   かどうか、NIC は、TCP オプションを含む大きな TCP パケットを分割することができます。

-   かどうか、NIC は、IPv4 のオプションを含む大きな TCP パケットを分割することができます。

## <a name="related-topics"></a>関連トピック


[タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)

 

 






