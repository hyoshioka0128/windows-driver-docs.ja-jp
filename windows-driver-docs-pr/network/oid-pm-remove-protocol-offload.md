---
title: OID_PM_REMOVE_PROTOCOL_OFFLOAD
description: NDIS ドライバーとプロトコルドライバーは、セット要求として OID_PM_REMOVE_PROTOCOL_OFFLOAD OID を使用して、ネットワークアダプターから電源管理プロトコルオフロードを削除します。
ms.assetid: efca3018-28bf-4d91-b698-4b1c9e02f6e3
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PM_REMOVE_PROTOCOL_OFFLOAD ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 1e3d78133e8d79eb2b42824a3cade7658545068f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844049"
---
# <a name="oid_pm_remove_protocol_offload"></a>OID\_PM\_\_プロトコル\_オフロードの削除


設定要求として、NDIS ドライバーとプロトコルドライバーは、ネットワークアダプターから電源管理プロトコルオフロードを削除するために、\_プロトコル\_オフロード\_を削除する OID\_PM を使用します。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 **ULONG**プロトコルオフロード識別子へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS およびプロトコルドライバーは、OID\_PM\_使用して\_プロトコル\_オフロード OID を削除し、基になるネットワークアダプターからプロトコルオフロードを削除します。

**データ。\_情報を設定します。** [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の informationbuffer メンバーは、以前に追加されたプロトコルオフロード識別子の**ULONG**値をポイントする必要があります。 Ndis は、ndis [ **\_pm\_\_プロトコル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)の**ProtocolOffloadId**メンバーで、 [\_プロトコルの追加\_前の OID\_pm が送信されたときに、このプロトコルオフロード識別子を設定\_](oid-pm-add-protocol-offload.md)基になるネットワークアダプターに対して OID 要求をオフロードします。

### <a name="remarks-for-miniport-driver-writers"></a>ミニポートドライバーライターの解説

NDIS では、バッファーサイズが少なくとも**sizeof**(**ULONG**) であり、有効なプロトコルオフロード ID が含まれていることが保証されます。 そのため、ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、この要求に対して成功\_NDIS\_状態を返す必要があります。

**注**  ミニポートドライバーがリセットされている場合、その[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、受け入れ\_受け入れられていない、NDIS\_の状態\_返す必要があります。

 

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、この要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>**NDIS\_状態\_成功**  
プロトコルオフロードが正常に削除されました。

<a href="" id="ndis-status-pending"></a>**NDIS\_状態\_保留中**  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_の状態\_無効な\_の長さです**  
情報バッファーが小さすぎます。 NDIS はデータを設定**します。\_情報を設定します。** Byte で必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体に必要な bytesneeded メンバー。

<a href="" id="ndis-status-file-not-found"></a>**NDIS\_状態\_ファイル\_見つかりませ\_んでした**  
OID 要求のプロトコルオフロード id が無効です。

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

[**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID\_PM\_\_プロトコル\_オフロードの追加](oid-pm-add-protocol-offload.md)

 

 




