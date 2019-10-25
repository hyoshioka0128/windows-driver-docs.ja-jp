---
title: OID_PM_REMOVE_WOL_PATTERN
description: セットとして、NDIS ドライバーとプロトコルドライバーは OID_PM_REMOVE_WOL_PATTERN OID を使用して、ネットワークアダプターから電源管理 wake on LAN (WOL) パターンを削除します。
ms.assetid: fdaa2646-6f41-4f51-9c27-6194270f26ed
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_REMOVE_WOL_PATTERN ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 25d10b0d52671d7041c02cc1d69eccf076c78e41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844047"
---
# <a name="oid_pm_remove_wol_pattern"></a>OID\_PM\_\_WOL\_パターンの削除


セットとして、NDIS ドライバーとプロトコルドライバーは、ネットワークアダプターから電源管理 wake on LAN (WOL) パターンを削除するために、\_WOL\_PATTERN OID\_削除する OID\_PM を使用します。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、ULONG パターン識別子へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS およびプロトコルドライバーでは、OID\_PM\_使用して\_WOL\_パターンを削除し、基になるネットワークアダプターから wake on LAN (WOL) パターンを削除します。

**データ。\_情報を設定します。** [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の informationbuffer メンバーは、以前に追加された WOL パターン識別子の ULONG 値をポイントする必要があります。 Ndis は、ndis [ **\_pm\_wol\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造で、このパターン識別子を設定**します。** ndis は、前の OID\_pm を送信したときに\_[wol\_pattern](oid-pm-add-wol-pattern.md) OID 要求を基になるネットワークアダプター。

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

 

NDIS は、この要求に対して次のいずれかの状態コードを返します。

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
<td><p>OID 要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>ミニポートドライバーの NDIS バージョンが NDIS 6.20 未満です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p>OID 要求のパターン識別子が無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS はデータを設定<strong>します。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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
<td><p>バージョン</p></td>
<td><p>NDIS 6.20 以降でサポートされています。 ミニポートドライバーの場合は必須です。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[OID\_PM\_\_WOL\_パターンの追加](oid-pm-add-wol-pattern.md)

[**NDIS\_状態\_PM\_WOL\_パターン\_拒否されました**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)

 

 




