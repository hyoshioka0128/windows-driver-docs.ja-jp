---
title: OID_SRIOV_HARDWARE_CAPABILITIES
description: このドライバーは、ネットワークアダプターのシングルルート i/o 仮想化 (SR-IOV) ハードウェア機能を取得するために、OID_SRIOV_HARDWARE_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: EEF99105-BBDC-4093-8B11-D27F13B1A3D0
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_HARDWARE_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 14574a9f973f2e5036f74977e1c87ebcd36c1e3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843989"
---
# <a name="oid_sriov_hardware_capabilities"></a>OID\_SRIOV\_ハードウェア\_機能


ネットワークアダプターのシングルルート i/o 仮想化 (SR-IOV) ハードウェア機能を取得するために、そのドライバーは OID\_SRIOV\_ハードウェア\_機能のオブジェクト識別子 (OID) クエリ要求を発行します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

[**NDIS\_SRIOV\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体には、ネットワークアダプターのハードウェア機能に関する情報が含まれます。これには、アダプターが sr-iov をサポートするかどうか、およびミニポートドライバーがアダプターの PCI Express を管理しているかどうか (PCIe) 物理機能 (PF) または仮想機能 (VF)。 これらの機能には、INF ファイルの設定によって現在無効になっているハードウェア機能や、 **[詳細設定**] プロパティページを含めることができます。

**  ネットワーク**アダプターのすべての sr-iov 機能は、機能が有効になっているか無効になっているかに関係なく、OID\_SRIOV\_ハードウェア\_機能の oid クエリ要求によって返されます。

 

NDIS 6.30 以降、ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに sr-iov ハードウェア機能を提供します。 このドライバーは、SR-IOV ハードウェア機能を使用して[**ndis\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造を初期化し、NDIS\_ミニポート\_アダプター\_ハードウェアの**ハード waresriの**機能メンバーを設定します。 [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)は、 **NDIS\_SRIOV\_CAPABILITIES**構造体へのポインターに\_属性構造体をサポートします。 次に、ミニポートドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを NDIS\_ミニポート\_アダプターへのポインターに設定します **\_ハードウェア\_サポート\_属性**構造体。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、ミニポートドライバーに対する OID\_SRIOV\_ハードウェア\_機能要求の oid クエリ要求を処理します。 ドライバーは、この OID 要求を発行しません。

NDIS が OID\_SRIOV\_HARDWARE\_CAPABILITIES 要求を処理するときに、次のいずれかのステータスコードが返されます。

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
<td><p>情報バッファーが短すぎます。 ミニポートドライバーはデータを設定する必要があり<strong>ます。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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
[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_フィルター\_\_パラメーターをアタッチする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_SRIOV\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

 

 




