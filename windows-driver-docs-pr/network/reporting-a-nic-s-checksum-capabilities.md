---
title: NIC のチェックサム機能のレポート
description: NIC のチェックサム機能のレポート
ms.assetid: a90f8d01-8318-44de-acf0-7903ef7e85e0
keywords:
- タスクオフロード WDK TCP/IP トランスポート、チェックサムタスク
- チェックサムタスク (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f714960cf14af55d3848ade613fa69290bc4fae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842056"
---
# <a name="reporting-a-nics-checksum-capabilities"></a>NIC のチェックサム機能のレポート





NDIS ミニポートドライバーは、NIC が現在構成されているかどうかを報告するために、 [**ndis\_tcp\_ip\_チェックサム\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)構造体の IP、tcp、および UDP チェックサムを計算して検証します。 ミニポートドライバーには、 [**NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造の現在のチェックサムオフロード構成が含まれている必要があります。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、NDIS\_ミニポート\_アダプター\_オフロード\_属性の情報を渡します。

ミニポートドライバーでは、現在のチェックサムオフロード構成 (存在する場合) の変更を、 [**NDIS\_ステータス\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態表示に報告する必要があります。

[現在の\_CONFIG\_の OID\_tcp\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)のクエリに応答して、ndis には、NDIS\_[**オフ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)ロード構造にある NDIS\_TCP\_IP\_CHECKSUM\_オフロード構造が含まれています。Ndis は、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーでを返します。 NDIS は、ミニポートドライバーによって提供された情報を使用します。

ミニポートドライバーは、IPv4 および IPv6 の送受信パケットに関する次のチェックサム情報を示します。

-   NIC が送信パケットに対して計算できるチェックサム (IP、TCP、または UDP) の種類。受信パケットに対して検証できます。

-   カプセル化の設定 (**カプセル化**メンバー内)。 このメンバーの詳細については、「 [**NDIS\_TCP\_IP\_CHECKSUM\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)」の「解説」セクションを参照してください。

-   IP ヘッダーに IPv4 オプションが含まれているパケットのチェックサムを、NIC が計算または検証 (または計算および検証) できるかどうかを指定します。

-   IP ヘッダーに IPv6 拡張ヘッダーが含まれている IPv6 パケットのチェックサムを、NIC が計算または検証 (または計算および検証) できるかどうか。

-   Tcp ヘッダーに TCP オプションが含まれているパケットのチェックサムを、NIC が計算または検証 (または計算および検証) できるかどうかを指定します。

## <a name="related-topics"></a>関連トピック


[タスクオフロード機能の決定](determining-task-offload-capabilities.md)

 

 






