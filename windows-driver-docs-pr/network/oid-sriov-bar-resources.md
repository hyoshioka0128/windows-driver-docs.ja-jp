---
title: OID_SRIOV_BAR_RESOURCES
description: NDIS は、PCI Express (PCIe) ベース アドレスを登録 (バー) PCIe 仮想機能 (VF) の割り当てられたメモリ リソースを決定する OID_SRIOV_BAR_RESOURCES のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: CA29591B-EBFB-4B12-A980-F3FAD65207E2
ms.date: 08/08/2017
keywords: -OID_SRIOV_BAR_RESOURCES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c00487b842b64e49307e3a05a18a24e2fde978ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529941"
---
# <a name="oidsriovbarresources"></a>OID\_SRIOV\_バー\_リソース


OID のオブジェクト識別子 (OID) メソッド要求を発行する NDIS\_SRIOV\_バー\_リソースに、PCI Express (PCIe) ベース アドレスを登録 (バー) PCIe 仮想機能 (VF) の割り当てられたメモリ リソースを確認するには.

NDIS は、ネットワーク アダプターの PCIe 物理機能 (PF)、ミニポート ドライバーをこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次の構造が含まれています。

-   [ **NDIS\_SRIOV\_バー\_リソース\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451675) VF とバーを指定する構造体を PF ミニポート ドライバー返すリソース情報。

-   A [ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)従った構造体、 [ **NDIS\_SRIOV\_バー\_リソース\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451675)構造体。 **CM\_部分\_リソース\_記述子**構造に割り当てられたメモリのリソースに関する情報が含まれていますを指定したバー。

<a name="remarks"></a>注釈
-------

OID の OID メソッド要求を発行する NDIS\_SRIOV\_バー\_リソース システムの物理アドレスと VF バーに割り当てられていたメモリ リソースの長さを取得します。 NDIS OID メソッド要求を発行する前に書式設定、 [ **NDIS\_SRIOV\_バー\_リソース\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451675)次のように構造体。

-   NDIS セット、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_バー\_リソース\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451675)構造体をVF に関連付けられている識別子です。

-   NDIS セット、 **BarIndex**のメンバー、 [ **NDIS\_SRIOV\_バー\_リソース\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451675)構造体をバーの指定した VF のインデックス。 バーのインデックスは、PCI 構成領域でのバーのテーブル内のレジスタのオフセットです。

-   NDIS セット、 **BarResourcesOffset**のメンバー、 [ **NDIS\_SRIOV\_バー\_リソース\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451675)先頭からバイト単位のオフセットに構造体、 **NDIS\_SRIOV\_バー\_リソース\_情報**構造体を[ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)構造体。

**注**  OID の OID メソッドの要求を発行できないなど、プロトコルまたはフィルター ドライバー、ドライバー、スライド\_SRIOV\_バー\_PF ミニポート ドライバーにリソース。

 

ドライバーは、指定されたリソースを返します、PF ミニポート ドライバーでは、OID メソッド要求を受け取る、バーの書式設定によって、 [ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)内で構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 ドライバーのフォーマット、 **CM\_部分\_リソース\_記述子**指定 VF のバーに関連付けられているシステムのハードウェア リソースを含む構造体。

**注**  ドライバーは、リソースの種類の構造体の書式設定する必要があります**CmResourceTypeMemory**します。

 

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID のメソッドの要求に関する次の状態コードのいずれかを返します\_SRIOV\_バー\_リソース。

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
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451675" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451675)"> <strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーがより小さい (sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451675" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451675)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>) + sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/ff541977" data-raw-source="[&lt;strong&gt;CM_PARTIAL_RESOURCE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541977)"><strong>CM_PARTIAL_RESOURCE_DESCRIPTOR</strong> </a>). PF のミニポート ドライバーを設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[**CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_バー\_リソース\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451675)

 

 




