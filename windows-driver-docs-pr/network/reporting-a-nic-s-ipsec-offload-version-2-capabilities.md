---
title: NIC の IPsec Offload Version 2 の機能のレポート
description: NIC の IPsec Offload Version 2 の機能のレポート
ms.assetid: 0ce5c42d-5c0c-4dfa-8a9f-a80c8924201d
keywords:
- IPsecOV2 WDK TCP/IP transport, 機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0074ae518e92e3344491615890554889a29032f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842051"
---
# <a name="reporting-a-nics-ipsec-offload-version-2-capabilities"></a>NIC の IPsec Offload Version 2 の機能のレポート

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




IPsec オフロードバージョン 2 (IPsecOV2) の機能を指定するために、NDIS 6.1 以降のミニポートドライバーは、 [**ndis\_IPsec\_オフロード\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)構造体の NIC の現在または既定の構成を指定します。 ミニポートドライバーには、 [**NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造の既定の IPsecOV2 構成が含まれている必要があります。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、NDIS\_ミニポート\_アダプター\_オフロード\_属性の情報を渡します。

ミニポートドライバーは、IPsecOV2 機能がある場合は、 [**NDIS\_ステータス\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)の状態を示している場合に、その変更を報告する必要があります。

**  ndis**は、ndis 6.1 以降のドライバー用の直接 OID 要求インターフェイスを提供します。 [直接 oid 要求パス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)は、クエリまたは頻繁に設定される oid 要求をサポートしています。

 

[\_現在の\_構成に対する OID\_TCP\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)のクエリへの応答として、ndis には ndis\_の[**oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーに含まれる ndis\_[**OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体に、ndis\_IPSEC\_offload 構造体が含まれています。\_ NDIS は、ミニポートドライバーによって提供された情報を使用します。

 

 





