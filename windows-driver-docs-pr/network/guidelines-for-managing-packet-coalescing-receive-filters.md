---
title: パケット結合受信フィルターを管理するためのガイドライン
description: パケット結合受信フィルターを管理するためのガイドライン
ms.assetid: 7FA44368-1641-478A-927B-020619F39A0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b14ec469f154efb5b78181465e97fd7e892c70b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842406"
---
# <a name="guidelines-for-managing-packet-coalescing-receive-filters"></a>パケット結合受信フィルターを管理するためのガイドライン


ミニポートドライバーで NDIS パケット合体がサポートされている場合は、次のガイドラインに従って、パケット合体受信フィルターを管理する必要があります。

-   ミニポートドライバーおよび基になるネットワークアダプターは、受信フィルターの設定とクリアを動的に処理できる必要があります。 個々の受信フィルターは、いつでも設定またはクリアできます。

-   ミニポートドライバーは、結合されたパケットカウンターを保持する必要があります。 この64ビットカウンターには、パケット合体フィルターに一致した受信パケットの数の値が含まれています。 NDIS は、oid [\_パケット\_結合\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-packet-coalescing-filter-match-count)を使用してこのカウンターを照会し、\_COUNT に一致\_します。

    [\_PNP\_\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された OID の oid 設定要求を処理することによって、ミニポートドライバーがフルパワー状態に移行するときに、このカウンターがクリアさ  ことを**確認**します。 ミニポートドライバーは、ミニ[*Portresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数が呼び出されたときにも、カウンターをクリアします。

     

-   低電力状態に移行する場合、ミニポートドライバーはパケット合体受信フィルターを破棄しないようにする必要があります。 ただし、ネットワークアダプターが低電力状態のときは、受信パケットをフィルター処理する必要があるのは、そのアダプターに対してオフロードされたウェイクアップパターンに基づいて、 [\_ウェイク\_up\_有効にする oid\_PNP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)の oid セット要求だけです。

    ミニポートドライバーは、アダプターがフルパワー状態に移行するときに、パケット合体受信フィルターを使用してネットワークアダプターを構成する必要があります。

-   NDIS がドライバーの[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を呼び出すと、ミニポートドライバーはパケット合体受信フィルターを破棄しないようにする必要があります。 ドライバーは、ネットワークアダプターをリセットした後、パケット合体フィルターを使用してアダプターを構成する必要があります。 また、ドライバーは、結合されたパケットカウンターを*クリアする必要があり*ます。

    ドライバーが*Addressingreset*パラメーターを TRUE に設定しているかどうかに関係なく、ミニポートドライバーはこの操作を実行**する  ます**。

     

-   ミニポートドライバーがネイティブ802.11 拡張ステーション (ExtSTA) モードで動作している場合、oid\_DOT11 の OID メソッド要求を処理するときに、パケット合体受信フィルターを破棄しないようにする必要があります[\_要求\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)。 ミニポートドライバーは802.11 リセット操作を実行した後、パケット合体受信フィルターを使用してネットワークアダプターを構成する必要があります。 また、ドライバーは、結合されたパケットカウンターをクリアしないように*する必要があり*ます。

    ネイティブ802.11 拡張ステーションモードの詳細については、「[拡張ステーションの操作モード](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/extensible-station-operation-mode)」を参照してください。

    **注**  NDIS では、拡張アクセスポイント (extap) モードで動作するネイティブ802.11 ミニポートドライバーのパケット合体はサポートされていません。 ExtAP 操作モードの詳細については、「[拡張アクセスポイント操作モード](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/extensible-access-point-operation-mode)」を参照してください。

     

 

 





