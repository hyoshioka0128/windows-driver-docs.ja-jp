---
title: 電源管理用の必須およびオプションの OID
description: 電源管理用の必須およびオプションの OID
ms.assetid: 147e35b2-dfa5-4238-82e6-5c48ffa30af5
keywords:
- Oid WDK ネットワーク、電源管理
- ウェイクアップ機能 WDK ネットワーク、Oid
- 電源管理 WDK NDIS ミニポート、Oid
- オブジェクト識別子 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad88bdb5161051bb3137f62377ae148ec6aa62e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842030"
---
# <a name="required-and-optional-oids-for-power-management"></a>電源管理用の必須およびオプションの OID





ミニポートドライバーの場合、電源管理をサポートするには、電源管理オブジェクト識別子 (Oid) をサポートする必要があります。 ミニポートドライバーがクエリを処理して Oid に設定する方法の詳細については、「[ミニポートドライバー情報の取得と設定」および「WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)」を参照してください。

ミニポートドライバーには、次の2つのレベルの電源管理サポートがあります。

1.  ミニポートドライバーは、電源状態を切り替えるためのネットワークアダプターをサポートできます。 このサポートは、最小レベルの電源管理サポートです。 ネットワークアダプターのデバイスの電源状態の説明については、「[ネットワークアダプターのデバイスの電源状態](device-power-states-for-network-adapters.md)」を参照してください。

2.  ミニポートドライバーは、1つまたは複数の[ネットワークウェイクアップイベント](network-wake-up-events.md)をサポートすることもできます。

ミニポートドライバーは、初期化中に電源管理機能を報告します。 初期化中に報告される電源管理機能の詳細については、「 [**NDIS\_ミニポート\_アダプターの\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)と関連属性の構造体」を参照してください。

ミニポートドライバーは、次の Oid を直接サポートしているか、ネットワークアダプターの属性で電源状態を切り替える必要があります。

-   [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)

    中間ドライバーは、この OID クエリに応答する必要があります。 NDIS は、物理ネットワークアダプターに代わって OID\_PNP\_機能の要求に応答します。 中間ドライバーでこの OID に応答する方法の詳細については、「[中間ドライバーでの PnP イベントと電源管理イベントの処理](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)」を参照してください。

-   [OID\_PNP\_クエリ\_の機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)

    この OID は、ネットワークアダプターの移行を準備するデバイスの電源状態を指定します。 ミニポートドライバーは、OID\_PNP\_クエリ\_パワーのクエリに応答して、常に NDIS\_STATUS\_SUCCESS を返す必要があります。 この OID 要求に応答して NDIS\_STATUS\_SUCCESS を返すことによって、ミニポートドライバーは、後続の OID\_PNP\_セットを受信したときに、ネットワークアダプターが指定されたデバイスの電源状態に移行することを保証\_電源要求。 この場合、ミニポートドライバーは、遷移を危険にさらすために何も行う必要はありません。

-   [OID\_PNP\_設定\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

    この OID は、ネットワークアダプターが、指定されたデバイスの電源状態に移行する必要があることを示します。 ミニポートドライバーは、ドライバーが NDIS\_STATUS\_SUCCESS を返す前に、ネットワークアダプターを指定された状態に設定する必要があります。 ミニポートドライバーは、この OID に対する応答として、常に NDIS\_STATUS\_SUCCESS を返す必要があります。 OID\_PNP\_\_設定すると、ネットワークアダプターが動作している電源状態に設定され、ミニポートドライバーがこの OID に失敗した場合、NDIS はデバイスが回復できない状態であると想定します。

ネットワークウェイクアップイベントをサポートするには、ミニポートドライバーで、 [\_ウェイク\_up oid を有効にするための oid\_PNP\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)もサポートする必要があります。 プロトコルドライバーと NDIS は、この OID を使用して、ネットワークアダプターのウェイクアップ機能を有効にします。 詳細については、「[ウェイクアップイベントの有効化](enabling-wake-up-events.md)」を参照してください。

ネットワークウェイクアップフレーム (「[ネットワークウェイクアップイベント](network-wake-up-events.md)」を参照) をサポートするには、ミニポートドライバーが、ウェイクアップイベントに関連する次の oid もサポートしている必要があります。

-   [OID\_PNP\_追加\_ウェイクアップ\_上\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)

    プロトコルドライバーは、この OID を使用して、ネットワークアダプターまたはミニポートドライバーのいずれかまたは両方を保持しているリストにウェイクアップパターンを追加します。

-   [OID\_PNP\_削除\_ウェイクアップ\_上\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)

    プロトコルドライバーは、この OID を使用して、以前に OID\_PNP で指定したウェイクアップパターンを削除し、\_WAKE\_UP\_パターン\_追加します。

ネットワークウェイクアップイベントをサポートする NDIS ミニポートドライバーでは、必要に応じて、ウェイクアップイベントに関連する次の統計的な Oid をサポートできます。

-   [OID\_PNP\_WAKE\_UP\_エラー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-error)

    プロトコルドライバーは、この OID を照会して、ミニポートドライバーのネットワークアダプターによって通知される偽ウェイクアップの数を特定します。

-   [OID\_PNP\_WAKE\_UP\_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-ok)

    プロトコルドライバーは、この OID を照会して、ミニポートドライバーのネットワークアダプターによって通知される有効なウェイクアップの数を判断します。

 

 





