---
title: OID_SRIOV_CURRENT_CAPABILITIES
description: このドライバーは、ネットワークアダプターの現在のシングルルート i/o 仮想化 (SR-IOV) 機能を取得するために、OID_SRIOV_CURRENT_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: EE76B3F8-2883-484A-B2EE-6F7D4738934E
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_CURRENT_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3462bf4802036fe60c78cee5ad4aceb6b73dad6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843992"
---
# <a name="oid_sriov_current_capabilities"></a>OID\_SRIOV\_現在の\_機能


ネットワークアダプターの現在のシングルルート i/o 仮想化 (SR-IOV) 機能を取得するために、それ以降のドライバーは OID\_SRIOV のオブジェクト識別子 (OID) クエリ要求を発行し、現在の\_機能を\_します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_SRIOV\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS 6.30 以降、ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、ネットワークアダプターで有効になっている sr-iov ハードウェア機能を提供します。 このドライバーは、現在有効になっている SR-IOV ハードウェア機能を使用して[**ndis\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造を初期化し、NDIS\_ミニポート\_アダプターの**currentsriの**機能メンバーを設定します。 [ **\_ハードウェア\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)は、 **NDIS\_SRIOV\_CAPABILITIES**構造体へのポインターに\_属性構造をサポートします。 次に、ミニポートドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを NDIS\_ミニポート\_アダプターへのポインターに設定します **\_ハードウェア\_サポート\_属性**構造体。

プロトコルドライバーとフィルタードライバーは、OID\_SRIOV の OID クエリ要求を、現在の\_の機能\_発行する必要はありません。 NDIS は、次のように、ネットワークアダプターの現在有効になっている SR-IOV 機能をこれらのドライバーに提供します。

-   NDIS は、基になるネットワークアダプターの現在有効になっている**sr-iov 機能を**、バインド操作中に、 [**ndis\_bind\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造内のプロトコルドライバーに報告します。

-   NDIS は、基になるネットワークアダプターの現在有効になっている SR-IOV 機能を、 [**ndis\_フィルター\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)の**sriの機能**メンバーにあるフィルタードライバーに報告します。アタッチ操作です。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、ミニポートドライバーに対する現在の\_機能要求\_OID\_SRIOV の OID クエリ要求を処理します。 ドライバーは、この OID 要求を発行しません。

NDIS は、OID\_SRIOV\_現在の\_機能の要求を処理するときに、次のいずれかのステータスコードを返します。

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

 

 




