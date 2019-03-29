---
title: KSPROPERTY\_BDA\_OUTER\_FEC\_型
description: クライアントを使用して、KSPROPERTY\_BDA\_OUTER\_FEC\_復調器ノードの外部の転送エラーの修正 (FEC) の種類を制御する型。
ms.assetid: 952fd2d6-20c8-4fb3-a92a-1e6bcedfd68b
keywords:
- KSPROPERTY_BDA_OUTER_FEC_TYPE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_OUTER_FEC_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e42e7d23beebd1cc5949a10473d5bdc8dcd081e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573927"
---
# <a name="kspropertybdaouterfectype"></a>KSPROPERTY\_BDA\_OUTER\_FEC\_型


クライアントを使用して、KSPROPERTY\_BDA\_OUTER\_FEC\_復調器ノードの外部の転送エラーの修正 (FEC) の種類を制御する型。

## <span id="ddk_ksproperty_bda_outer_fec_type_ks"></span><span id="DDK_KSPROPERTY_BDA_OUTER_FEC_TYPE_KS"></span>


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

 

 






