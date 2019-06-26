---
title: OID_NIC_SWITCH_PARAMETERS
description: 上にある、ドライバーは、ネットワーク アダプターで指定された NIC スイッチの現在の構成パラメーターを取得する OID_NIC_SWITCH_PARAMETERS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 3F2FF2C0-8710-4243-8583-CD80F244FCFB
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2bc175478337d37ac0008672b9a1fd67dde191a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380844"
---
# <a name="oidnicswitchparameters"></a>OID\_NIC\_スイッチ\_パラメーター


上位のドライバーの OID オブジェクト識別子 (OID) メソッド要求を発行する\_NIC\_切り替える\_ネットワーク アダプター スイッチ パラメーターを指定した NIC の現在の構成パラメーターを取得します。 NDIS は、ミニポート ドライバーのこれらの OID メソッド要求を処理します。

ドライバーの問題を後続 OID の要求の設定、OID\_NIC\_スイッチ\_ネットワーク アダプターで指定した NIC の構成パラメーターを設定するパラメーターの切り替え。 これらの OID セット要求は、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) に発行されます。 これらの OID セット要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体。

上にあるドライバーは、OID メソッドの NIC スイッチを指定しますまたは、セットの要求を設定して、 **SwitchId**のメンバー、 [ **NDIS\_NIC\_切り替える\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)スイッチ識別子に構造体。 上にあるドライバーを通じて、次の方法のいずれかのスイッチの識別子を取得します。

-   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_スイッチ](oid-nic-switch-enum-switches.md)します。

-   **NicSwitchArray**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体。 この構造体へのポインターを渡します NDIS、 *BindParameters*のパラメーター、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数。

-   **NicSwitchArray**のメンバー、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体。 この構造体へのポインターを渡します NDIS、 *AttachParameters*のパラメーター、 [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数。

**注**  以降 Windows Server 2012 では、Windows サポート NIC スイッチの既定値のみ、ネットワーク アダプター。 **SwitchId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体は、NDIS に設定する必要があります\_既定の\_スイッチ\_id。

 

<a name="remarks"></a>注釈
-------

上位のドライバーの問題の OID\_NIC\_スイッチ\_次のようにパラメーター要求。

-   上にあるドライバーは、OID の OID メソッド要求を発行\_NIC\_切り替える\_パラメーターを指定した NIC スイッチの現在のパラメーターを取得します。 詳細については、次を参照してください。 [NIC スイッチのパラメーターのクエリを実行する](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-parameters-of-a-nic-switch)します。

    **注**  OID の OID メソッド要求を処理する NDIS\_NIC\_スイッチ\_PF ミニポート ドライバーのパラメーター。

     

-   上にあるドライバーは、OID の OID セット要求を発行\_NIC\_切り替える\_パラメーターを指定した NIC スイッチの現在のパラメーターを変更します。 詳細については、次を参照してください。 [NIC スイッチのパラメーターを設定する](https://docs.microsoft.com/windows-hardware/drivers/network/setting-the-parameters-of-a-nic-switch)します。

    **注**  、PF ミニポート ドライバー OID の OID のセット要求を処理する\_NIC\_スイッチ\_パラメーター。

     

### <a name="return-status-codes"></a>リターン状態コード

NDIS または PF ミニポート ドライバーにより、設定、またはメソッドの次のステータス コードが OID の OID 要求返します\_NIC\_スイッチ\_パラメーター。

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
<td><p>要求は正常に完了しました。 <strong>InformationBuffer</strong>を指す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)"> <strong>NDIS_NIC_SWITCH_CAPABILITIES</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF のミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"> <strong>NDIS_NIC_SWITCH_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS または PF ミニポート ドライバーの設定、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong> (OID メソッド要求) のメンバーまたは<strong>データ。SET_INFORMATION します。BytesNeeded</strong>で (OID セット要求) のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_REINIT_REQUIRED</p></td>
<td><p>PF のミニポート ドライバーでは、NIC のスイッチに変更を適用するネットワーク アダプターの再初期化が必要です。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)

[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_フィルター\_アタッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_ENUM\_SWITCHES](oid-nic-switch-enum-switches.md)

[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)

 

 




