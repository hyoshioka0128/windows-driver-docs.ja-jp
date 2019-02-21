---
title: OID_802_3_DELETE_MULTICAST_ADDRESS
description: セットの要求として NDIS と上位のプロトコル ドライバーはミニポート アダプタのマルチキャスト アドレスの一覧から、以前に追加されたマルチキャスト アドレスを削除するのに OID_802_3_DELETE_MULTICAST_ADDRESS OID を使用します。
ms.assetid: 5efaa724-80b4-4721-a1b0-8ba67c03bb32
ms.date: 08/08/2017
keywords: -OID_802_3_DELETE_MULTICAST_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1edd7f5dfe57c943a05daf4277b00544eb6baf87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549998"
---
# <a name="oid8023deletemulticastaddress"></a>OID\_802\_3\_削除\_マルチキャスト\_アドレス


セットの要求では、NDIS と上位のプロトコルのドライバーを使用、OID\_802\_3\_削除\_マルチキャスト\_のマルチキャスト アドレスの一覧から、以前に追加されたマルチキャスト アドレスを削除するアドレスの OID をミニポート アダプター。 マルチキャスト アドレスは、6 バイトの配列です。 アドレスを削除すると、不要になったマルチキャスト パケットを受信できるようにそのアドレスが無効にします。

**バージョン情報**

<a href="" id="windows-vista"></a>Windows Vista  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a name="remarks"></a>注釈
-------

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造にはから削除する 6 バイトのアドレスが含まれています、マルチキャスト アドレスの一覧。

OID\_802\_3\_削除\_マルチキャスト\_アドレス OID 要求は、1 つのアドレスを削除できます。 プロトコル ドライバーに 1 つ以上のアドレスを削除するには、複数の OID を発行する必要があります\_802\_3\_削除\_マルチキャスト\_アドレス OID を要求します。

NDIS ミニポート ドライバーでは、この OID 要求を直接受け取りません。 代わりに、各シーケンスの統合 NDIS [OID\_802\_3\_追加\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)と OID\_802\_3\_削除\_マルチキャスト\_アドレス OID 要求を 1 つに[OID\_802\_3\_マルチキャスト\_一覧](oid-802-3-multicast-list.md)OID 要求。

置換またはマルチキャスト リスト全体を削除、プロトコルのドライバーを使用できます、 [OID\_802\_3\_マルチキャスト\_一覧](oid-802-3-multicast-list.md)OID 要求。

一覧にアドレスを追加するプロトコル ドライバーを使用できます、 [OID\_802\_3\_追加\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)OID 要求。

プロトコル ドライバーに上にあることができます、特定のマルチキャスト アドレスを複数回追加複数を送信することによって[OID\_802\_3\_追加\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)OID 要求. NDIS は後続のすべての成功 NDIS には、指定されたマルチキャスト アドレスの最初の追加要求が成功すると、そのアドレスの要求を追加します。 上にあるドライバーは複数回追加されたマルチキャスト アドレスを削除するには、アドレスをアドレスが追加されたことと同じ回数を削除する必要があります。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、次のいずれかがこの要求の値を返します。

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
<td><p>ミニポート ドライバーでは、要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>関数<strong>NDIS_STATUS_SUCCESS</strong>の<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート ドライバーがリセットされています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>ミニポート ドライバーでは、要求の処理を停止します。 たとえば、NDIS と呼ばれる、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559432" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559432)"> <em>MiniportResetEx</em> </a>関数。</p></td>
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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_802\_3\_追加\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_最大\_一覧\_サイズ](oid-802-3-maximum-list-size.md)

[OID\_802\_3\_マルチキャスト\_一覧](oid-802-3-multicast-list.md)

 

 




