---
title: OID_NIC_SWITCH_ENUM_VFS
description: 上にあるドライバーまたはユーザー モード アプリケーションでは、配列を取得する OID_NIC_SWITCH_ENUM_VFS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: ABACB70C-9307-4560-93DD-0475AD1FFF10
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_ENUM_VFS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c3ea8f06739035dac11b7325a714b01255176dc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359268"
---
# <a name="oidnicswitchenumvfs"></a>OID\_NIC\_スイッチ\_ENUM\_VFS


上にあるドライバーまたはユーザー モード アプリケーションの OID オブジェクト識別子 (OID) メソッド要求の発行\_NIC\_スイッチ\_ENUM\_VFS 配列を取得します。 配列内の各要素は、NIC にアタッチされている属性の PCI Express (PCIe) 仮想機能 (VF) は、ネットワーク アダプターの NIC のスイッチのスイッチを指定します。

この OID クエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体以下を含むバッファーへのポインターが含まれます。

-   [ **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451592)配列内の要素の数を定義する構造体。

-   配列の[ **NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)構造体。 各構造体には、NIC のスイッチのネットワーク アダプターの 1 つの VF に関する情報が含まれています。 VF がアタッチされている NIC の OID メソッド要求をスイッチに[OID\_NIC\_スイッチ\_割り当て\_VF](oid-nic-switch-allocate-vf.md)します。

    **注**  VFs が添付されていない場合、ネットワーク アダプター上の NIC スイッチに、 **NumElements**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451592)構造を設定に 0 と no [ **NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)構造体が返されます。

     

<a name="remarks"></a>注釈
-------

上にあるドライバーとユーザー モード アプリケーションは、OID の OID メソッド要求を発行\_NIC\_切り替える\_ENUM\_VFS VFs を列挙するためには、ネットワーク アダプターの NIC のスイッチに接続します。

ドライバーまたはアプリケーションは、OID 要求を発行して、前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451592)要求と共に渡される構造体。 ドライバーまたはアプリケーションは、初期化するときに、次のガイドラインに従う必要があります、 **NDIS\_NIC\_スイッチ\_VF\_情報\_配列**構造体。

-   場合は、NDIS\_NIC\_スイッチ\_VF\_情報\_配列\_ENUM\_ON\_特定\_スイッチ フラグに設定されて、**フラグ**メンバー、ドライバーまたはアプリケーションを設定する必要があります、 **SwitchId** SR-IOV ネットワーク アダプターで NIC スイッチ識別子へのメンバー。 この方法でこれらのメンバーを設定して指定された NIC スイッチ、SR-IOV ネットワーク アダプターに対してのみ、VF の情報が返されます。

    **注**  上にあるドライバーとユーザー モード アプリケーションの OID クエリ要求を発行して NIC スイッチの識別子を取得できます[OID\_NIC\_切り替える\_ENUM\_スイッチ](oid-nic-switch-enum-switches.md)します。

     

-   場合、**フラグ**メンバーが 0 に設定されている、ドライバーまたはアプリケーションを設定する必要があります、 **SwitchId**メンバーをゼロにします。 この方法でこれらのメンバーを設定して、VF 情報がすべての返されます NIC は、SR-IOV ネットワーク アダプターのスイッチします。

**注**  以降 Windows Server 2012 では、Windows サポート NIC スイッチの既定値のみ、ネットワーク アダプター。 設定されているフラグに関係なく、**フラグ**、メンバー、 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

 

NIC のスイッチの詳細については、次を参照してください。 [NIC スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh439961)します。

### <a name="return-status-codes"></a>リターン状態コード

NDIS OID の OID メソッド要求を処理する\_NIC\_スイッチ\_ENUM\_ミニポート ドライバーの VFS 要求。 ドライバーにはこの OID 要求が発行するされません。

NDIS が、OID を処理するときに\_NIC\_スイッチ\_ENUM\_VFS 要求と、次のステータス コードの 1 つを返します。

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
[**NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)

[**NDIS\_NIC\_スイッチ\_VF\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh451592)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_スイッチ](oid-nic-switch-create-switch.md)

[OID\_NIC\_スイッチ\_VF\_パラメーター](oid-nic-switch-vf-parameters.md)

 

 




