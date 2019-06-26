---
title: NIC のチェックサム機能のレポート
description: NIC のチェックサム機能のレポート
ms.assetid: a90f8d01-8318-44de-acf0-7903ef7e85e0
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、チェックサム タスク
- チェックサム タスク WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e18d68432d9cc7f60d967c49318c0a808b5aed9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373295"
---
# <a name="reporting-a-nics-checksum-capabilities"></a>NIC のチェックサム機能のレポート





NDIS ミニポート ドライバーは、NIC が計算しでの IP、TCP、および UDP チェックサムの検証に現在構成されているかどうかを報告する[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)構造体。 ミニポート ドライバーで現在のチェックサム オフロードの構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数を[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

存在する場合、ミニポート ドライバーは現在のチェックサム オフロードの構成の変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_構成** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態を示す値。

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)、NDIS には、NDIS が含まれています\_TCP\_IP\_チェックサム\_オフロード構造、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS を表す構造体、 **InformationBuffer**のメンバー、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

ミニポート ドライバーは、IPv4 と IPv6 の送信および受信パケット、次のチェックサム情報を示します。

-   NIC を選択し、送信パケットを計算できますを検証できるチェックサム (IP、TCP または UDP) の型は、パケットを受信します。

-   カプセル化の設定で、**カプセル化**メンバー。 このメンバーの詳細については、「解説」セクションを参照してください。 [ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)します。

-   できるかどうか、NIC を計算または検証 (または計算検証) パケットのチェックサムが IP ヘッダーは、IPv4 のオプションを含めます。

-   できるかどうか、NIC を計算または検証 (または計算検証)、IPv6 パケットのチェックサムが IP ヘッダーは、IPv6 拡張ヘッダーを含めます。

-   NIC できますを計算または検証 (または計算し、検証) パケットのチェックサムかどうかを TCP ヘッダーには TCP オプションが含まれます。

## <a name="related-topics"></a>関連トピック


[タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)

 

 






