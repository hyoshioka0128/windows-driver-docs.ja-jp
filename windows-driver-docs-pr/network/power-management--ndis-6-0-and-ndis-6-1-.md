---
title: 電源管理 (NDIS 6.0 および NDIS 6.1)
description: 電源管理 (NDIS 6.0 および NDIS 6.1)
ms.assetid: 10CACB4E-BBC8-497F-9B54-810518B726A8
keywords:
- ミニポート ドライバー WDK ネットワーク、電源管理
- NDIS ミニポート ドライバー WDK、電源管理
- 電源管理の WDK ネットワー キング、ミニポート ドライバー
- 電源管理 WDK NDIS ミニポート
- 電源管理ミニポート ドライバーの電源管理についての WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf4cce87afac49cffd4ebaf7856eb857551efb6a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384538"
---
# <a name="power-management-ndis-60-and-ndis-61"></a>電源管理 (NDIS 6.0 および NDIS 6.1)





このセクションでは、Windows XP および NDIS 5.1 で導入された NDIS 電源管理のインターフェイスについて説明します。 この電源管理のインターフェイスは、次のバージョンの NDIS でサポートされています。

-   NDIS 5.1 (Windows XP)

-   NDIS 6.0 および以降のバージョンの NDIS (Windows Vista および Windows の以降のバージョン)

このセクションについて説明します。

-   NDIS ミニポート ドライバーの NDIS を提供する電源管理サービス。

-   電源管理をサポートするためのミニポート ドライバーの要件。

-   NDIS がネットワーク アダプター、電源ポリシーを設定する方法。

ここでは、次のトピックについて説明します。

[電源管理のための必須および省略可能な Oid](required-and-optional-oids-for-power-management.md)

[ネットワーク アダプターのデバイスの電源の状態](device-power-states-for-network-adapters.md)

[ネットワークのウェイク アップ イベント](network-wake-up-events.md)

[OID の処理\_PNP\_クエリ\_POWER OID](handling-an-oid-pnp-query-power-oid.md)

[OID の処理\_PNP\_設定\_POWER OID](handling-an-oid-pnp-set-power-oid.md)

[ギガビット イーサネット ネットワーク アダプターの電源管理の考慮事項](power-management-considerations-for-gigabit-ethernet-network-adapters.md)

[古いミニポート ドライバーの電源管理](power-management-for-old-miniport-drivers.md)

[NDIS がネットワーク アダプター、電源ポリシーを設定する方法](how-ndis-sets-the-power-policy-for-a-network-adapter.md)

[NDIS 電源管理の問題を回避](avoiding-ndis-power-management-problems.md)

**注**  以降 NDIS 6.20 が動作では、NDIS 電源管理のインターフェイスが改訂され拡張します。 電源管理をサポートする NDIS 6.20 ミニポート ドライバーを開発している場合は、内の情報を確認してください[(NDIS 6.20 以降) の電源管理](https://docs.microsoft.com/windows-hardware/drivers/network/power-management--ndis-6-20-)します。 電源管理をサポートする NDIS 6.30 ミニポート ドライバーを開発している場合は、内の情報を確認してください[(NDIS 6.30 以降) の電源管理](https://docs.microsoft.com/windows-hardware/drivers/network/power-management--ndis-6-30-)します。

 

 

 





