---
title: OID_NIC_SWITCH_PARAMETERS
description: 上にある、ドライバーは、ネットワーク アダプターで指定された NIC スイッチの現在の構成パラメーターを取得する OID_NIC_SWITCH_PARAMETERS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 3F2FF2C0-8710-4243-8583-CD80F244FCFB
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f41ef06761ea0091456e500a59d42bde2db14e6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350965"
---
# <a name="oidnicswitchparameters"></a>OID\_NIC\_スイッチ\_パラメーター


上位のドライバーの OID オブジェクト識別子 (OID) メソッド要求を発行する\_NIC\_切り替える\_ネットワーク アダプター スイッチ パラメーターを指定した NIC の現在の構成パラメーターを取得します。 NDIS は、ミニポート ドライバーのこれらの OID メソッド要求を処理します。

ドライバーの問題を後続 OID の要求の設定、OID\_NIC\_スイッチ\_ネットワーク アダプターで指定した NIC の構成パラメーターを設定するパラメーターの切り替え。 これらの OID セット要求は、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) に発行されます。 これらの OID セット要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。

上にあるドライバーは、OID メソッドの NIC スイッチを指定しますまたは、セットの要求を設定して、 **SwitchId**のメンバー、 [ **NDIS\_NIC\_切り替える\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)スイッチ識別子に構造体。 上にあるドライバーを通じて、次の方法のいずれかのスイッチの識別子を取得します。

-   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_スイッチ](oid-nic-switch-enum-switches.md)します。

-   **NicSwitchArray**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。 この構造体へのポインターを渡します NDIS、 *BindParameters*のパラメーター、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。

-   **NicSwitchArray**のメンバー、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。 この構造体へのポインターを渡します NDIS、 *AttachParameters*のパラメーター、 [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)関数。

**注**  以降 Windows Server 2012 では、Windows サポート NIC スイッチの既定値のみ、ネットワーク アダプター。 **SwitchId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体は、NDIS に設定する必要があります\_既定の\_スイッチ\_id。

 

<a name="remarks"></a>注釈
-------

上位のドライバーの問題の OID\_NIC\_スイッチ\_次のようにパラメーター要求。

-   上にあるドライバーは、OID の OID メソッド要求を発行\_NIC\_切り替える\_パラメーターを指定した NIC スイッチの現在のパラメーターを取得します。 詳細については、次を参照してください。 [NIC スイッチのパラメーターのクエリを実行する](https://msdn.microsoft.com/library/windows/hardware/hh440179)します。

    **注**  OID の OID メソッド要求を処理する NDIS\_NIC\_スイッチ\_PF ミニポート ドライバーのパラメーター。

     

-   上にあるドライバーは、OID の OID セット要求を発行\_NIC\_切り替える\_パラメーターを指定した NIC スイッチの現在のパラメーターを変更します。 詳細については、次を参照してください。 [NIC スイッチのパラメーターを設定する](https://msdn.microsoft.com/library/windows/hardware/hh440227)します。

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
<td><p>要求は正常に完了しました。 <strong>InformationBuffer</strong>を指す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566583" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566583)"> <strong>NDIS_NIC_SWITCH_CAPABILITIES</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF のミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451587" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451587)"> <strong>NDIS_NIC_SWITCH_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS または PF ミニポート ドライバーの設定、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong> (OID メソッド要求) のメンバーまたは<strong>データ。SET_INFORMATION します。BytesNeeded</strong>で (OID セット要求) のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[*FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)

[**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_フィルター\_アタッチ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff565481)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_ENUM\_SWITCHES](oid-nic-switch-enum-switches.md)

[*ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)

 

 




