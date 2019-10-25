---
title: OID_PNP_WAKE_UP_PATTERN_LIST
description: OID_PNP_WAKE_UP_PATTERN_LIST
ms.assetid: 36e4243f-5df6-4231-b1e3-63fcb2e2ec04
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PNP_WAKE_UP_PATTERN_LIST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 5fc6dbcef75e41c260d9b08e355e747b2211e793
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844033"
---
# <a name="oid_pnp_wake_up_pattern_list"></a>OID\_PNP\_ウェイクアップ\_\_パターン\_一覧





OID\_PNP\_WAKE\_UP\_パターン\_LIST OID は、現在ミニポートドライバーのネットワークアダプターに設定されているウェイクアップパターンの一覧を照会するためにプロトコルによって使用されます。 プロトコルでは、 [\_ウェイクアップ\_up\_パターンを追加](oid-pnp-add-wake-up-pattern.md)することにより、OID\_\_PNP でウェイクアップパターンを指定します。

OID\_PNP\_WAKE\_UP\_パターン\_一覧は、ミニポートドライバーではなく NDIS によって処理されます。

NDIS は、ミニポートドライバーで設定されている各ウェイクアップパターンの説明をプロトコルに返します。 各ウェイクアップパターンは、そのマスクと共に、 [**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造によって記述されます。

各ウェイクアップパターンについて、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、次のものが含まれます。

-   \_パターンとそのマスクに関する情報を提供する、 [**NDIS\_PM\_パケットパターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造体。

-   受信パケットのうち、パターン内の対応するバイトと比較する必要があるバイトを示すマスク。 マスクは、パケットの最初のバイトで開始されます。 このマスクは、 **Informationbuffer**内の[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造の直後にあります。

-   ウェイクアップパターン。これは、 **Informationbuffer**の先頭からの**PatternOffset**バイトを開始します。

上端がこの OID 要求を受信する中間ドライバーは、Ndis (Co) 要求を呼び出すことによって、常に要求を基になるミニポートドライバーに伝達する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および6.1 でサポートされています。 NDIS 6.20 以降では、代わりに<a href="oid-pm-wol-pattern-list.md" data-raw-source="[OID_PM_WOL_PATTERN_LIST](oid-pm-wol-pattern-list.md)">OID_PM_WOL_PATTERN_LIST</a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_PM\_WOL\_パターン\_リスト](oid-pm-wol-pattern-list.md)

[OID\_PNP\_追加\_ウェイクアップ\_上\_パターン](oid-pnp-add-wake-up-pattern.md)

[OID\_PNP\_削除\_ウェイクアップ\_上\_パターン](oid-pnp-remove-wake-up-pattern.md)

 

 




