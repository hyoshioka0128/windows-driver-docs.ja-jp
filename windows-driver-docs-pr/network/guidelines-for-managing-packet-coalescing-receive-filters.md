---
title: パケット結合受信フィルターを管理するためのガイドライン
description: パケット結合受信フィルターを管理するためのガイドライン
ms.assetid: 7FA44368-1641-478A-927B-020619F39A0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5b610880fa65ed5284accf9967b5efa0b77c3b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369627"
---
# <a name="guidelines-for-managing-packet-coalescing-receive-filters"></a>パケット結合受信フィルターを管理するためのガイドライン


これらに従う必要があります、ミニポート ドライバーでは、NDIS パケットの結合をサポートする場合は、パケットの結合を管理するためのガイドラインは、フィルターを受信します。

-   ミニポート ドライバーと基になるネットワーク アダプターは、設定を処理できなければなりませんし、フィルターを動的に受信の消去します。 個別の受信フィルターを設定または、いつでもオフに可能性があります。

-   ミニポート ドライバーでは、結合されたパケット カウンターを維持する必要があります。 この 64 ビットのカウンターには、パケットの結合フィルターに一致した受信パケットの数の値が含まれています。 このカウンターの OID クエリ要求から、NDIS を照会[OID\_パケット\_COALESCING\_フィルター\_一致\_カウント](https://docs.microsoft.com/windows-hardware/drivers/network/oid-packet-coalescing-filter-match-count)します。

    **注**  ミニポート ドライバーの OID セット要求を処理することで電力状態に遷移するときにこのカウンターをクリアします[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)します。 ミニポート ドライバーでは、カウンターもクリアするときにその[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)関数が呼び出されます。

     

-   ミニポート ドライバーでは、パケットを破棄する必要があります低電力状態に遷移したときにフィルターが表示される結合します。 ただし、ネットワーク アダプターは、低電力状態では、する必要がありますの OID のセット要求を通じてアダプターにオフロードされがウェイク アップ パターンに基づいてのみのフィルターが受信したパケット[OID\_PNP\_を有効にする\_WAKE\_を](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)します。

    ミニポート ドライバーは、ネットワーク アダプターを構成する必要があります、パケットの結合と表示されるフィルター アダプターが電力状態に遷移します。

-   ミニポート ドライバーでは、パケットを破棄する必要があります NDIS ドライバーを呼び出すときにフィルターが表示される結合[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)関数。 ドライバーには、ネットワーク アダプターがリセットされ後、は、パケットの結合フィルターを使用してアダプターを構成にする必要があります。 また、ドライバー*をオフにする必要があります*まとめられたパケット カウンター。

    **注**  ミニポート ドライバーがドライバーを設定するかどうかに関係なく、この操作を実行する必要があります、 *AddressingReset*パラメーターを TRUE にします。

     

-   パケットが破棄する必要があります、ミニポート ドライバーは、ネイティブ 802.11 の拡張可能な局 (ExtSTA) モードで動作が場合の OID メソッド要求を処理する場合、フィルターが表示される結合[OID\_DOT11\_リセット\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)します。 ネットワーク アダプターを構成する必要があります、ミニポート ドライバーが 802.11 のリセット操作を実行した後、パケットの結合フィルターを受信します。 また、ドライバー*オフにする必要があります*まとめられたパケット カウンター。

    ネイティブの 802.11 の拡張可能なステーション モードの詳細については、次を参照してください。[ステーションの操作モードは拡張可能な](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/extensible-station-operation-mode)します。

    **注**  NDIS サポートしていないパケット結合拡張可能なアクセスで動作するネイティブの 802.11 ミニポート ドライバー (ExtAP) モードをポイントします。 ExtAP 操作モードの詳細については、次を参照してください。[拡張可能なアクセス ポイントの操作モード](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/extensible-access-point-operation-mode)します。

     

 

 





