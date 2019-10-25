---
title: タスクオフロード機能の決定
description: タスクオフロード機能の決定
ms.assetid: 9348a595-7bc0-467e-aeaf-e23100c99524
keywords:
- タスクオフロード WDK TCP/IP トランスポート、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f30d33bb144f1790cc656f9fb0193ffea8a076
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838147"
---
# <a name="determining-task-offload-capabilities"></a>タスクオフロード機能の決定





NDIS は、NDIS 5.1 以前のタスクオフロードサービスの拡張形式であるタスクオフロードサービスをサポートしています。 接続のオフロード機能を確認する方法の詳細については、「[接続のオフロード機能の決定](determining-connection-offload-capabilities.md)」を参照してください。

NDIS は、負荷の軽減ハードウェア機能と、基になるミニポートアダプターの現在の構成を[**ndis\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体のプロトコルドライバーに提供します。 NDIS には、タスクのオフロードハードウェア機能と、基になるミニポートアダプターの現在の構成が用意されています。これにより、 [**ndis\_フィルター\_\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体にフィルターを適用できます。

管理アプリケーションは、オブジェクト識別子 (OID) クエリを使用して、ミニポートアダプターのタスクオフロード機能を取得します。 ただし、それ以上のドライバーは OID クエリを使用しないようにする必要があります。 プロトコルドライバーは、基になるドライバーが報告するタスクオフロード機能の変更を処理する必要があります。 ミニポートドライバーは、ステータスを示す状態のタスクオフロード機能の変更を報告できます。 ステータスの表示の一覧については、「 [NDIS 6.0 Tcp/ip オフロードの状態](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)の表示」を参照してください。

管理アプリケーション (またはそれ以降のドライバー) は、[現在の\_CONFIG oid\_の oid\_TCP\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)を照会することによって、ネットワークインターフェイスカード (NIC) の現在のタスクオフロード構成を特定できます。

[\_\_現在の\_CONFIG\_、OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)に関連付けられている[**NDIS\_offload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体は、次のように指定します。

-   TCP/IP トランスポートがサポートするタスクオフロードバージョンを含むヘッダー情報。

-   [**NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)構造体のチェックサムオフロード情報。

-   [**NDIS\_TCP\_\_大**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)規模な送信オフロードバージョン 1 (LSOV1) の情報は、\_オフロード\_V1 構造を送信ます。

-   [**NDIS\_ipsec\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)のインターネットプロトコルセキュリティ (ipsec) の情報は、V1 の\_V1 構造体をオフロードします。

-   NDIS\_TCP\_大規模な送信オフロードバージョン 2 (LSOV2) の情報は、 [ **\_オフロード\_V2 構造\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)します。

-   [**NDIS\_IPSEC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)のインターネットプロトコルセキュリティ (IPsecvOV) の情報は\_V2 構造体をオフロードします。

次のトピックには、オフロードサービスの種類ごとに固有の情報が含まれています。

-   [NIC のチェックサム機能の報告](reporting-a-nic-s-checksum-capabilities.md)
-   [NIC の LSOV1 の TCP パケットセグメント化機能の報告](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)
-   [NIC の LSOV2 の TCP パケットセグメント化機能の報告](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)
-   [NIC の IPsec 機能を報告する](reporting-a-nic-s-ipsec-capabilities.md)
    - \[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]

 

 





