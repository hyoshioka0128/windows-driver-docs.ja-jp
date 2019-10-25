---
title: OID_802_3_ADD_MULTICAST_ADDRESS
description: 設定要求として、NDIS およびそれ以降のプロトコルドライバーは、OID_802_3_ADD_MULTICAST_ADDRESS OID 要求を使用して、802.3 マルチキャストアドレスをミニポートアダプターのマルチキャストアドレス一覧に追加します。
ms.assetid: e3e6defe-e65f-46bb-9cd6-cb65ffa7d7f0
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_802_3_ADD_MULTICAST_ADDRESS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 00843282c99f4673ff3426a42adf6fab2d00afd4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834567"
---
# <a name="oid_802_3_add_multicast_address"></a>OID\_802\_3\_\_マルチキャスト\_アドレスの追加


セット要求として、NDIS およびそれ以降のプロトコルドライバーは、OID\_802\_3\_\_マルチキャスト\_アドレス OID 要求を追加して、ミニポートアダプターのマルチキャストアドレスリストに802.3 マルチキャストアドレスを追加します。 マルチキャストアドレスは6バイトの配列です。 アドレスを追加すると、そのアドレスがマルチキャストパケットを受信できるようになります。

**バージョン情報**

<a href="" id="windows-vista"></a>Windows Vista  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。

<a name="remarks"></a>解説
-------

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、マルチキャストアドレス一覧に追加する6バイトのアドレスが含まれています。

OID\_802\_3\_\_マルチキャスト\_アドレス OID 要求で追加できるアドレスは1つだけです。 複数のアドレスを追加するには、複数の OID\_802\_3\_\_マルチキャスト\_アドレス OID 要求を追加する必要があります。

NDIS ミニポートドライバーは、この OID 要求を直接受信しません。 代わりに、NDIS は、OID の各シーケンス\_802\_3\_\_マルチキャスト\_アドレスおよび[oid\_802\_3\_削除\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)oid 要求を1つ[にまとめます。OID\_802\_3\_マルチキャスト\_リスト](oid-802-3-multicast-list.md)oid 要求をミニポートドライバーに送信します。

マルチキャストパケットを受信するには、その後のドライバーが[oid\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md) oid を使用して、パケットフィルター **NDIS\_パケット\_種類\_マルチキャスト**フラグを設定する必要があります。

ミニポートドライバーでは、マルチキャストアドレス一覧に含めることができるマルチキャストアドレスの数に制限を設定できます。 マルチキャストアドレスの最大数を指定するために、ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造**のメンバーを設定し**[**ます。NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数。 Ndis 6.0 より前の NDIS バージョンに基づくミニポートドライバーの場合、NDIS は[oid\_802\_3\_最大\_LIST\_SIZE](oid-802-3-maximum-list-size.md) oid 要求を送信することにより、マルチキャストアドレスの最大数を照会します。 OID\_802\_3\_追加\_のマルチキャスト\_アドレス要求がこの制限を超えた場合、ndis は**ndis\_STATUS\_マルチキャスト\_完全**を返します。

以前に追加したマルチキャストアドレスを削除するには、 [oid\_802\_3\_削除\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)oid を持つ set 要求を作成します。 このドライバーは、指定されたマルチキャストアドレスを複数回追加できます。 指定されたマルチキャストアドレスの最初の add 要求が NDIS によって成功した場合、NDIS はそのアドレスに対する後続の追加要求すべてを成功させます。 複数回追加されたマルチキャストアドレスを削除するには、そのアドレスを追加したときと同じ回数だけアドレスを削除する必要があります。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[OID\_802\_3\_\_のマルチキャスト\_アドレスの削除](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_最大\_リスト\_サイズ](oid-802-3-maximum-list-size.md)

[OID\_802\_3\_マルチキャスト\_リスト](oid-802-3-multicast-list.md)

[OID\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md)

 

 




