---
title: OID_SRIOV_PF_LUID
description: このドライバーは、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) に関連付けられているローカル一意識別子 (LUID) を受信するために、OID_SRIOV_PF_LUID のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: 363D308D-CE88-4F3B-81FF-37A2D86CB7BC
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SRIOV_PF_LUID
ms.localizationpriority: medium
ms.openlocfilehash: 62c796a33f2597068cb385af660a68a960dcf8e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843987"
---
# <a name="oid_sriov_pf_luid"></a>OID\_SRIOV\_PF\_LUID


ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) に関連付けられているローカル一意識別子 (LUID) を受信するために、SRIOV\_PF\_LUID\_のオブジェクト識別子 (OID) クエリ要求が実行されています。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_PF\_LUID\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_pf_luid_info)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

Ndis では、NDIS が PF のミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出す前に、PF の LUID が生成されます。 この LUID は、NDIS がドライバーの[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出すまで有効です。

**Luid**メンバーの値は、 [**NDIS\_ミニポート\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体の**netluid**メンバーとは異なる  に**注意**してください。 この構造体は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の*Miniportinitparameters*パラメーターを使用してミニポートドライバーに渡されます。

 

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、ミニポートドライバーに対する OID\_SRIOV\_PF\_LUID 要求の oid クエリ要求を処理します。 ドライバーは、この OID 要求を発行しません。

NDIS が\_SRIOV\_PF\_LUID 要求を処理すると、次のいずれかのステータスコードが返されます。

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
<td><p>情報バッファーが短すぎます。 ミニポートドライバーはデータを設定する必要があり<strong>ます。QUERY_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
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
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_PF\_LUID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_pf_luid_info)

 

 




