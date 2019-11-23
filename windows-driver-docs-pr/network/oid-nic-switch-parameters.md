---
title: OID_NIC_SWITCH_PARAMETERS
description: ネットワークアダプター上の指定した NIC スイッチの現在の構成パラメーターを取得するために、OID_NIC_SWITCH_PARAMETERS のオブジェクト識別子 (OID) メソッドの要求が、後のドライバーによって発行されます。
ms.assetid: 3F2FF2C0-8710-4243-8583-CD80F244FCFB
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_NIC_SWITCH_PARAMETERS
ms.localizationpriority: medium
ms.openlocfilehash: c6f0b640dae8975c188fd0a0b6dd82076dbb7b58
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844079"
---
# <a name="oid_nic_switch_parameters"></a>OID\_NIC\_スイッチ\_パラメーター


ネットワークアダプター上で指定された NIC スイッチの現在の構成パラメーターを取得するために、関連するドライバーが OID\_\_\_OID のオブジェクト識別子 (OID) メソッド要求を発行します。 NDIS は、ミニポートドライバーに対するこれらの OID メソッド要求を処理します。

これまでのドライバーは oid\_NIC の OID セット要求を発行し、ネットワークアダプター上で指定された NIC スイッチの構成パラメーターを設定するために\_パラメーターを\_スイッチします。 これらの OID セット要求は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行されます。 これらの OID セット要求は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする PF ミニポートドライバーに必要です。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体へのポインターが含まれています。

前のドライバーでは、 [**NDIS\_\_\_nic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)の**switchid**メンバーをスイッチ識別子に設定することによって、OID メソッドまたは set 要求の nic スイッチを指定します。 前のドライバーは、次のいずれかの方法でスイッチ識別子を取得します。

-   Oid\_NIC の以前の OID メソッド要求からは[\_スイッチ\_列挙型\_スイッチ](oid-nic-switch-enum-switches.md)です。

-   NDIS の**NicSwitchArray**メンバーから[ **\_PARAMETERS 構造体\_バインド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)します。 NDIS は、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数の*bindparameters*パラメーターでこの構造体へのポインターを渡します。

-   NDIS\_フィルターの**NicSwitchArray**メンバーから[ **\_\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体をアタッチします。 NDIS は、 [*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数の*attachparameters*パラメーターにこの構造体へのポインターを渡します。

**注**  windows Server 2012 以降では、ネットワークアダプターの既定の NIC スイッチのみがサポートされます。 [**Ndis\_NIC\_スイッチ\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体の**switchid**メンバーは、既定\_スイッチ\_ID\_に設定する必要があります。

 

<a name="remarks"></a>注釈
-------

この後のドライバーは、次の方法で\_パラメーターの要求を\_、OID\_NIC に発行します。

-   前のドライバーは oid\_oid の OID メソッド要求を発行し、\_パラメーターを指定して、指定された NIC スイッチの現在のパラメーターを取得し\_ます。 詳細については、「 [NIC スイッチのパラメーターのクエリ](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-parameters-of-a-nic-switch)」を参照してください。

    **注**  NDIS は、OID の oid メソッド要求を処理します\_NIC\_、PF ミニポートドライバーの\_パラメーターを切り替えます。

     

-   前のドライバーは oid\_\_NIC の OID セット要求を発行し、\_パラメーターを指定して、指定された NIC スイッチの現在のパラメーターを変更します。 詳細については、「 [NIC スイッチのパラメーターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-parameters-of-a-nic-switch)」を参照してください。

    PF ミニポートドライバーは、OID\_NIC\_スイッチ\_パラメーターの OID セット要求を処理  **ことに注意**してください。

     

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS または PF ミニポートドライバーは、OID\_NIC\_スイッチ\_パラメーターの設定またはメソッド OID 要求について、次のステータスコードを返します。

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
<td><p>要求は正常に完了しました。 <strong>Informationbuffer</strong>は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>構造体を指します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF ミニポートドライバーは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS または PF ミニポートドライバーは、データを設定し<strong>ます。METHOD_INFORMATION。BytesNeeded な</strong>メンバー (OID メソッド要求の場合) または<strong>データ。SET_INFORMATION。</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の bytesneeded メンバー (OID セット要求の場合) が、必要な最小バッファーサイズに設定されている必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_REINIT_REQUIRED</p></td>
<td><p>PF ミニポートドライバーは、NIC スイッチに変更を適用するために、ネットワークアダプターを再初期化する必要があります。</p></td>
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
[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_フィルター\_\_パラメーターをアタッチする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_NIC\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_列挙型\_スイッチ](oid-nic-switch-enum-switches.md)

[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

 

 




