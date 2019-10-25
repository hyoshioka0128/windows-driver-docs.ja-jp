---
title: OID_PNP_REMOVE_WAKE_UP_PATTERN
description: OID_PNP_REMOVE_WAKE_UP_PATTERN
ms.assetid: 493019d0-9cd9-4712-8d18-5ee0264be9e1
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PNP_REMOVE_WAKE_UP_PATTERN ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 171a27315d3b488cff94bb2974905b7584c9cb30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844038"
---
# <a name="oid_pnp_remove_wake_up_pattern"></a>OID\_PNP\_削除\_ウェイクアップ\_上\_パターン





OID\_PNP\_REMOVE\_WAKE\_UP\_PATTERN OID は、以前に Oid\_PNP で受信したウェイクアップパターンを削除するようにミニポートドライバーに要求し\_[wake\_up\_追加します。パターン](oid-pnp-add-wake-up-pattern.md)要求を\_しています。 ウェイクアップパターンは、そのマスクと共に、 [**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造によって記述されます。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、次のものが含まれています。

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
<td><p>NDIS 6.0 および6.1 でサポートされています。 NDIS 6.20 以降では、代わりに<a href="oid-pm-remove-wol-pattern.md" data-raw-source="[OID_PM_REMOVE_WOL_PATTERN](oid-pm-remove-wol-pattern.md)">OID_PM_REMOVE_WOL_PATTERN</a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID\_PNP\_追加\_ウェイクアップ\_上\_パターン](oid-pnp-add-wake-up-pattern.md)

[OID\_PM\_\_WOL\_パターンの削除](oid-pm-remove-wol-pattern.md)

 

 




