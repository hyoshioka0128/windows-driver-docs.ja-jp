---
title: OID_SRIOV_BAR_RESOURCES
description: NDIS は、PCIe 仮想機能 (VF) の PCI Express (PCIe) ベースアドレスレジスタ (BAR) に割り当てられたメモリリソースを特定するために、OID_SRIOV_BAR_RESOURCES のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: CA29591B-EBFB-4B12-A980-F3FAD65207E2
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_SRIOV_BAR_RESOURCES
ms.localizationpriority: medium
ms.openlocfilehash: 8bfa71685bdb8017777d131ea2ac46656a68674f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843993"
---
# <a name="oid_sriov_bar_resources"></a>OID\_SRIOV\_BAR\_リソース


NDIS は、オブジェクト識別子 (OID) メソッドの OID\_SRIOV\_BAR\_リソースを発行して、PCIe 仮想機能 (VF) の PCI Express (PCIe) ベースアドレスレジスタ (BAR) に割り当てられたメモリリソースを特定します。

NDIS は、この OID メソッド要求をネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行します。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーには、次の構造体が含まれています。

-   [**NDIS\_SRIOV\_bar\_RESOURCES\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)構造体で、PF ミニポートドライバーがリソース情報を返す VF とバーを指定します。

-   [**CM\_\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)構造体は、 [**NDIS\_SRIOV\_BAR\_RESOURCES\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)構造体に従います。 **CM\_PARTIAL\_リソース\_記述子**構造体には、指定されたバーに割り当てられたメモリリソースに関する情報が含まれています。

<a name="remarks"></a>注釈
-------

NDIS は、SRIOV\_BAR\_リソースの oid メソッド\_要求を発行して、VF バーに割り当てられたメモリリソースのシステム物理アドレスと長さを取得します。 NDIS は OID メソッド要求を発行する前に、次の方法で[**ndis\_SRIOV\_BAR\_RESOURCES\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)構造体をフォーマットします。

-   NDIS は、 [**ndis\_SRIOV\_BAR\_RESOURCES\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)構造体の**VFId**メンバーに、VF に関連付けられている識別子を設定します。

-   NDIS は、 [**ndis\_SRIOV\_\_\_BAR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)の**barindex**メンバーを指定された VF のバーインデックスに設定します。 バーインデックスは、PCI 構成領域の横棒の表におけるレジスタのオフセットです。

-   Ndis は、ndis [ **\_SRIOV\_bar\_resources\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)構造体の**barresourcesoffset**メンバーを、 **ndis\_SRIOV\_bar\_resources\_INFO**構造体の先頭から[**CM\_部分的\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)構造に設定します。

**注**  プロトコルやフィルタードライバーなどのそれ以降のドライバーは、OID の oid メソッド要求を\_SRIOV\_BAR\_のリソースを PF ミニポートドライバーに発行することはできません。

 

PF ミニポートドライバーが OID メソッド要求を受信すると、ドライバーは、指定されたバー [ **\_部分\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)構造体を、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバー内に書式設定して返します。 ドライバーは、指定された VF のバーに関連付けられているシステムハードウェアリソースを使用して、 **CM\_部分\_リソース\_記述子**構造体をフォーマットします。

**CmResourceTypeMemory**のリソースの種類の構造は、ドライバーによってフォーマットされる必要**が  ます**。

 

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、OID\_SRIOV\_BAR\_リソースのメソッド要求について、次のいずれかの状態コードを返します。

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
<td><p>PF ミニポートドライバーは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーがより小さい (sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor" data-raw-source="[&lt;strong&gt;CM_PARTIAL_RESOURCE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)"><strong>CM_PARTIAL_RESOURCE_DESCRIPTOR</strong></a>)。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。METHOD_INFORMATION。BytesNeeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
</tr>
<tr class="odd">
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
[**CM\_部分\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_BAR\_リソース\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)

 

 




