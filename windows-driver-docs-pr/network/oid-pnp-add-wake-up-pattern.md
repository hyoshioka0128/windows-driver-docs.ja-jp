---
title: OID_PNP_ADD_WAKE_UP_PATTERN
description: OID_PNP_ADD_WAKE_UP_PATTERN
ms.assetid: 96b95d1d-d557-4012-b95f-b1c43e2c590f
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PNP_ADD_WAKE_UP_PATTERN ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 41425f07f43e4d8f17747f1ffc98cfa817c6574d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844043"
---
# <a name="oid_pnp_add_wake_up_pattern"></a>OID\_PNP\_追加\_ウェイクアップ\_上\_パターン





\_ウェイクアップパターンを指定するために、WAKE\_UP\_パターン OID を追加する OID\_PNP\_、ミニポートドライバーに送信されます。 ウェイクアップパターンは、そのマスクと共に、 [**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造によって記述されます。

ミニポートドライバーに対してパターン一致のウェイクアップを有効にするプロトコル ( [\_\_ウェイク\_up を有効にする oid\_](oid-pnp-enable-wake-up.md)を参照してください) OID\_pnp を使用し\_ウェイクアップパターンを指定するために\_wake\_UP\_を追加します。 ウェイクアップパターンは、ネットワークアダプターの機能に応じて、ホストメモリまたはネットワークアダプターに格納できます。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、次のものが含まれています。

-   \_パターンとそのマスクに関する情報を提供する、 [**NDIS\_PM\_パケットパターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造体。

-   受信パケットのうち、パターン内の対応するバイトと比較する必要があるバイトを示すマスク。 マスクは、パケットの最初のバイトで開始されます。 このマスクは、 *Informationbuffer*内の[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)構造の直後にあります。 このマスクのしくみの詳細については、「[ネットワークデバイスクラスの電源管理のリファレンス仕様](https://go.microsoft.com/fwlink/p/?linkid=27255)」を参照してください。

-   ウェイクアップパターン。これは、 *Informationbuffer*の先頭からの**PatternOffset**バイトを開始します。 ウェイクアップパターンの詳細については、「[ネットワークデバイスクラスの電源管理のリファレンス仕様](https://go.microsoft.com/fwlink/p/?linkid=27255)」を参照してください。

ミニポートドライバーがプロトコルから受け入れることができるウェイクアップパターンの数は、そのようなパターンに対してミニポートドライバーが割り当てたホストメモリや、ネットワークアダプターで使用可能な記憶域など、リソースの可用性によって異なる場合があります。 リソース不足のためにミニポートドライバーがウェイクアップパターンを追加できない場合、ミニポートドライバーは、OID\_\_PNP に応答して、 **NDIS\_STATUS\_リソース**を返します\_ウェイクアップ\_UP\_パターンを追加します。

プロトコルドライバーが重複したパターンを追加しようとすると、ミニポートドライバーは、 **\_データが無効\_\_** を返します。これは、OID\_PNP に応答して\_\_ウェイクアップ\_上\_パターンを追加します。

上端がこの OID 要求を受信する中間ドライバーは、 [**NdisRequest**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff554681(v=vs.85))または[**NdisCoRequest**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551877(v=vs.85))を呼び出すことによって、常に要求を基になるミニポートドライバーに伝達する必要があります。

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
<td><p>NDIS 6.0 および NDIS 6.1 でサポートされています。 NDIS 6.20 以降では、代わりに<a href="oid-pm-add-wol-pattern.md" data-raw-source="[OID_PM_ADD_WOL_PATTERN](oid-pm-add-wol-pattern.md)">OID_PM_ADD_WOL_PATTERN</a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_PM\_パケット\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID\_PM\_\_WOL\_パターンの追加](oid-pm-add-wol-pattern.md)

 

 




