---
title: OID_NIC_SWITCH_VF_PARAMETERS
description: 上にあるドライバー、またはユーザー モード アプリケーションは、現在の構成パラメーターの PCI Express (PCIe) 仮想機能 (VF)、ネットワーク アダプターを取得する OID_NIC_SWITCH_VF_PARAMETERS のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: DF08B0BA-6D86-4C4F-AC38-8A401F097925
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_VF_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 69a7bdb5f9f3050aca78adcf3b7d207a44abae6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570552"
---
# <a name="oidnicswitchvfparameters"></a>OID\_NIC\_スイッチ\_VF\_パラメーター


上にあるドライバーまたはユーザー モード アプリケーションの OID オブジェクト識別子 (OID) メソッド要求の発行\_NIC\_スイッチ\_VF\_PCI Express (PCIe) の現在の構成パラメーターを取得するパラメーター仮想機能 (VF) ネットワーク アダプターにします。 OID メソッド要求を通じて割り当てられたリソースがある VFs のみ[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md) OIDのOIDメソッドの要求を使って照会できます\_NIC\_スイッチ\_VF\_パラメーター。

OID の OID メソッド要求を処理する NDIS\_NIC\_スイッチ\_VF\_ミニポート ドライバーのパラメーター。

OID メソッドの要求が行われたときに、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、[ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。

<a name="remarks"></a>コメント
-------

上にあるドライバーまたはユーザー モード アプリケーションを設定して、VF にクエリを指定します、 **VFId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593) VF の識別子に構造体。 上にあるドライバーやアプリケーションは次の方法のいずれかで VF 識別子を取得します。

-   OID メソッド要求を発行して[OID\_NIC\_スイッチ\_ENUM\_VFS](oid-nic-switch-enum-vfs.md)します。

    この OID 要求が正常に完了すると、上にあるドライバーまたはユーザー モード アプリケーションは、ネットワーク アダプターに割り当てられているすべての VFs の一覧を受け取ります。 リスト内の各要素は、 [ **NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)構造は、指定された、 VFid**VFId**メンバー。

-   OID メソッド要求を発行して[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。

    上にあるドライバーがで新しく作成された VF の識別子を受け取るこの OID 要求が正常に完了している場合、 **VFId** 、返されたメンバー [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。

    **注**  専用ドライバーの関連でこの方法で VF 識別子を取得できます。

     

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。 この構造体には、指定した VF の構成パラメーターが含まれています。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID メソッド要求を処理する NDIS\_NIC\_スイッチ\_VF\_ミニポート ドライバー、および返しますが、次の状態コードの OID の OID メソッド要求のパラメーターを\_NIC\_スイッチ\_VF\_パラメーター。

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
<td><p>要求は正常に完了しました。 <strong>InformationBuffer</strong>へのポインター、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"> <strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"> <strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451593" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451593)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>)。 NDIS セット、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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
[**NDIS\_NIC\_スイッチ\_VF\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451593)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_SWITCH\_ENUM\_VFS](oid-nic-switch-enum-vfs.md)

[**NDIS\_NIC\_スイッチ\_VF\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451591)

[OID\_NIC\_スイッチ\_VF\_パラメーター](oid-nic-switch-vf-parameters.md)

 

 




