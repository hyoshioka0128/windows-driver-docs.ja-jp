---
title: NIC の接続オフロード機能のレポート
description: NIC の接続オフロード機能のレポート
ms.assetid: a9bf798b-382c-4904-b0b2-ed1e54f9c36b
keywords:
- 接続オフロード WDK TCP/IP トランスポート、レポート機能
- レポート接続のオフロード機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afe818385736c1926b6ecc73103452f85a41bf0c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842061"
---
# <a name="reporting-a-nics-connection-offload-capabilities"></a>NIC の接続オフロード機能のレポート





NDIS ミニポートドライバーは、 [**ndis\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造の NIC の現在の接続のオフロード構成を指定します。 ミニポートドライバーには、 [**NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造の現在の接続オフロード構成が含まれている必要があります。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、NDIS\_ミニポート\_TCP\_接続\_オフロード\_属性の情報を渡します。

ミニポートドライバーは、接続のオフロード機能の変更を報告する必要があります。 ドライバーは、状態の表示を発行することによって、一時停止し、すべての接続をアップロードするようにスタックに要求します。 (NDIS の\_ステータス\_オフロード\_一時停止の詳細については、「 [FULL TCP OFFLOAD](full-tcp-offload.md)」を参照してください)。構成の変更が完了すると、ドライバーはスタックを要求し、状態の表示を発行して、ミニポートアダプターのオフロード機能を再クエリします。 (NDIS の\_ステータス\_オフロード\_再開の詳細については、「Full TCP Offload」を参照してください)。

[\_現在の\_構成に対する OID\_tcp\_接続\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)のクエリに応答して、ndis は、情報バッファーに[**ndis\_tcp\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造を返します。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバー。 NDIS は、ミニポートドライバーによって提供された情報を使用します。

接続オフロード機能の指定の詳細については、「 [NDIS 6.0 TCP chimney オフロードのドキュメント](full-tcp-offload.md)」の「オフロードターゲットの初期化」を参照してください。

 

 





