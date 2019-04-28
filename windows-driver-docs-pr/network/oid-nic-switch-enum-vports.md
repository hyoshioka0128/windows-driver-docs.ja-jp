---
title: OID_NIC_SWITCH_ENUM_VPORTS
description: 上にあるドライバーまたはユーザー モード アプリケーションでは、配列を取得する OID_NIC_SWITCH_ENUM_VPORTS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 4B9587E0-3CA9-46AF-A80E-969E6D563922
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_ENUM_VPORTS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f3f621dae5fbf00dc0883f8b97bcbfdc58af9126
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382200"
---
# <a name="oidnicswitchenumvports"></a>OID\_NIC\_スイッチ\_ENUM\_拡張


上にあるドライバーまたはユーザー モード アプリケーションの OID オブジェクト識別子 (OID) メソッド要求の発行\_NIC\_スイッチ\_列挙\_拡張配列を取得します。 配列内の各要素には、ネットワーク アダプターの NIC のスイッチが作成されている仮想ポート (VPort) の属性を指定します。

この OID クエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体以下を含むバッファーへのポインターが含まれます。

-   [ **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451595)配列内の要素の数を定義する構造体。

-   配列の[ **NDIS\_NIC\_スイッチ\_VPORT\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451594)構造体。 各構造体には、ネットワーク アダプターの NIC のスイッチ上の VPort に関する情報が含まれています。

    **注**  ネットワーク アダプターの拡張が作成されていない場合、ドライバーの設定、 **NumElements**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451595)構造体を 0、no [ **NDIS\_NIC\_スイッチ\_VPORT\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451594)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

上にあるドライバーとユーザー モード アプリケーションは、OID の OID クエリ要求を発行\_NIC\_スイッチ\_ENUM\_のネットワーク アダプターの NIC のスイッチに割り当てられている拡張を列挙するために拡張します。

ドライバーまたはアプリケーションは、OID 要求を発行して、前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451595)要求と共に渡される構造体。 ドライバーまたはアプリケーションは、初期化するときに、次のガイドラインに従う必要があります、 **NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**構造体。

-   場合は、NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列\_ENUM\_ON\_特定\_スイッチ フラグに設定されて、 **フラグ**メンバー、指定した NIC のスイッチで作成されたすべての拡張の情報が返されます。 NIC のスイッチがで指定された、 **SwitchId**その構造体のメンバー。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチの既定値のみ、ネットワーク アダプター。 設定されているフラグに関係なく、**フラグ**、メンバー、 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

     

-   場合は、NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列\_ENUM\_ON\_特定\_関数フラグに設定されて、 **フラグ**メンバー、ネットワーク アダプターで指定された PCI Express (PCIe) 物理機能 (PF) または仮想機能 (VF) に接続してすべての拡張の情報が返されます。 PF または VF がで指定された、 **AttachedFunctionId**その構造体のメンバー。

    場合、 **AttachedFunctionId** NDIS にメンバーが設定されている\_PF\_関数\_ID、ネットワーク アダプターの PF. に関連付けられているすべての拡張、VPort、既定値などの情報が返されます 場合、 **AttachedFunctionId** VF の有効な識別子にメンバーが設定されている、指定した VF にすべての拡張の情報が返されます。

    **注**  VPort、VF に接続できる 1 つだけの既定以外の Windows Server 2012 以降します。 ただし、(VPort の既定値を含む) 複数の拡張は、PF. に接続できます。

     

-   場合、**フラグ**メンバーが 0 に設定されている、すべての拡張が VF、PF にネットワーク アダプターの接続情報が返されます。 ここでの値、 **SwitchId**と**AttachedFunctionId**は無視されます。

詳細については、次を参照してください。[ネットワーク アダプターの仮想ポートを列挙](https://msdn.microsoft.com/library/windows/hardware/hh406710)します。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID メソッド要求を処理する NDIS\_NIC\_スイッチ\_列挙\_ミニポート ドライバーの拡張要求。 ドライバーにはこの OID 要求が発行するされません。

NDIS が、OID を処理するときに\_NIC\_スイッチ\_ENUM\_拡張要求と、次のステータス コードの 1 つを返します。

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
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451592" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_INFO_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451592)"> <strong>NDIS_NIC_SWITCH_VF_INFO_ARRAY</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
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
[**NDIS\_NIC\_スイッチ\_VPORT\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451594)

[**NDIS\_NIC\_スイッチ\_VPORT\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451595)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_SWITCH\_PARAMETERS](oid-nic-switch-parameters.md)

 

 




