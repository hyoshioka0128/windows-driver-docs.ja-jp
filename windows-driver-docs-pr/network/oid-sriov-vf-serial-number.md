---
title: OID_SRIOV_VF_SERIAL_NUMBER
description: このドライバーは、PCI Express (PCIe) 仮想関数 (VF) のネットワークアダプターのシリアル番号を決定するために、OID_SRIOV_VF_SERIAL_NUMBER のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: C4D04C96-94FA-4E01-839C-A9C5026D7AE5
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_VF_SERIAL_NUMBER ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 07a6d73766e383b4737ee0de4c6ce2ad3a271fe9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843974"
---
# <a name="oid_sriov_vf_serial_number"></a>OID\_SRIOV\_VF\_シリアル\_番号


SRIOV\_VF\_シリアル\_番号の OID\_オブジェクト識別子 (OID) クエリ要求を実行しているドライバーが、PCI Express (PCIe) 仮想関数 (VF) のネットワークアダプターのシリアル番号を確認します。 この仮想ネットワークアダプターは、VF が接続されている Hyper-v 子パーティションのゲストオペレーティングシステムで公開されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_VF\_シリアル\_番号\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

このドライバーは、シリアル番号を使用して、VF ネットワークアダプターを物理ネットワークアダプターの VF のインスタンスにマップします。 シリアル番号は、仮想化スタックによって生成される前に、Oid のリソースが[\_NIC\_スイッチ](oid-nic-switch-allocate-vf.md)によって割り当てられ\_\_VF が割り当てられます。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、ミニポートドライバーに対して、OID\_SRIOV\_VF\_シリアル\_番号要求の oid クエリ要求を処理します。 ドライバーは、この OID 要求を発行しません。

NDIS が OID\_SRIOV\_VF\_SERIAL\_NUMBER 要求を処理するときに、次のいずれかのステータスコードが返されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポートドライバーがシングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_VF\_シリアル\_番号\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

 

 




