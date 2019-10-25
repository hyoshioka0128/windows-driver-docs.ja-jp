---
title: NIC の LSOV1 TCP パケット セグメンテーション機能のレポート
description: NIC の LSOV1 TCP パケット セグメンテーション機能のレポート
ms.assetid: 976f5943-a50e-413b-8520-e280b04122f9
keywords:
- LSOV1 WDK ネットワーク
- 大きな TCP パケットセグメント化 WDK ネットワーク
- 大きな TCP パケットのセグメンテーション (WDK ネットワーク)
- タスクオフロード WDK TCP/IP transport、LSOV1、および LSOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0795f42c6ae5e5c82d427e47c429c39d0eaaa56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842048"
---
# <a name="reporting-a-nics-lsov1-tcp-packet-segmentation-capabilities"></a>NIC の LSOV1 TCP パケット セグメンテーション機能のレポート





NDIS ミニポートドライバーでは、現在の large send offload バージョン 1 (LSOV1) を指定しています。これは、 [**ndis\_tcp\_large\_\_オフロード\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)構造を送信します。ミニポートドライバーには、 [**NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造の現在の LSOV1 オフロード構成が含まれている必要があります。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、NDIS\_ミニポート\_アダプター\_オフロード\_属性の情報を渡します。

ミニポートドライバーは、 [**NDIS\_status\_タスク\_オフロード\_現在\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態の表示にある場合に、LSOV1 構成の変更を報告する必要があります。

[\_現在の\_構成に対する OID\_tcp\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)のクエリへの応答として、ndis には[ **、ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) tcp\_、\_の\_が含まれます。ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーで返される構造体。 NDIS は、ミニポートドライバーによって提供された情報を使用します。

NDIS は、LSO の拡張バージョンである large send offload version 2 (LSOV2) をサポートしています。 LSOV2 機能の詳細については、「 [NIC の LSOV2 機能の報告](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)」を参照してください。

ミニポートドライバーでは、次の情報を NDIS\_TCP\_l\_送信\_オフロード\_V1 構造に指定する必要があります。

-   カプセル化の設定 (**カプセル化**メンバー内)。 このメンバーの詳細については、「 [**NDIS\_TCP\_LARGE\_SEND\_OFFLOAD\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)」の「解説」セクションを参照してください。

-   TCP/IP トランスポートが、 **Maxoffloadsize**メンバー内の大きな tcp パケットのミニポートドライバーに渡すことができるユーザーデータの最大バイト数。 最大サイズは64K バイトを超えることはできません。

-   TCP/IP トランスポートが、 **MinSegmentCount**メンバーのセグメント化のために NIC にオフロードできるようになるまでに、大きな tcp パケットが割り切れないセグメントの最小数。

-   TCP オプションを含む大きな TCP パケットを NIC が分割できるかどうか。

-   IPv4 オプションを含む大きな TCP パケットを NIC が分割できるかどうか。

## <a name="related-topics"></a>関連トピック


[タスクオフロード機能の決定](determining-task-offload-capabilities.md)

 

 






