---
title: OID_PNP_WAKE_UP_PATTERN_LIST
description: OID_PNP_WAKE_UP_PATTERN_LIST
ms.assetid: 36e4243f-5df6-4231-b1e3-63fcb2e2ec04
ms.date: 08/08/2017
keywords: -OID_PNP_WAKE_UP_PATTERN_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 423600aae56ab222fba6139c3eadb0c59d80e1ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385239"
---
# <a name="oidpnpwakeuppatternlist"></a>OID\_PNP\_WAKE\_を\_パターン\_一覧





OID\_PNP\_WAKE\_を\_パターン\_一覧 OID が現在設定されて、ミニポート ドライバーのネットワーク アダプターにウェイク アップ パターンの一覧を照会する、プロトコルで使用します。 プロトコルでウェイク アップ パターンを指定する[OID\_PNP\_追加\_WAKE\_を\_パターン](oid-pnp-add-wake-up-pattern.md)します。

OID\_PNP\_WAKE\_を\_パターン\_一覧は、NDIS ミニポート ドライバーではなくによって処理されます。

NDIS は、プロトコルにウェイク アップのパターンがミニポート ドライバーの設定ごとの説明を返します。 によって、マスク、と共に各ウェイク アップ パターンが記載されている、 [ **NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造体。

ウェイク アップ パターンごとに、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、次が含まれています。

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
<td><p>NDIS 6.0 および 6.1 ではサポートされています。 NDIS 6.20 以降を使用して<a href="oid-pm-wol-pattern-list.md" data-raw-source="[OID_PM_WOL_PATTERN_LIST](oid-pm-wol-pattern-list.md)">OID_PM_WOL_PATTERN_LIST</a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[OID\_PM\_WOL\_パターン\_一覧](oid-pm-wol-pattern-list.md)

[OID\_PNP\_追加\_WAKE\_を\_パターン](oid-pnp-add-wake-up-pattern.md)

[OID\_PNP\_削除\_WAKE\_を\_パターン](oid-pnp-remove-wake-up-pattern.md)

 

 




