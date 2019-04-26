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
ms.openlocfilehash: e031ed48a5b2d36cd1d2951cb65d6d699864031e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349695"
---
# <a name="handling-oidpnpxxx-queries-and-sets"></a>OID の処理\_PNP\_Xxx クエリとセット





中間のドライバーの仮想ミニポートをエクスポートする必要があります、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数。 NDIS ドライバーの中間の呼び出し*MiniportOidRequest*関数の場合、中間のドライバーのミニポート仮想呼び出しにバインドされている上位のドライバー [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)クエリまたはオブジェクトの情報を設定する (OID\_*Xxx*)。 NDIS は呼び出すことができますも*MiniportOidRequest*独自の代わりにします。 セットとオブジェクトの情報をクエリのミニポート ドライバーの処理の詳細については、次を参照してください。[取得し、ミニポート ドライバー情報の設定と、WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)します。

中間のドライバーが、基になるミニポート アダプターで受信するの機能に関する情報を保持する必要があります、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。 ミニポート アダプタの管理に対応した電源は、NDIS 設定、**デバイス**のメンバー [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)に**NULL**します。

中間のドライバーの照会または OID を設定できます\_*Xxx*基になるミニポート ドライバーによって保持されています。 これは、これを**NdisOidRequest**(かどうか、中間のドライバーがコネクションレスの下端)、または[ **NdisCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561711)(中間のドライバーがある場合、接続指向下端)。

中間のドライバーは、次のようにクエリとセット処理する必要があります。

-   [OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)

    この OID クエリに応答して、中間ドライバーは、基になる物理ミニポート アダプタの PnP 機能をレポートする必要があります。 物理デバイスに対してミニポート アダプターがこの OID クエリを受け取らないに注意してください。

    中間のドライバーでは、バインド パラメーターの基になるミニポート アダプタの PnP 機能を受信します。 中間ドライバーの使用目的に適したドライバーをスライドに渡すする必要があります。 中間およびミニポートのドライバーは、ミニポート アダプター属性での PnP 機能を報告します。 中間のドライバーは、OID を発行しません\_PNP\_基になるミニポート ドライバーへの機能要求。 基になるミニポート アダプターが電源管理対応では、ndis\_PM\_WAKE\_を\_仮想ミニポート属性の機能を構成、中間のドライバーがデバイスの電源を指定する必要があります状態の**NdisDeviceStateUnspecified**ウェイク アップ機能ごと。

    -   MinMagicPacketWakeUp
    -   MinPatternWakeUp
    -   MinLinkChangeWakeUp

    このような設定は、中間ドライバーが電源管理に対応したが、システムをスリープ解除できないことを示します。

-   [OID\_PNP\_クエリ\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569778)と[OID\_PNP\_設定\_電源](https://msdn.microsoft.com/library/windows/hardware/ff569780)

    中間のドライバーは、NDIS を返す必要があります常に\_状態\_OID のクエリに成功\_PNP\_クエリ\_電源または一連の OID\_PNP\_設定\_電源。 中間のドライバーでは、基になるミニポート ドライバーにこれらの OID 要求のいずれかの反映されませんする必要があります。

-   "ウェイク アップ Oid"

    中間のドライバーが基になるミニポート ドライバーに渡す必要があります、基になる NIC が電源管理対応の場合は、(呼び出して**NdisOidRequest**または**NdisCoOidRequest**) 次の OID\_PNP\_*Xxx*ウェイク アップに関連したイベント。

    [OID\_PNP\_を有効にする\_WAKE\_を](https://msdn.microsoft.com/library/windows/hardware/ff569775)

    [OID\_PNP\_追加\_WAKE\_を\_パターン](https://msdn.microsoft.com/library/windows/hardware/ff569773)

    [OID\_PNP\_削除\_WAKE\_を\_パターン](https://msdn.microsoft.com/library/windows/hardware/ff569779)

    [OID\_PNP\_WAKE\_を\_パターン\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569783)

    [OID\_PNP\_WAKE\_を\_エラー](https://msdn.microsoft.com/library/windows/hardware/ff569781)

    [OID\_PNP\_WAKE\_を\_OK](https://msdn.microsoft.com/library/windows/hardware/ff569782)

中間ドライバーでは、上位のプロトコル ドライバーにこれらの Oid を基になるミニポート ドライバーの応答も反映する必要があります。

場合は、基になるミニポート アダプタの管理に対応した電源は、ミニポート ドライバーの設定、**デバイス**のメンバー [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)に**NULL**と NDIS セット、**デバイス**のメンバー [**NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)に**NULL**します。

中間ドライバーが NDIS を返す場合は、基になるミニポート アダプターの管理に対応した電源は、\_状態\_いない\_クエリまたはこれらの Oid のセットへの応答でサポートされています。

 

 





