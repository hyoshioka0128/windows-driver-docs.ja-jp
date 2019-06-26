---
title: NIC の接続オフロード機能のレポート
description: NIC の接続オフロード機能のレポート
ms.assetid: a9bf798b-382c-4904-b0b2-ed1e54f9c36b
keywords:
- 接続は、WDK TCP/IP トランスポートは、レポート機能をオフロードします。
- レポート接続のオフロード機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6c5d7bbeecc5473ebc5f72225075aa2405f230
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373294"
---
# <a name="reporting-a-nics-connection-offload-capabilities"></a>NIC の接続オフロード機能のレポート





NDIS ミニポート ドライバーでは、NIC の現在の接続オフロードの構成を指定します、 [ **NDIS\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造体。 ミニポート ドライバーでの現在の接続オフロードの構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数を[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数を渡す、NDIS 情報\_ミニポート\_TCP\_接続\_オフロード\_属性。

ミニポート ドライバーでは、オフロード機能を接続の変更を報告する必要があります。 ドライバーは、スタックを一時停止し、状態を示す値を発行してアップロードするすべての接続を要求します。 (NDIS について\_状態\_オフロード\_一時停止を参照してください[完全な TCP オフロード](full-tcp-offload.md))。構成の変更が完了した後、ドライバーを再起動し、状態を示す値を発行してミニポート アダプターのオフロード機能を再クエリ スタックを要求します。 (NDIS について\_状態\_オフロード\_再開、完全な TCP オフロードを参照してください)。

クエリに対する応答で[OID\_TCP\_接続\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)、NDIS を返します、 [ **NDIS\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

オフロード機能の接続の指定の詳細についてでのオフロードのターゲットの初期化を参照してください、 [NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md)します。

 

 





