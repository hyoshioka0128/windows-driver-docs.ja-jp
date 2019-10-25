---
title: OID_SRIOV_PROBED_BARS
description: NDIS は、OID_SRIOV_PROBED_BARS のオブジェクト識別子 (OID) クエリ要求を発行して、ネットワークアダプターの PCI Express (PCIe) ベースアドレスレジスタ (バー) の値を取得します。
ms.assetid: 81C3A5B5-58D5-41F4-A000-79F3F4E00DAD
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_PROBED_BARS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: fc31e0c4e6696ca67e74b1736cdb2b6002811865
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843986"
---
# <a name="oid_sriov_probed_bars"></a>OID\_SRIOV\_プローブ\_バー


NDIS は、OID\_OID のオブジェクト識別子 (OID) クエリ要求を発行し、ネットワークアダプターの PCI Express (PCIe) ベースアドレスレジスタ (Bar) の値を取得するために、探索された\_バー\_します。 この関数は、PCI バスドライバーによって実行されるクエリに従ってネットワークアダプターによって報告されたバーの値を返します。 このクエリでは、ネットワークアダプターが必要とするメモリまたは i/o アドレス空間を決定します。

NDIS は oid のクエリ要求 oid\_SRIOV\_ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに\_バーを調査します。 この OID クエリ要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   [**NDIS\_SRIOV\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info) 、ネットワークアダプターの PCI バーに対する読み取り操作のパラメーターを含む、\_バーの\_情報の構造を調査します。

-   PCIe ネットワークアダプターの各バーの ULONG 値の配列。 この配列内の要素の最大数は、PCI\_TYPE0\_アドレスです。

<a name="remarks"></a>注釈
-------

Hyper-v 親パーティションの管理オペレーティングシステムで実行される PCI バスドライバーは、ネットワークアダプターの各 PCI ベースアドレスレジスタ (バー) のメモリまたは i/o アドレス空間の要件を照会します。 PCI バスドライバーは、バス上のアダプターを最初に検出したときに、このクエリを実行します。

Pci バスドライバーは、この PCI BAR クエリを使用して次のことを決定します。

-   PCI バーがネットワークアダプターによってサポートされているかどうか。

-   バーがサポートされている場合は、バーに必要なメモリまたは i/o アドレス空間の量を指定します。

仮想 PCI (VPCI) バスドライバーは、Hyper-v 子パーティションのゲストオペレーティングシステムで実行されます。 PCI Express (PCIe) 仮想関数 (VF) が子パーティションにアタッチされている場合、VPCI バスドライバーは VF (*vf ネットワークアダプター*) 用の仮想ネットワークアダプターを公開します。 これを行う前に、VPCI バスドライバーは、VF ネットワークアダプターに必要なメモリまたはアドレス空間を決定するために PCI バークエリを実行する必要があります。

PCI 構成領域へのアクセスは特権操作であるため、Hyper-v 親パーティションの管理オペレーティングシステムで実行されるコンポーネントによってのみ実行できます。 VPCI バスドライバーが PCI バーに対してクエリを実行すると、NDIS は oid\_oid の OID クエリ要求を発行し、\_PF ミニポートドライバーに\_バーを調査します。 この OID クエリ要求によって返される結果は、VF ネットワークアダプターで必要とされるメモリアドレス空間の量を決定できるように、VPCI バスドライバーに転送されます。

Oid **  oid**要求\_SRIOV\_調査済みの\_バーは、NDIS によってのみ発行されます。 OID 要求は、フィルタードライバーのプロトコルなど、それまでのドライバーによって発行されていない必要があります。

 

OID\_SRIOV\_調査された\_バーのクエリ要求には、\_\_情報構造を調査した[**NDIS\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)が含まれています。 PF ミニポートドライバーがこの OID を処理する場合、ドライバーは、 **NDIS\_\_\_\_SRIOV**の**BaseRegisterValuesOffset**メンバーによって参照される配列内の PCI バーの値を返す必要があります。 PF ミニポートドライバーは、配列内のオフセットごとに、物理アダプターの PCI 構成領域内の同じオフセットにあるバーの ULONG 値に配列要素を設定する必要があります。

ドライバーによって返される各棒値は、管理オペレーティングシステムで実行されている PCI ドライバーによって実行される PCI バークエリに続くものと同じ値である必要があります。 この情報を確認するために、PF ミニポートドライバーは[**NdisMQueryProbedBars**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars)を呼び出すことができます。

PCI デバイスのバーの詳細については、 *Pci ローカルバスの仕様*を参照してください。

VF の PCI BAR レジスタに対してクエリを実行する方法の詳細については、「[仮想関数の Pci ベースアドレスレジスタを照会](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-pci-base-address-registers-of-a-virtual-function)する」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、OID\_\_\_SRIOV のクエリ要求について、次のいずれかの状態コードを返します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが未満 (sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>) + PCI_TYPE0_ADDRESSES) です。 PF ミニポートドライバーはデータを設定する必要があり<strong>ます。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_調査した\_バーの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)

[**NdisMQueryProbedBars**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars)

 

 




