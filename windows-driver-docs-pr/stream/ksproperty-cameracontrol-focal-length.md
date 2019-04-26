---
title: KSPROPERTY\_CAMERACONTROL\_焦点\_長さ
description: KSPROPERTY\_CAMERACONTROL\_焦点\_LENGTH プロパティは、カメラの焦点距離情報を取得します。
ms.assetid: a7fba5e4-abd1-46ae-b93c-5fede0249771
keywords:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5512d79baa88e74de9a386e36fdd11b614781fa8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341830"
---
# <a name="kspropertycameracontrolfocallength"></a>KSPROPERTY\_CAMERACONTROL\_焦点\_長さ


KSPROPERTY\_CAMERACONTROL\_焦点\_LENGTH プロパティは、カメラの焦点距離情報を取得します。

## <span id="ddk_ksproperty_cameracontrol_focal_length_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_KS"></span>


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
<td><p>X</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564408" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564408)"><strong>KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff564418" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564418)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの焦点距離を指定する LONG が。

<a name="remarks"></a>注釈
-------

このプロパティの要求を使用すると、ズーム値を解釈します。 ズームの範囲がでなければなりません**lObjectiveFocalLengthMin**/**lOcularFocalLength**と**lObjectiveFocalLengthMax** / **lOcularFocalLength**します。 (**lOcularFocalLength**、 **lObjectiveFocalLengthMin**、および**lObjectiveFocalLengthMax**のメンバーである、 [ **KSPROPERTY\_CAMERACONTROL\_焦点\_長さ\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff564408)と[ **KSPROPERTY\_CAMERACONTROL\_ノード\_焦点\_長さ\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff564418)構造体)。

たとえば場合、 **lObjectiveFocalLengthMax** 105 = と**lOcularFocalLength** = 35、このカメラは 105/35、または 3 の光学ズームの最大比率。

また、*光学ズーム*USB ビデオ クラス デバイス クラス仕様のセクション。 この仕様は、 [USB Implementers Forum](https://go.microsoft.com/fwlink/p/?linkid=8780) web サイト。

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
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_CAMERACONTROL\_焦点\_長さ\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564408)

[**KSPROPERTY\_CAMERACONTROL\_ノード\_焦点\_長さ\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564418)

[**KSPROPERTY\_CAMERACONTROL\_ズーム**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY\_CAMERACONTROL\_ズーム\_相対**](ksproperty-cameracontrol-zoom-relative.md)

 

 






