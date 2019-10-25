---
title: NIC の LSOV2 TCP パケット セグメンテーション機能のレポート
description: NIC の LSOV2 TCP パケット セグメンテーション機能のレポート
ms.assetid: 2894c1a8-503f-4b53-8eb3-5c5eaea150db
keywords:
- LSOV2 WDK ネットワーク
- 大きな TCP パケットセグメント化 WDK ネットワーク
- 大きな TCP パケットのセグメンテーション (WDK ネットワーク)
- タスクオフロード WDK TCP/IP transport、LSOV1、および LSOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3a7deeeeda1bd4910128ff6e2d1222a778ba83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842046"
---
# <a name="reporting-a-nics-lsov2-tcp-packet-segmentation-capabilities"></a>NIC の LSOV2 TCP パケット セグメンテーション機能のレポート





NDIS ミニポートドライバーは、\_Ndis 内の NIC の現在の large send offload version 2 (LSOV2) TCP パケットセグメント構成を指定します。 [**tcp\_large\_\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)構造を送信します。ミニポートドライバーには、 [**NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造の現在の LSOV2 構成が含まれている必要があります。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、NDIS\_ミニポート\_アダプター\_オフロード\_属性の情報を渡します。

ミニポートドライバーは、 [**NDIS\_status\_タスク\_オフロード\_現在\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態の表示にある場合に、LSOV2 構成の変更を報告する必要があります。

[\_現在の\_構成に対する OID\_tcp\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)のクエリへの応答として、ndis には[ **、ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) tcp\_、\_の\_が含まれます。ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーで返される構造体。 NDIS は、ミニポートドライバーによって提供された情報を使用します。

LSOV2 ハードウェアをサポートするミニポートドライバーでも LSOV1 がサポートされるようにすることをお勧めします。 このサポートにより、NDIS 5 の場合、TCP/IP トランスポートで LSOV1 を使用できるようになります。*x*中間ドライバーは、ミニポートアダプターにインストールされます。 LSOV1 機能の詳細については、「 [NIC の LSOV1 機能の報告](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)」を参照してください。

LSOV2 は、IPv4 および IPv6 パケットをサポートしています。 ミニポートドライバーでは、NDIS 内の IPv4 と IPv6 の両方について次の情報を指定する必要があります[ **\_TCP\_LARGE\_送信\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)構造体。

-   カプセル化の設定 (**カプセル化**メンバー内)。 このメンバーの詳細については、「 [**NDIS\_TCP\_LARGE\_SEND\_OFFLOAD\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)」の「解説」を参照してください。

-   TCP/IP トランスポートが、 **Maxoffloadsize**メンバー内の大きな tcp パケットのミニポートドライバーに渡すことができるユーザーデータの最大バイト数。

-   TCP/IP トランスポートが、 **MinSegmentCount**メンバーのセグメント化のために NIC にオフロードできるようになるまでに、大きな tcp パケットが割り切れないセグメントの最小数。

## <a name="related-topics"></a>関連トピック


[タスクオフロード機能の決定](determining-task-offload-capabilities.md)

 

 






