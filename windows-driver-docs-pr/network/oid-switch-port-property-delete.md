---
title: OID_SWITCH_PORT_PROPERTY_DELETE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、拡張可能なスイッチポートのポリシープロパティの削除について拡張可能なスイッチ拡張機能に通知するために、オブジェクト識別子 (OID) セット要求を OID_SWITCH_PORT_PROPERTY_DELETE に発行します。
ms.assetid: BA8AB5D9-FF2C-4E16-B09F-B09E3EC19B90
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PORT_PROPERTY_DELETE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f57290bb4268a59ca745158796b34124aa7b56a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843929"
---
# <a name="oid_switch_port_property_delete"></a>OID\_スイッチ\_ポート\_プロパティ\_削除


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) set 要求の OID\_スイッチ\_ポート\_プロパティ\_削除を使用して、拡張可能なスイッチ拡張機能に、のポリシープロパティの削除について通知します。拡張可能なスイッチポート。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_スイッチ\_ポート\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)を含むバッファーへのポインターが含まれています\_パラメーターを削除\_データ.

<a name="remarks"></a>注釈
-------

転送拡張機能は、OID\_スイッチ\_ポート\_プロパティ\_削除の OID セット要求を処理できます。 その他のすべての種類の拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックの次の拡張機能に OID 要求を転送する必要があります。

Oid の OID セット要求を処理する方法に関するガイドラインについては\_\_ポート\_プロパティ\_削除については、「[ポートポリシーの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-port-policies)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

転送拡張機能が oid の OID セット要求を完了すると、\_スイッチ\_ポート\_プロパティ\_削除によって、次のいずれかのステータスコードが返されます。

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
<td><p>転送拡張機能は、ポートポリシーをサポートしていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>OID 要求は、他の理由で失敗しました。</p></td>
</tr>
</tbody>
</table>

 

転送拡張機能が oid の OID 設定要求を完了していない場合\_\_ポート\_プロパティ\_削除の場合、要求は、拡張可能スイッチの基になるミニポートエッジによって完了します。 ミニポートエッジは、次の状態コードを返します。

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

[**NDIS\_スイッチ\_ポート\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_custom)

[**NDIS\_スイッチ\_ポート\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)

[**NDIS\_スイッチ\_ポート\_プロパティ\_VLAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_vlan)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




