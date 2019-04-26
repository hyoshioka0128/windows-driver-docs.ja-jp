---
title: KSPROPERTY\_BDA\_GUARD\_間隔
description: クライアントを使用して、KSPROPERTY\_BDA\_ガード\_復調器ノードのガード間隔の設定を制御する間隔。
ms.assetid: 7c0c6c5e-94fd-4013-9778-d41568ae9f0b
keywords:
- KSPROPERTY_BDA_GUARD_INTERVAL ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_GUARD_INTERVAL
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cadafae4ce7d46c0da6f89f4771548563a5eaa96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340880"
---
# <a name="kspropertybdaguardinterval"></a>KSPROPERTY\_BDA\_GUARD\_間隔


クライアントを使用して、KSPROPERTY\_BDA\_ガード\_復調器ノードのガード間隔の設定を制御する間隔。

## <span id="ddk_ksproperty_bda_guard_interval_ks"></span><span id="DDK_KSPROPERTY_BDA_GUARD_INTERVAL_KS"></span>


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
<td><p>GuardInterval</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

GuardInterval 列挙型から返される値は、ガード間隔の設定を識別します。

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


[**GuardInterval**](https://msdn.microsoft.com/library/windows/hardware/ff559626)

[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






