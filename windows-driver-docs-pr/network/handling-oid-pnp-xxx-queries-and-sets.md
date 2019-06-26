---
title: OID_PNP_Xxx クエリと設定の処理
description: OID_PNP_Xxx クエリと設定の処理
ms.assetid: 2d5db7fb-2a27-4359-9d75-35939e72de69
keywords:
- OID_PNP_Xxx
- クエリ操作 WDK NDIS 中間
- WDK NDIS 中間の設定操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a0800e9d7d5edc9bc2a320c267f91ed2a3c3077
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379790"
---
# <a name="handling-oidpnpxxx-queries-and-sets"></a>OID の処理\_PNP\_Xxx クエリとセット





中間のドライバーの仮想ミニポートをエクスポートする必要があります、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数。 NDIS ドライバーの中間の呼び出し*MiniportOidRequest*関数の場合、中間のドライバーのミニポート仮想呼び出しにバインドされている上位のドライバー [ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)クエリまたはオブジェクトの情報を設定する (OID\_*Xxx*)。 NDIS は呼び出すことができますも*MiniportOidRequest*独自の代わりにします。 セットとオブジェクトの情報をクエリのミニポート ドライバーの処理の詳細については、次を参照してください。[取得し、ミニポート ドライバー情報の設定と、WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)します。

中間のドライバーが、基になるミニポート アダプターで受信するの機能に関する情報を保持する必要があります、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数。 ミニポート アダプタの管理に対応した電源は、NDIS 設定、**デバイス**のメンバー [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)に**NULL**します。

中間のドライバーの照会または OID を設定できます\_*Xxx*基になるミニポート ドライバーによって保持されています。 これは、これを**NdisOidRequest**(かどうか、中間のドライバーがコネクションレスの下端)、または[ **NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)(中間のドライバーがある場合、接続指向下端)。

中間のドライバーは、次のようにクエリとセット処理する必要があります。

-   [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)

    この OID クエリに応答して、中間ドライバーは、基になる物理ミニポート アダプタの PnP 機能をレポートする必要があります。 物理デバイスに対してミニポート アダプターがこの OID クエリを受け取らないに注意してください。

    中間のドライバーでは、バインド パラメーターの基になるミニポート アダプタの PnP 機能を受信します。 中間ドライバーの使用目的に適したドライバーをスライドに渡すする必要があります。 中間およびミニポートのドライバーは、ミニポート アダプター属性での PnP 機能を報告します。 中間のドライバーは、OID を発行しません\_PNP\_基になるミニポート ドライバーへの機能要求。 基になるミニポート アダプターが電源管理対応では、ndis\_PM\_WAKE\_を\_仮想ミニポート属性の機能を構成、中間のドライバーがデバイスの電源を指定する必要があります状態の**NdisDeviceStateUnspecified**ウェイク アップ機能ごと。

    -   MinMagicPacketWakeUp
    -   MinPatternWakeUp
    -   MinLinkChangeWakeUp

    このような設定は、中間ドライバーが電源管理に対応したが、システムをスリープ解除できないことを示します。

-   [OID\_PNP\_クエリ\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)と[OID\_PNP\_設定\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

    中間のドライバーは、NDIS を返す必要があります常に\_状態\_OID のクエリに成功\_PNP\_クエリ\_電源または一連の OID\_PNP\_設定\_電源。 中間のドライバーでは、基になるミニポート ドライバーにこれらの OID 要求のいずれかの反映されませんする必要があります。

-   "ウェイク アップ Oid"

    中間のドライバーが基になるミニポート ドライバーに渡す必要があります、基になる NIC が電源管理対応の場合は、(呼び出して**NdisOidRequest**または**NdisCoOidRequest**) 次の OID\_PNP\_*Xxx*ウェイク アップに関連したイベント。

    [OID\_PNP\_を有効にする\_WAKE\_を](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)

    [OID\_PNP\_追加\_WAKE\_を\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)

    [OID\_PNP\_削除\_WAKE\_を\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)

    [OID\_PNP\_WAKE\_を\_パターン\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-pattern-list)

    [OID\_PNP\_WAKE\_を\_エラー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-error)

    [OID\_PNP\_WAKE\_を\_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-ok)

中間ドライバーでは、上位のプロトコル ドライバーにこれらの Oid を基になるミニポート ドライバーの応答も反映する必要があります。

場合は、基になるミニポート アダプタの管理に対応した電源は、ミニポート ドライバーの設定、**デバイス**のメンバー [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)に**NULL**と NDIS セット、**デバイス**のメンバー [**NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)に**NULL**します。

中間ドライバーが NDIS を返す場合は、基になるミニポート アダプターの管理に対応した電源は、\_状態\_いない\_クエリまたはこれらの Oid のセットへの応答でサポートされています。

 

 





