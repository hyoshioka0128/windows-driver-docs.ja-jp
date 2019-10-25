---
title: OID_SWITCH_PROPERTY_DELETE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、OID_SWITCH_PROPERTY_DELETE のオブジェクト識別子 (OID) セット要求を発行して、スイッチポリシープロパティの削除に関する拡張可能なスイッチ拡張機能に通知します。
ms.assetid: 55291392-C018-4578-9767-DC5621F75D44
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_PROPERTY_DELETE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: bd5e50243d427493c6d713502fccf567ffe81cf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843918"
---
# <a name="oid_switch_property_delete"></a>OID\_スイッチ\_プロパティ\_削除


Hyper-v 拡張可能スイッチのプロトコルエッジでは、オブジェクト識別子 (OID) セットの OID\_スイッチ\_プロパティ\_削除を発行して、スイッチポリシープロパティの削除に関する拡張可能なスイッチ拡張機能に通知します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SWITCH\_プロパティ\_DELETE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)構造を含むバッファーへのポインターが含まれています。

<a name="remarks"></a>注釈
-------

転送拡張機能は、OID\_スイッチ\_プロパティ\_削除の OID セット要求を処理できます。 その他のすべての種類の拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックの次の拡張機能に OID 要求を転送する必要があります。

Oid の OID セット要求を処理する方法に関するガイドラインについては\_スイッチ\_プロパティ\_削除、「[スイッチポリシーの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-switch-policies)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

転送拡張機能によって oid の OID セット要求が完了し\_\_プロパティ\_削除されると、次のステータスコードのいずれかが返されます。

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
<td><p>転送拡張機能では、スイッチポリシーはサポートされていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>OID 要求は、他の理由で失敗しました。</p></td>
</tr>
</tbody>
</table>

 

転送拡張機能が oid の OID 設定要求を完了していない場合は\_\_プロパティ\_削除されますが、要求は、拡張可能スイッチの基になるミニポートエッジによって完了します。 ミニポートエッジは、次の状態コードを返します。

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

[**NDIS\_スイッチ\_プロパティ\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)

[**NDIS\_スイッチ\_プロパティ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




