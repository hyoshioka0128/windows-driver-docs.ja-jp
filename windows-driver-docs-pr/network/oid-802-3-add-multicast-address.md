---
title: OID_802_3_ADD_MULTICAST_ADDRESS
description: セットの要求として NDIS と上位のプロトコル ドライバーはミニポート アダプタのマルチキャスト アドレスの一覧に 802.3 のマルチキャスト アドレスを追加するのに OID_802_3_ADD_MULTICAST_ADDRESS OID 要求を使用します。
ms.assetid: e3e6defe-e65f-46bb-9cd6-cb65ffa7d7f0
ms.date: 08/08/2017
keywords: -OID_802_3_ADD_MULTICAST_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c9ba8b1e689d3ce2ce190a0967ae58f29dd428ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377280"
---
# <a name="oid8023addmulticastaddress"></a>OID\_802\_3\_追加\_マルチキャスト\_アドレス


セットの要求では、NDIS と上位のプロトコルのドライバーを使用、OID\_802\_3\_追加\_マルチキャスト\_ミニポートのマルチキャスト アドレスの一覧を 802.3 のマルチキャスト アドレスを追加するアドレス OID 要求アダプター。 マルチキャスト アドレスは、6 バイトの配列です。 アドレスを追加すると、そのアドレスをマルチキャスト パケットの受信ができます。

**バージョン情報**

<a href="" id="windows-vista"></a>Windows Vista  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a name="remarks"></a>注釈
-------

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、マルチキャストに追加する 6 バイトのアドレスが含まれています。アドレスの一覧です。

OID\_802\_3\_追加\_マルチキャスト\_アドレス OID 要求は、1 つのアドレスを追加できます。 1 つ以上のアドレスを追加するには、上にあるドライバーが複数の OID を発行する必要があります\_802\_3\_追加\_マルチキャスト\_アドレス OID を要求します。

NDIS ミニポート ドライバーでは、この OID 要求を直接受け取りません。 代わりに、各シーケンスの OID の統合 NDIS\_802\_3\_追加\_マルチキャスト\_アドレスと[OID\_802\_3\_DELETE\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)OID 要求 1 つに[OID\_802\_3\_マルチキャスト\_一覧](oid-802-3-multicast-list.md)OID 要求を送信すること、ミニポート ドライバー。

マルチキャスト パケットを受信するには、上にあるドライバーを使用する必要があります、 [OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md)パケット フィルターを設定する OID **NDIS\_パケット\_型\_マルチキャスト**フラグ。

ミニポート ドライバーは、マルチキャスト アドレスの一覧に含めることができるマルチキャスト アドレスの数に上限を設定することができます。 マルチキャストの最大数を指定するアドレス、ミニポート ドライバーのセット、 **MaxMulticastListSize**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_一般的な\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)に渡される構造体、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。 NDIS 6.0 より前に、の NDIS バージョンに基づくミニポート ドライバーでは、NDIS が送信することによってマルチキャスト アドレスの最大数を照会、 [OID\_802\_3\_最大\_一覧\_サイズ](oid-802-3-maximum-list-size.md) OID 要求。 NDIS 返します**NDIS\_状態\_マルチキャスト\_完全**場合 OID\_802\_3\_追加\_マルチキャスト\_アドレス要求は、この制限を超えています。

以前に追加されたマルチキャスト アドレスを削除するには、セット要求を行う、 [OID\_802\_3\_削除\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)OID。 上にあるドライバーは、複数回指定したマルチキャスト アドレスを追加できます。 NDIS は後続のすべての成功 NDIS には、指定されたマルチキャスト アドレスの最初の追加要求が成功すると、そのアドレスの要求を追加します。 上にあるドライバーは複数回追加されたマルチキャスト アドレスを削除するには、アドレスをアドレスが追加されたことと同じ回数を削除する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[OID\_802\_3\_削除\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_最大\_一覧\_サイズ](oid-802-3-maximum-list-size.md)

[OID\_802\_3\_マルチキャスト\_一覧](oid-802-3-multicast-list.md)

[OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md)

 

 




