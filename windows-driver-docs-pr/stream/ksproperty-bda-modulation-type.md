---
title: KSPROPERTY\_BDA\_変調\_型
description: クライアントを使用して、KSPROPERTY\_BDA\_変調\_QPSK など 8VSB 復調器の種類を制御する型。
ms.assetid: 7c7dd8a4-4aa2-4e62-9b08-05c202df957d
keywords:
- KSPROPERTY_BDA_MODULATION_TYPE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_MODULATION_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6150b222d9d94d17ee2c8664da68787345c17ac9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361702"
---
# <a name="kspropertybdamodulationtype"></a>KSPROPERTY\_BDA\_変調\_型


クライアントを使用して、KSPROPERTY\_BDA\_変調\_QPSK など 8VSB 復調器の種類を制御する型。

## <span id="ddk_ksproperty_bda_modulation_type_ks"></span><span id="DDK_KSPROPERTY_BDA_MODULATION_TYPE_KS"></span>


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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ModulationType</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ModulationType 列挙型から返される値は、復調器の種類を識別します。

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


[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

[**ModulationType**](https://msdn.microsoft.com/library/windows/hardware/ff567735)

 

 






