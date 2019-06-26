---
title: 電源管理用の必須およびオプションの OID
description: 電源管理用の必須およびオプションの OID
ms.assetid: 147e35b2-dfa5-4238-82e6-5c48ffa30af5
keywords:
- Oid WDK ネットワーク、電源管理
- ウェイク アップ機能 WDK ネットワー キング、Oid
- WDK の NDIS ミニポート、Oid の電源管理
- オブジェクト識別子の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2c474f158d0d0db475460ab8a26e383978fd73
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373226"
---
# <a name="required-and-optional-oids-for-power-management"></a>電源管理用の必須およびオプションの OID





ミニポート ドライバーでは、電源管理をサポートしている必要があります電源管理のオブジェクト識別子 (Oid) をサポートしています。 ミニポート ドライバーでのクエリと Oid にセットの処理方法の詳細については、次を参照してください。[取得と SettingMiniport ドライバー情報と、WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)します。

ミニポート ドライバーの電源管理のサポートのレベルは 2 つです。

1.  ミニポート ドライバーでは、電源の状態の間の遷移を行うネットワーク アダプターをサポートできます。 このサポートは、電源管理のサポートの最小レベルです。 ネットワーク アダプターのデバイスの電源状態の説明は、次を参照してください。[ネットワーク アダプターのデバイスの電源状態](device-power-states-for-network-adapters.md)します。

2.  1 つまたは複数のミニポート ドライバーもサポート[ネットワーク ウェイク アップ イベント](network-wake-up-events.md)します。

ミニポート ドライバーでは、初期化中に電源管理機能を報告します。 初期化中に報告される電源管理機能の詳細については、次を参照してください[ **NDIS\_ミニポート\_アダプター\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_attributes)と。関連する属性の構造体。

ミニポート ドライバーは、直接、または電源の状態の間の遷移をネットワーク アダプターの属性で、次の Oid をサポートする必要があります。

-   [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)

    中間ドライバーは、この OID クエリに応答する必要があります。 NDIS に応答する OID\_PNP\_機能の物理ネットワーク アダプターの代わりに要求します。 中間のドライバーでは、この OID に応答する方法の詳細については、次を参照してください。 [PnP イベントを処理し、中間のドライバーで電源管理イベント](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)します。

-   [OID\_PNP\_クエリ\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)

    この OID には、デバイスの電源状態が遷移するネットワーク アダプターを準備する必要がありますを指定します。 ミニポート ドライバーは、NDIS を返す必要があります常に\_状態\_OID のクエリに対する応答で成功\_PNP\_クエリ\_電源。 NDIS を返すことによって\_状態\_この OID への応答の成功を要求、ミニポート ドライバーでは、ネットワーク アダプターに後続の OID の受信時に指定したデバイスの電源状態に変わりますが保証されます\_PNP\_設定\_POWER 要求。 ミニポート ドライバーでは、ここでは、する必要があります何もしない移行を危険にさらし。

-   [OID\_PNP\_設定\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

    この OID は、ネットワーク アダプターが、指定されたデバイスの電源状態に移行する必要があることを示します。 ミニポート ドライバーは、ドライバーは、NDIS を返す前に、指定の状態へのネットワーク アダプターを設定する必要があります\_状態\_成功します。 ミニポート ドライバーは、NDIS を返す必要があります常に\_状態\_この OID への応答に成功します。 場合 OID\_PNP\_設定\_POWER ネットワーク アダプターを作業の電源の状態と設定、ミニポート ドライバー失敗がこの OID、NDIS は、デバイスが回復不能な状態であることを想定しています。

ネットワークのウェイク アップのイベントをサポートするために、ミニポート ドライバーをサポートする必要がありますも、 [OID\_PNP\_を有効にする\_WAKE\_を](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)OID。 プロトコル ドライバーおよび NDIS の両方は、この OID を使用して、ネットワーク アダプターのウェイク アップ機能を有効にします。 詳細については、次を参照してください。[ウェイク アップのイベントを有効にする](enabling-wake-up-events.md)します。

ネットワークのウェイク アップのフレームをサポートするために (を参照してください[ネットワーク ウェイク アップ イベント](network-wake-up-events.md))、ミニポート ドライバーは、ウェイク アップのイベントに関連する次の Oid もサポートする必要があります。

-   [OID\_PNP\_追加\_WAKE\_を\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)

    プロトコル ドライバーでは、この OID を使用して、ネットワーク アダプターのミニポート ドライバーまたはその両方で管理一覧にウェイク アップのパターンを追加します。

-   [OID\_PNP\_削除\_WAKE\_を\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)

    プロトコル ドライバーでは、この OID を使用して、以前に OID の指定、ウェイク アップ パターンを削除する\_PNP\_追加\_WAKE\_を\_パターン。

ネットワークのウェイク アップのイベントをサポートする NDIS ミニポート ドライバーではウェイク アップに関連する次の統計の Oid をサポートできます必要に応じてイベント。

-   [OID\_PNP\_WAKE\_を\_エラー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-error)

    プロトコル ドライバーでは、false ウェイク アップの見逃しミニポート ドライバーのネットワーク アダプターによって通知の数を決定するには、この OID をクエリします。

-   [OID\_PNP\_WAKE\_を\_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-ok)

    プロトコル ドライバーでは、有効なウェイク アップの見逃しミニポート ドライバーのネットワーク アダプターではシグナル状態の数を決定するには、この OID をクエリします。

 

 





