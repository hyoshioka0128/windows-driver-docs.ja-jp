---
title: OID_SRIOV_PF_LUID
description: 上にある、ドライバーは、ローカル一意識別子 (LUID) と、PCI Express (PCIe) 物理機能 (PF) のネットワーク アダプターに関連付けられているを受信する OID_SRIOV_PF_LUID のオブジェクト識別子 (OID) のクエリ要求を発行します。
ms.assetid: 363D308D-CE88-4F3B-81FF-37A2D86CB7BC
ms.date: 08/08/2017
keywords: -OID_SRIOV_PF_LUID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 65992a7e5f8afe66bf48954040c9b882acab7169
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580898"
---
# <a name="oidsriovpfluid"></a>OID\_SRIOV\_PF\_LUID


上にある、ドライバーの OID オブジェクト識別子 (OID) のクエリ要求を発行する\_SRIOV\_PF\_LUID ローカル一意識別子 (LUID) と、PCI Express (PCIe) 物理機能 (PF)、ネットワークの関連付けられているを受信するにはアダプター。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_SRIOV\_PF\_LUID\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451678)構造体。

<a name="remarks"></a>コメント
-------

NDIS は、NDIS 呼び出される前に PF の LUID を生成、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) PF. のミニポート ドライバーの機能 NDIS 呼び出されるまでこの LUID が正しく、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)ドライバーの機能です。

**注**  の値、 **Luid**メンバーとは異なります、 **NetLuid**のメンバー、 [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)構造体。 この構造体は、ミニポート ドライバーに渡される、 *MiniportInitParameters*パラメーターの[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。

 

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_SRIOV\_PF\_ミニポート ドライバーの LUID 要求。 ドライバーにはこの OID 要求が発行するされません。

NDIS が、OID を処理するときに\_SRIOV\_PF\_LUID 要求と、次のステータス コードの 1 つを返します。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 ミニポート ドライバーを設定する必要があります、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_PF\_LUID\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451678)

 

 




