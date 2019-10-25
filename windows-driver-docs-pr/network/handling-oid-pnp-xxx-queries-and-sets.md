---
title: OID_PNP_Xxx クエリと設定の処理
description: OID_PNP_Xxx クエリと設定の処理
ms.assetid: 2d5db7fb-2a27-4359-9d75-35939e72de69
keywords:
- OID_PNP_Xxx
- クエリ操作 WDK NDIS 中間
- set 操作 WDK NDIS 中間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee414f25f6a7efa668f15360842eee823fd5d50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842579"
---
# <a name="handling-oid_pnp_xxx-queries-and-sets"></a>OID\_PNP\_Xxx クエリとセットの処理





中間ドライバーの仮想ミニポートは、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数をエクスポートする必要があります。 NDIS は中間ドライバーの*Miniportoidrequest*関数を呼び出します。このとき、中間ドライバーの仮想ミニポートにバインドされているドライバーが、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して情報オブジェクト (OID\_*Xxx*) を照会または設定します。 また、NDIS は、その代わりに*Miniportoidrequest*を呼び出すこともできます。 設定および情報オブジェクトに対するクエリのミニポートドライバーの処理の詳細については、「[ミニポートドライバー情報の取得と設定」および「WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)」を参照してください。

中間ドライバーは、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数で受信した、基になるミニポートアダプターの機能に関する情報を保持する必要があります。 ミニポートアダプターが電源管理に対応していない場合、NDIS は、 [ **\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)を**NULL**にバインド\_、ndis の**PowerManagementCapabilities**メンバーを設定します。

中間ドライバーは、基になるミニポートドライバーによって管理される OID\_*Xxx*に対してクエリまたは設定を行うことができます。 これを行うには、 **NdisOidRequest**を使用します (中間ドライバーにコネクションレスの下端がある場合)。または、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を使用します (中間ドライバーに接続指向のエッジがある場合)。

中間ドライバーは、次のようにクエリとを処理する必要があります。

-   [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)

    この OID クエリに応答して、中間ドライバーは、基になる物理ミニポートアダプターの PnP 機能を報告する必要があります。 物理デバイスのミニポートアダプターは、この OID クエリを受信しないことに注意してください。

    中間ドライバーは、バインドパラメーターの基になるミニポートアダプターの PnP 機能を受け取ります。 中間ドライバーの使用目的に応じて、それを後続のドライバーに渡す必要があります。 中間ドライバーとミニポートドライバーは、ミニポートアダプターの属性の PnP 機能を報告します。 中間ドライバーは、基になるミニポートドライバーに対する OID\_PNP\_機能要求を発行しません。 基になるミニポートアダプターが電源管理に対応している場合は、NDIS\_PM\_WAKE\_UP\_CAPABILITIES 属性で、中間ドライバーはデバイスの**電源状態を指定する必要があります。** 各ウェイクアップ機能の NdisDeviceStateUnspecified:

    -   MinMagicPacketWakeUp
    -   Minpattern ウェイクアップ
    -   MinLinkChangeWakeUp

    このような設定は、中間ドライバーが電源管理に対応しているが、システムをウェイクアップできないことを示します。

-   [Oid\_pnp\_クエリ\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)と[oid\_pnp\_設定\_電力](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

    中間ドライバーは、常に NDIS\_の状態\_正常に返される必要があります\_クエリ\_POWER または一連の OID\_PNP\_設定\_POWER\_します。 中間ドライバーは、これらの OID 要求のいずれも、基になるミニポートドライバーに伝達しないようにする必要があります。

-   "ウェイクアップ Oid"

    基になる NIC が電源管理に対応している場合、中間ドライバーは、( **NdisOidRequest**または**NdisCoOidRequest**を呼び出すことによって) 基になるミニポートドライバーに渡す必要があります。これに関連する次の OID\_PNP\_*Xxx*です。ウェイクアップイベント:

    [\_\_ウェイクアップ\_を有効にする OID\_の PNP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)

    [OID\_PNP\_追加\_ウェイクアップ\_上\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)

    [OID\_PNP\_削除\_ウェイクアップ\_上\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)

    [OID\_PNP\_ウェイクアップ\_\_パターン\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-pattern-list)

    [OID\_PNP\_WAKE\_UP\_エラー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-error)

    [OID\_PNP\_WAKE\_UP\_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-ok)

中間ドライバーは、これらの Oid に対する基になるミニポートドライバーの応答も、プロトコルドライバーに伝達する必要があります。

基になるミニポートアダプターが電源管理に対応していない場合、ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の**PowerManagementCapabilities**メンバーを**NULL**に設定し、NDIS は、\_パラメーターを**NULL**に[**バインド\_、ndis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)の**PowerManagementCapabilities**メンバーを設定します。

基になるミニポートアダプターが電源管理に対応していない場合、中間ドライバーは、クエリまたはこれらの Oid のセットに応答して\_サポートされていない NDIS\_の状態\_返す必要があります。

 

 





