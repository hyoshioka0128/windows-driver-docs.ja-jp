---
title: NIC の IPsec Offload Version 2 の機能のレポート
description: NIC の IPsec Offload Version 2 の機能のレポート
ms.assetid: 0ce5c42d-5c0c-4dfa-8a9f-a80c8924201d
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab959b80e4a03c609f8c19e6cf3cfceac2ec14b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373284"
---
# <a name="reporting-a-nics-ipsec-offload-version-2-capabilities"></a>NIC の IPsec Offload Version 2 の機能のレポート

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




IPsec オフロード バージョン 2 (IPsecOV2) を指定する、現在、NDIS 6.1 と以降のバージョンのミニポート ドライバー、機能するを指定しますまたは既定の構成では、NIC の、 [ **NDIS\_IPSEC\_オフロード\_V2。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)構造体。 ミニポート ドライバーが既定の IPsecOV2 構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数を[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

ミニポート ドライバーが存在する場合に IPsecOV2 機能、変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態を示す値。

**注**  NDIS NDIS 6.1 と以降のドライバーの直接の OID 要求インターフェイスを提供します。 [OID の直接の要求パス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)クエリを実行したり、頻繁に設定されている OID 要求をサポートします。

 

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)、NDIS には、NDIS が含まれています\_IPSEC\_オフロード\_V2構造体、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS を表す構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

 

 





