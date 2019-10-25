---
title: OID_NIC_SWITCH_VF_PARAMETERS
description: ネットワークアダプター上の PCI Express (PCIe) 仮想関数 (VF) の現在の構成パラメーターを取得するために、OID_NIC_SWITCH_VF_PARAMETERS のオブジェクト識別子 (OID) メソッドの要求を、それ以降のドライバーまたはユーザーモードアプリケーションが発行します。
ms.assetid: DF08B0BA-6D86-4C4F-AC38-8A401F097925
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NIC_SWITCH_VF_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 7b837949593853fd8f7b7c7107387da1a7c96dad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844077"
---
# <a name="oid_nic_switch_vf_parameters"></a>OID\_NIC\_スイッチ\_VF\_パラメーター


それ以降のドライバーまたはユーザーモードアプリケーションは、OID\_\_NIC のオブジェクト識別子 (OID) メソッド要求を発行します。これにより、VF\_パラメーター\_、の PCI Express (PCIe) 仮想関数 (VF) の現在の構成パラメーターを取得します。ネットワークアダプター。 Oid の oid メソッド要求を通じて割り当てられたリソースを持つ VFs [\_nic\_スイッチ\_割り当て\_vf](oid-nic-switch-allocate-vf.md)は、OID\_NIC\_スイッチ\_の oid メソッド要求を使用して照会でき\_パラメータ.

NDIS では、OID\_NIC\_スイッチの OID メソッド要求を処理します。これは、ミニポートドライバーの VF\_パラメーター\_ます。

OID メソッド要求が行われると、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

前のドライバーまたはユーザーモードアプリケーションでは、 [ **\_vf\_PARAMETERS 構造体\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)の**VFID**メンバーを vf の識別子に設定することによって、クエリの対象となる vf を指定します。 その後のドライバーまたはアプリケーションは、次のいずれかの方法で VF 識別子を取得します。

-   Oid\_oid の OID メソッド要求を発行すると、 [\_列挙型\_VFS\_切り替わり](oid-nic-switch-enum-vfs.md)ます。

    この OID 要求が正常に完了した場合、それ以降のドライバーまたはユーザーモードアプリケーションは、ネットワークアダプターに割り当てられているすべての VFs の一覧を受け取ります。 リスト内の各要素は、 **VFId**メンバーによって指定された vf 識別子を使用して、 [ **\_の vf\_INFO 構造体\_スイッチの NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)です。

-   Oid\_oid の OID メソッド要求を発行することによって、 [\_VF\_割り当て\_](oid-nic-switch-allocate-vf.md)ます。

    この OID 要求が正常に完了すると、新しく作成された VF の識別子が、返された[**NDIS\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体の**VFId**メンバーに渡されます。

    **注**  は、この方法で VF 識別子を取得できるのは、それまでのドライバーのみです。

     

OID メソッド要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、ndis\_\_NIC へのポインターが含まれ[ **\_VF\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体。 この構造体には、指定された VF の構成パラメーターが含まれています。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、oid の oid メソッド要求を処理します。これは、ミニポートドライバー用の VF\_パラメーター\_\_スイッチによって\_し、oid\_NIC の oid メソッド要求に対して次の状態コードを返します.

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
<td><p>要求は正常に完了しました。 <strong>Informationbuffer</strong>メンバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>構造体を指します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポートドライバーがシングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートしていないか、インターフェイスの使用が有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>) 未満です。 NDIS はデータを設定<strong>します。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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
[**NDIS\_NIC\_スイッチ\_VF\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_列挙型\_VFS](oid-nic-switch-enum-vfs.md)

[**NDIS\_NIC\_スイッチ\_VF\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)

[OID\_NIC\_スイッチ\_VF\_パラメーター](oid-nic-switch-vf-parameters.md)

 

 




