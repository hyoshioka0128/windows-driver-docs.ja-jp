---
title: OID_PNP_REMOVE_WAKE_UP_PATTERN
description: OID_PNP_REMOVE_WAKE_UP_PATTERN
ms.assetid: 493019d0-9cd9-4712-8d18-5ee0264be9e1
ms.date: 08/08/2017
keywords: -OID_PNP_REMOVE_WAKE_UP_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a995266d6c0ecfeafe8d4b5f29064bf229c3ed43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356135"
---
# <a name="oidpnpremovewakeuppattern"></a>OID\_PNP\_削除\_WAKE\_を\_パターン





OID\_PNP\_削除\_WAKE\_を\_パターンの OID が以前に受信したウェイク アップのパターンを削除するミニポート ドライバーを要求する[OID\_PNP\_追加\_WAKE\_を\_パターン](oid-pnp-add-wake-up-pattern.md)要求。 によって、マスク、と共に、ウェイク アップのパターンが記載されている、 [ **NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造体。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、次が含まれています。

-   [ **NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)パターンとそのマスクについての情報を提供する構造体。

-   着信パケットのデータの量を示すマスク パターンに対応するバイト数と比較する必要があります。 マスクは、パケットの最初のバイトを開始します。 マスクの直後に、 [ **NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造体、 **InformationBuffer**します。

-   ウェイク アップ パターンでは、開始**PatternOffset**の先頭からのバイト、 **InformationBuffer**します。

上端がこの OID 要求を受信する中間のドライバーは、Ndis (Co) 要求を呼び出すことによって、基になるミニポート ドライバーに要求を伝達する必要があります常にします。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および 6.1 ではサポートされています。 NDIS 6.20 以降を使用して<a href="oid-pm-remove-wol-pattern.md" data-raw-source="[OID_PM_REMOVE_WOL_PATTERN](oid-pm-remove-wol-pattern.md)">OID_PM_REMOVE_WOL_PATTERN</a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID\_PNP\_追加\_WAKE\_を\_パターン](oid-pnp-add-wake-up-pattern.md)

[OID\_PM\_削除\_WOL\_パターン](oid-pm-remove-wol-pattern.md)

 

 




