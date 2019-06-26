---
title: OID_PNP_ADD_WAKE_UP_PATTERN
description: OID_PNP_ADD_WAKE_UP_PATTERN
ms.assetid: 96b95d1d-d557-4012-b95f-b1c43e2c590f
ms.date: 08/08/2017
keywords: -OID_PNP_ADD_WAKE_UP_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5d59e684e90a178ebc722c6875c02bcf05bc9f4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357729"
---
# <a name="oidpnpaddwakeuppattern"></a>OID\_PNP\_追加\_WAKE\_を\_パターン





OID\_PNP\_追加\_WAKE\_を\_ウェイク アップのパターンを指定するミニポート ドライバーにパターンの OID をプロトコル ドライバーによって送信されます。 によって、マスク、と共に、ウェイク アップのパターンが記載されている、 [ **NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造体。

ミニポート ドライバーのパターン マッチのウェイク アップを可能にするプロトコル (を参照してください[OID\_PNP\_を有効にする\_WAKE\_を](oid-pnp-enable-wake-up.md)) OID を使用して\_PNP\_の追加\_WAKE\_を\_パターン、ウェイク アップのパターンを指定します。 ホストのメモリまたはネットワーク アダプターの機能によって、ネットワーク アダプターにウェイク アップのパターンを格納できます。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、次が含まれています。

-   [ **NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)パターンとそのマスクについての情報を提供する構造体。

-   着信パケットのデータの量を示すマスク パターンに対応するバイト数と比較する必要があります。 マスクは、パケットの最初のバイトを開始します。 マスクの直後に、 [ **NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造体、 *InformationBuffer*します。 このマスクのしくみの詳細については、次を参照してください。、[ネットワーク デバイス クラスの電源管理の参照の仕様](https://go.microsoft.com/fwlink/p/?linkid=27255)します。

-   ウェイク アップ パターンでは、開始**PatternOffset**の先頭からのバイト、 *InformationBuffer*します。 ウェイク アップのパターンの詳細については、次を参照してください。、[ネットワーク デバイス クラスの電源管理の参照の仕様](https://go.microsoft.com/fwlink/p/?linkid=27255)します。

ウェイク アップ パターン プロトコルから受け入れることができる、ミニポート ドライバーの数、このようなパターンでは、または、ネットワーク アダプターで使用可能記憶域ミニポート ドライバーによって割り当てられたホストのメモリなどのリソースの可用性に依存します。 かどうか、ミニポート ドライバーは、リソース不足のため、ウェイク アップのパターンを追加できません、ミニポート ドライバーを返します**NDIS\_状態\_リソース**OID への応答で\_PNP\_の追加\_WAKE\_を\_パターン。

ミニポート ドライバーを返す必要があるかどうかプロトコル ドライバーは、重複するパターンを追加しようと、 **NDIS\_状態\_無効な\_データ**OID への応答で\_PNP\_の追加\_WAKE\_を\_パターン。

上端がこの OID 要求を受信する中間のドライバーする必要があります、呼び出すことによって、基になるミニポート ドライバーに要求を常に反映されるまで[ **NdisRequest** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff554681(v=vs.85))または[ **NdisCoRequest**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551877(v=vs.85))します。

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
<td><p>NDIS 6.0 および 6.1 NDIS でサポートされています。 NDIS 6.20 以降を使用して<a href="oid-pm-add-wol-pattern.md" data-raw-source="[OID_PM_ADD_WOL_PATTERN](oid-pm-add-wol-pattern.md)">OID_PM_ADD_WOL_PATTERN</a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID\_PM\_追加\_WOL\_パターン](oid-pm-add-wol-pattern.md)

 

 




