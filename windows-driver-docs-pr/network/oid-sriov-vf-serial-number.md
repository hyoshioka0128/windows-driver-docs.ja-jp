---
title: OID_SRIOV_VF_SERIAL_NUMBER
description: 上にある、ドライバーは、PCI Express (PCIe) 仮想機能 (VF) ネットワーク アダプターのシリアル番号を特定する OID_SRIOV_VF_SERIAL_NUMBER のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: C4D04C96-94FA-4E01-839C-A9C5026D7AE5
ms.date: 08/08/2017
keywords: -OID_SRIOV_VF_SERIAL_NUMBER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f2f4b5fddfc84b6ca1bbd6362afc46481cbba87b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572763"
---
# <a name="oidsriovvfserialnumber"></a>OID\_SRIOV\_VF\_シリアル\_数


上にある、ドライバーの OID オブジェクト識別子 (OID) のクエリ要求を発行する\_SRIOV\_VF\_シリアル\_PCI Express (PCIe) 仮想機能 (VF) ネットワーク アダプターのシリアル番号を特定する番号。 この仮想ネットワーク アダプターは、VF がアタッチされている HYPER-V 子パーティションのゲスト オペレーティング システムで公開されます。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_SRIOV\_VF\_シリアル\_数\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451685)構造体。

<a name="remarks"></a>コメント
-------

上にあるドライバーでは、シリアル番号を使用して、VF のネットワーク アダプターを物理ネットワーク アダプター上の VF のインスタンスにマップします。 VF のリソースの割り当ての OID セット要求を使用する前に、シリアル番号が、仮想化スタックによって生成された[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_SRIOV\_VF\_シリアル\_ミニポート ドライバーの数の要求。 ドライバーにはこの OID 要求が発行するされません。

NDIS が、OID を処理するときに\_SRIOV\_VF\_シリアル\_数要求と、次のステータス コードの 1 つを返します。

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
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_VF\_シリアル\_数\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451685)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




