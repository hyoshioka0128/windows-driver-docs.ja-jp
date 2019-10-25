---
title: CoNDIS WAN ドライバーの WAN 固有の機能
description: CoNDIS WAN ドライバーの WAN 固有の機能
ms.assetid: c4e8e0ae-7dd5-4c4e-900a-b1f7e5eecb16
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、および非 WAN 接続ドライバー
- 非 WAN 接続ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee176336f933f34b74eea39586a072b3b57ed7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842936"
---
# <a name="wan-specific-capabilities-of-condis-wan-drivers"></a>CoNDIS WAN ドライバーの WAN 固有の機能





Conconwan ドライバーは、次のように、WAN 以外のドライバーとは異なります。

-   TAPI サービスをサポートする CoNDIS WAN ドライバーは、CO\_アドレス\_ファミリ\_TAPI\_プロキシアドレスファミリを使用します。

-   CoNDIS WAN ドライバーは、WAN 固有の Oid をサポートしています。 [oid\_wan\_永続的な\_アドレス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561220(v=vs.85))、 [oid\_wan\_現在の\_アドレス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561200(v=vs.85))、 [oid\_WAN\_MEDIUM\_のサブタイプ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561216(v=vs.85))です。

-   Condis WAN ミニポートドライバーは、一連の CoNDIS WAN Oid をサポートして、動作特性を設定および照会します。 CoNDIS WAN Oid の詳細については、「 [CONDIS Wan オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)」を参照してください。

-   TAPI サービスが提供する condis WAN ミニポートドライバーは、一連の condis TAPI Oid をサポートして、動作特性を設定および照会します。 CoNDIS TAPI Oid の詳細については、「 [Tapi Extensions For Connection 志向 NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/tapi-extension-oids-for-connection-oriented-ndis)」を参照してください。

-   CoNDIS WAN ミニポートドライバーでは、リンクのステータスの変化を示す一連の WAN 固有のステータスインジケーターがサポートされています。 CoNDIS WAN ミニポートドライバーの状態の表示の詳細については、「 [Wan ミニポートドライバーの状態](indicating-condis-wan-miniport-driver-status.md)を確認する」を参照してください。

-   CoNDIS WAN ミニポートドライバーは、WAN 固有の統計情報のセットを保持します。 [Oid\_WAN\_CO\_GET\_STATS\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info) oid は、統計情報を返すようにミニポートドライバーに要求します。

-   CoNDIS WAN ミニポートドライバーは、パケットのループバックを試行しません。NDISWAN では、ループバックがサポートされています。

 

 





