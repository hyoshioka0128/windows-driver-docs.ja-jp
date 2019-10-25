---
title: OID_NIC_SWITCH_ENUM_VFS
description: 前のドライバーまたはユーザーモードアプリケーションが、配列を取得するために OID_NIC_SWITCH_ENUM_VFS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: ABACB70C-9307-4560-93DD-0475AD1FFF10
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NIC_SWITCH_ENUM_VFS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 7e9acf7303d8f3f5af0d6ca11ce589116ac6f8be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844087"
---
# <a name="oid_nic_switch_enum_vfs"></a>OID\_NIC\_スイッチ\_列挙型\_VFS


それ以降のドライバーまたはユーザーモードアプリケーションは、OID\_NIC\_\_\_スイッチのオブジェクト識別子 (OID) メソッド要求を発行して、配列を取得します。 配列の各要素は、ネットワークアダプターの NIC スイッチの NIC スイッチに接続されている PCI Express (PCIe) 仮想関数 (VF) の属性を指定します。

この OID クエリ要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、次を含むバッファーへのポインターが含まれています。

-   [**NDIS\_NIC\_スイッチ\_VF\_INFO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)配列内の要素の数を定義する配列構造体です。

-   [**VF\_INFO 構造体\_の NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)の配列。 これらの各構造体には、ネットワークアダプターの NIC スイッチ上の単一の VF に関する情報が含まれています。 VF は、Oid による oid メソッドの要求を介して NIC スイッチに接続されます。 [\_nic\_スイッチによって\_vf が割り当て\_](oid-nic-switch-allocate-vf.md)ます。

    **注**  ネットワークアダプターの nic スイッチに VFs が接続されていない場合は、NDIS\_NIC\_スイッチの**numelements**メンバー [ **\_VF\_INFO\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)構造体が0に設定され、NDIS がありません[ **\_NIC\_スイッチ\_VF\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)構造が返されます。

     

<a name="remarks"></a>注釈
-------

それ以降のドライバーやユーザーモードアプリケーションは OID\_NIC\_スイッチの OID メソッド要求を発行して、ネットワークアダプターの NIC スイッチに接続されている VFs を列挙\_列挙型\_します。

ドライバーまたはアプリケーションが OID 要求を発行する前に、要求と共に渡される、 [**VF\_INFO\_配列の構造\_、NDIS\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)を初期化する必要があります。 ドライバーまたはアプリケーションは、 **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**構造体を初期化するときに、次のガイドラインに従う必要があります。

-   NDIS\_NIC\_スイッチ\_VF\_情報\_配列\_特定の\_スイッチフラグが**Flags**メンバーで設定されている場合では、ドライバーまたはアプリケーションが**Switchid**メンバーを sr-iov ネットワークアダプターの NIC スイッチ識別子に設定する必要があります。 この方法でこれらのメンバーを設定することにより、SR-IOV ネットワークアダプターの指定された NIC スイッチに対してのみ VF 情報が返されます。

    [\_列挙型\_スイッチ、oid\_nic\_スイッチ](oid-nic-switch-enum-switches.md)の oid クエリ要求を発行することによって、後続のドライバーおよびユーザーモードアプリケーションが nic スイッチ識別子を**取得  こと**ができます。

     

-   **Flags**メンバーが0に設定されている場合、ドライバーまたはアプリケーションは**switchid**メンバーを0に設定する必要があります。 この方法でこれらのメンバーを設定することにより、SR-IOV ネットワークアダプターのすべての NIC スイッチに対して VF 情報が返されます。

**注**  windows Server 2012 以降では、ネットワークアダプターの既定の NIC スイッチのみがサポートされます。 **Flags**メンバーで設定されているフラグに関係なく、 **SWITCHID**メンバーを NDIS\_既定\_スイッチ\_ID に設定する必要があります。

 

NIC スイッチの詳細については、「 [Nic スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/nic-switches)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS では、OID\_NIC\_スイッチの OID メソッド要求を処理します。これにより、ミニポートドライバーの\_列挙型\_VFS 要求が処理されます。 ドライバーは、この OID 要求を発行しません。

NDIS が OID\_NIC を処理するときに、\_列挙\_型の VFS 要求\_スイッチによって、次のステータスコードのいずれかが返されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)"><strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong></a>構造体の1つ以上のメンバーに無効な値が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが短すぎます。 NDIS はデータを設定<strong>します。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体の中で必要とされる最小バッファーサイズに対して、bytesneeded 必要です。</p></td>
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
[**NDIS\_NIC\_スイッチ\_VF\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)

[**NDIS\_NIC\_スイッチ\_VF\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_VF\_パラメーター](oid-nic-switch-vf-parameters.md)

 

 




