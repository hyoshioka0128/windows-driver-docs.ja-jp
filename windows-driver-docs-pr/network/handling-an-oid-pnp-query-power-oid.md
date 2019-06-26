---
title: OID_PNP_QUERY_POWER OID の処理
description: OID_PNP_QUERY_POWER OID の処理
ms.assetid: aec9393a-debb-41eb-a8a0-b3d1936d707b
keywords:
- OID_PNP_QUERY_POWER
- ネットワーク インターフェイス カード WDK ネットワーク、電源の状態遷移
- Nic の WDK ネットワーク、電源の状態遷移
- 電源管理 WDK NDIS ミニポート、電源の状態遷移
- デバイスの電源状態が WDK ネットワーク
- WDK ネットワークの状態を電源します。
- WDK のネットワークの状態遷移の電源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e25f95a384bd41e85af53143a6f508af3e79822
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379826"
---
# <a name="handling-an-oidpnpquerypower-oid"></a>OID の処理\_PNP\_クエリ\_POWER OID





[OID\_PNP\_クエリ\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power) OID は、ネットワーク アダプターを低電力状態に遷移できるかどうかを示すために、ミニポート ドライバーを要求します。 ミニポート ドライバーは、NDIS を返す必要があります常に\_状態\_OID のクエリに対する応答で成功\_PNP\_クエリ\_電源。 NDIS を返すことによって\_状態\_この oid の成功を要求、ミニポート ドライバーでは、ネットワーク アダプターに、後続の受信時に指定したデバイスの電源状態に変わりますが保証されます[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)要求。 ミニポート ドライバーでは、ここでは、する必要があります何もしない移行を危険にさらし。

[OID\_PNP\_クエリ\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)要求が常に続く OID\_PNP\_設定\_POWER 要求。 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) OID 要求の直後に\_PNP\_クエリ\_電源を要求または未指定の間隔で到着することができますOID 後\_PNP\_クエリ\_POWER 要求。 D0、OID で指定されているデバイスの状態\_PNP\_設定\_電源要求の場合は、上記の OID を効果的にキャンセル\_PNP\_クエリ\_POWER 要求。

 

 





