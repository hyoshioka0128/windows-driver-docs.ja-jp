---
title: KSPROPERTY\_BDA\_内部\_FEC\_型
description: クライアントを使用して、KSPROPERTY\_BDA\_内部\_FEC\_復調器ノードの内部の転送エラーの修正 (FEC) の種類を制御する型。
ms.assetid: e6640d89-cf75-4073-98fb-2a877d6c38d3
keywords:
- KSPROPERTY_BDA_INNER_FEC_TYPE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_INNER_FEC_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fdd9ed4757f52cbe069c958ef9cea1135d81731
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582569"
---
# <a name="kspropertybdainnerfectype"></a>KSPROPERTY\_BDA\_内部\_FEC\_型


クライアントを使用して、KSPROPERTY\_BDA\_内部\_FEC\_復調器ノードの内部の転送エラーの修正 (FEC) の種類を制御する型。

## <span id="ddk_ksproperty_bda_inner_fec_type_ks"></span><span id="DDK_KSPROPERTY_BDA_INNER_FEC_TYPE_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>FECMethod</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

FECMethod 列挙型から返される値は、FEC 型を認識します。

**NodeId** KSP のメンバー\_ノード復調器ノードの識別子を指定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FECMethod**](https://msdn.microsoft.com/library/windows/hardware/ff559594)

[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






