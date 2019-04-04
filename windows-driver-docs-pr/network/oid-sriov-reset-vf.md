---
title: OID_SRIOV_RESET_VF
description: ドライバーの問題に関連オブジェクト識別子 (OID) は、指定された PCI Express (PCIe) 仮想機能 (VF) でシングル ルート I/O 仮想化をサポートするネットワーク アダプターをリセットする OID_SRIOV_RESET_VF の要求を設定します。
ms.assetid: 7D5EB64B-3345-478A-8D42-192939C0B9C2
ms.date: 08/08/2017
keywords: -OID_SRIOV_RESET_VF ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1484aa08143befd9544f0237b73c08806addb440
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548749"
---
# <a name="oidsriovresetvf"></a>OID\_SRIOV\_リセット\_VF


ドライバーの問題に関連オブジェクト識別子 (OID) の設定の OID 要求\_SRIOV\_リセット\_VF を指定された PCI Express (PCIe) 仮想機能 (VF) でシングル ルート I/O 仮想化をサポートするネットワーク アダプターをリセットします。 上にあるドライバーは、、PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーをこの OID セット要求を発行します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_SRIOV\_リセット\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451682)構造体。 上にあるドライバーをリセットする VF の識別子を指定する、 **VFId**この構造体のメンバー。

<a name="remarks"></a>注釈
-------

VF にを通じて、PCI Express (PCIe) 関数レベルのリセット (FLR) をリセットできます。 FLR 要求は、特権が必要であるために、HYPER-V 親パーティションの管理オペレーティング システムで実行されている PF ミニポート ドライバーでのみ実行できます。 OID OID の要求の設定 FLR 要求と問題の通知は、管理オペレーティング システムで実行される上にあるドライバー\_SRIOV\_リセット\_VF PF ミニポート ドライバーにします。

この OID 要求を処理する場合、PF ミニポート ドライバーは次のガイドラインに従います。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_リセット\_VF\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451682)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   リセット操作には、指定 VF のみ影響する必要があります。 操作では、その他の VFs または同じネットワーク アダプターの PF には影響する必要があります。

詳細については、[仮想関数をリセットする](https://msdn.microsoft.com/library/windows/hardware/hh440219)を参照してください。

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID のセットの要求に関する次の状態コードのいずれかを返します\_SRIOV\_リセット\_VF します。

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
<td><p>PF のミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451682" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_RESET_VF_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451682)"> <strong>NDIS_SRIOV_RESET_VF_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_リセット\_VF\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451682)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




