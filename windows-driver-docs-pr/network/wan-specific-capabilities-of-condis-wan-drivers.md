---
title: CoNDIS WAN ドライバーの WAN 固有の機能
description: CoNDIS WAN ドライバーの WAN 固有の機能
ms.assetid: c4e8e0ae-7dd5-4c4e-900a-b1f7e5eecb16
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワークの非-WAN いる CoNDIS ドライバーとの比較
- 非-WAN いる CoNDIS ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2079dd4d442fc360a67c5d7075d7a7f083106d41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384345"
---
# <a name="wan-specific-capabilities-of-condis-wan-drivers"></a>CoNDIS WAN ドライバーの WAN 固有の機能





いる CoNDIS WAN ドライバーは、次のように、非-WAN いる CoNDIS ドライバーと異なります。

-   TAPI サービスをサポートしている CoNDIS WAN のドライバーを使用して、CO\_アドレス\_ファミリ\_TAPI\_プロキシ アドレス ファミリ。

-   いる CoNDIS WAN ドライバーでは、WAN に固有の Oid をサポートします。[OID\_WAN\_永続的な\_アドレス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561220(v=vs.85))、 [OID\_WAN\_現在\_アドレス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561200(v=vs.85))、および[OID\_WAN\_MEDIUM\_サブタイプ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561216(v=vs.85))します。

-   セットおよびクエリの特性を操作するには、いる CoNDIS WAN Oid のセットをサポートしている CoNDIS WAN ミニポート ドライバー。 いる CoNDIS WAN Oid の詳細については、次を参照してください。[いる CoNDIS WAN オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)します。

-   TAPI サービスを提供している CoNDIS WAN ミニポート ドライバーでは、セットおよびクエリの特性を操作している CoNDIS TAPI Oid のセットをサポートします。 いる CoNDIS TAPI Oid の詳細については、次を参照してください。 [Connection-Oriented NDIS の TAPI 拡張](https://docs.microsoft.com/windows-hardware/drivers/network/tapi-extension-oids-for-connection-oriented-ndis)します。

-   いる CoNDIS WAN ミニポート ドライバーでは、リンクの状態の変化を示す WAN に固有の状態インジケーターのセットをサポートします。 いる CoNDIS WAN ミニポート ドライバーの状態インジケーターの詳細については、次を参照してください。[を示すいる CoNDIS WAN ミニポート ドライバー ステータス](indicating-condis-wan-miniport-driver-status.md)します。

-   いる CoNDIS WAN ミニポート ドライバーでは、WAN に固有の一連の統計を保持します。 [OID\_WAN\_CO\_取得\_STATS\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info)OID は、統計情報を返す、ミニポート ドライバーを要求します。

-   いる CoNDIS WAN ミニポート ドライバーがすべてのパケットにループに戻ってを試行しないでください。NDISWAN は、ループバックのサポートを提供します。

 

 





