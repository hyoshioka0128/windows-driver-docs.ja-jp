---
title: OID_SRIOV_READ_VF_CONFIG_BLOCK
description: このドライバーは、指定された PCI Express (PCIe) 仮想関数 (VF) 構成ブロックからデータを読み取るために、OID_SRIOV_READ_VF_CONFIG_BLOCK のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: A7AC7A18-5DA2-4EE8-B635-04616ABFE08C
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SRIOV_READ_VF_CONFIG_BLOCK ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3ad76974bc7f1140279e63aaef1646449c840e16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843984"
---
# <a name="oid_sriov_read_vf_config_block"></a>OID\_SRIOV\_読み取り\_VF\_CONFIG\_BLOCK


あるドライバーが、指定された PCI Express (PCIe) 仮想関数 (VF) の構成ブロックからデータを読み取るために\_VF\_CONFIG\_ブロックを読み取る\_\_OID のオブジェクト識別子 (OID) メソッドの要求を発行します。

この OID メソッドの要求は、ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行されます。 この OID メソッド要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   NDIS\_SRIOV は、この構造体の先頭からデータを格納しているバッファー内の位置までのオフセット (バイト単位) を格納する[ **\_\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)構造体を読み取ります。これは、VF 構成ブロックから読み込まれます。

-   指定された VF 構成ブロックから読み取るデータ用の追加のバッファー領域。

<a name="remarks"></a>注釈
-------

VF 構成ブロックは、PF および VF ミニポートドライバー間のバックチャネル通信に使用されます。 IHV は、ミニポートドライバー用に1つまたは複数の VF 構成ブロックを定義できます。 各 VF 構成ブロックには、IHV によって定義された形式、長さ、およびブロック ID があります。

  **注**各 VF 構成ブロックのデータは、PF および vf ミニポートドライバーによってのみ使用されます。

 

Oid\_oid の OID メソッド要求を発行する前に、SRIOV\_VF\_CONFIG\_BLOCK\_読み取るために、前のドライバーでは、NDIS\_SRIOV のメンバーを設定する必要があり[ **\_の読み取り\_vf\_config\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)は、次のように\_PARAMETERS 構造体をブロックします。

-   **VFId**メンバーに、情報の読み取り元となる VF の識別子を設定します。

-   **ブロック id**メンバーに、情報の読み取り元となる VF 構成ブロックの識別子を設定します。

-   **Length**メンバーに、構成ブロックから読み取るバイト数を設定します。

-   **Bufferoffset**メンバーを、指定された VF 構成ブロックから読み取られるデータを格納するバッファー内のオフセット ( **informationbuffer**メンバーによって参照される) に設定します。 このオフセットは、NDIS\_SRIOV の先頭からのバイト単位で指定され[ **\_\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)構造体を読み取ります。

Oid\_oid の OID メソッド要求を処理するときに、\_VF\_CONFIG\_BLOCK\_読み取るために、PF ミニポートドライバーは次のガイドラインに従う必要があります。

-   PF ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された vf の[ **\_\_vf\_CONFIG\_BLOCK\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)構造体で指定されていることを確認し、以前のリソースがあることを確認する必要があります。済み. PF ミニポートドライバーは、oid の OID メソッド要求中に、 [\_NIC\_スイッチによって\_vf\_割り当てら](oid-nic-switch-allocate-vf.md)れるため、vf のリソースを割り当てます。 指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

-   PF ミニポートドライバーは、 [**NDIS\_SRIOV\_READ\_VF\_CONFIG\_block\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)構造体の**ブロック id**メンバーが有効な vf 構成ブロックを指定していることを確認する必要があります。 それ以外の場合、ドライバーは OID 要求を失敗させる必要があります。

シングルルート i/o 仮想化 (SR-IOV) インターフェイス内でのバックチャネル通信の詳細については、「sr-iov [PF/VF バックチャネル通信](https://docs.microsoft.com/windows-hardware/drivers/network/sr-iov-pf-vf-backchannel-communication)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

PF ミニポートドライバーは、OID\_SRIOV\_READ\_VF\_CONFIG\_BLOCK のメソッド要求について、次のいずれかの状態コードを返します。

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
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_READ_VF_CONFIG_BLOCK_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)"><strong>NDIS_SRIOV_READ_VF_CONFIG_BLOCK_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 ミニポートドライバーはデータを設定する必要があり<strong>ます。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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

[**NDIS\_SRIOV\_読み取り\_VF\_構成\_ブロック\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_読み取り\_VF\_CONFIG\_SPACE](oid-sriov-read-vf-config-space.md)

 

 




