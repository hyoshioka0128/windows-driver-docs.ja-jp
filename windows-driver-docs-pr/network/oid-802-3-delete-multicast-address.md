---
title: OID_802_3_DELETE_MULTICAST_ADDRESS
description: NDIS およびそれ以降のプロトコルドライバーは、set 要求として OID_802_3_DELETE_MULTICAST_ADDRESS OID を使用して、以前に追加したマルチキャストアドレスをミニポートアダプターのマルチキャストアドレスリストから削除します。
ms.assetid: 5efaa724-80b4-4721-a1b0-8ba67c03bb32
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_802_3_DELETE_MULTICAST_ADDRESS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3b60f6bd731976170ffef80745327aed39d0189a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834559"
---
# <a name="oid_802_3_delete_multicast_address"></a>OID\_802\_3\_\_のマルチキャスト\_アドレスの削除


設定要求として、NDIS およびそれ以降のプロトコルドライバーは OID\_802\_3\_削除\_マルチキャスト\_アドレス OID を使用して、以前に追加したマルチキャストアドレスをミニポートアダプターのマルチキャストアドレスの一覧から削除します。 マルチキャストアドレスは6バイトの配列です。 アドレスを削除すると、そのアドレスが無効になり、マルチキャストパケットを受信できなくなります。

**バージョン情報**

<a href="" id="windows-vista"></a>Windows Vista  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。

<a name="remarks"></a>注釈
-------

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、マルチキャストアドレス一覧から削除する6バイトのアドレスが含まれています。

OID\_802\_3\_削除\_マルチキャスト\_アドレス OID 要求では、1つのアドレスのみを削除できます。 複数のアドレスを削除するには、プロトコルドライバーが複数の OID\_802\_3 を発行し\_\_マルチキャスト\_アドレス OID 要求を削除する必要があります。

NDIS ミニポートドライバーは、この OID 要求を直接受信しません。 代わりに、NDIS は、OID の各シーケンス[\_802\_3\_\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)および oid\_802\_3\_削除\_マルチキャスト\_アドレス oid 要求を1つ[にまとめます。OID\_802\_3\_マルチキャスト\_リスト](oid-802-3-multicast-list.md)oid 要求。

マルチキャストリスト全体を置換または削除するには、プロトコルドライバーで[oid\_802\_3\_マルチキャスト\_リスト](oid-802-3-multicast-list.md)oid 要求を使用できます。

アドレスを一覧に追加するには、プロトコルドライバーで[oid\_802\_3\_\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)oid 要求を追加します。

このプロトコルドライバーでは、複数の[OID\_802\_3\_送信し、マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)OID 要求を\_追加することによって、特定のマルチキャストアドレスを複数回追加できます。 指定されたマルチキャストアドレスの最初の add 要求が NDIS によって成功した場合、NDIS はそのアドレスに対する後続の追加要求すべてを成功させます。 複数回追加されたマルチキャストアドレスを削除するには、そのアドレスを追加したときと同じ回数だけアドレスを削除する必要があります。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、この要求に対して次のいずれかの値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>ミニポートドライバーが要求を正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポートドライバーは、要求を非同期的に完了します。 ミニポートドライバーはすべての処理を完了した後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>関数を呼び出し、 <em>STATUS</em>パラメーターに<strong>NDIS_STATUS_SUCCESS</strong>を渡すことによって、要求を成功させる必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポートドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポートドライバーが要求の処理を停止しました。 たとえば、NDIS は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>Miniportresetex</em></a>関数を呼び出しました。</p></td>
</tr>
</tbody>
</table>

 

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_802\_3\_\_マルチキャスト\_アドレスの追加](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_最大\_リスト\_サイズ](oid-802-3-maximum-list-size.md)

[OID\_802\_3\_マルチキャスト\_リスト](oid-802-3-multicast-list.md)

 

 




