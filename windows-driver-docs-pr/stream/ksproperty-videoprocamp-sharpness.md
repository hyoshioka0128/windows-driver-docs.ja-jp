---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_鮮明度
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_鮮明度プロパティは、カメラの鮮明度の設定を制御します。 このプロパティは省略可能です。
ms.assetid: d6b10876-313b-420a-9d81-348030e580dd
keywords:
- KSPROPERTY_VIDEOPROCAMP_SHARPNESS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_SHARPNESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3878d22d7499e4073a64682399092261e92419c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327338"
---
# <a name="kspropertyvideoprocampsharpness"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_鮮明度


KSPROPERTY\_ビデオ プロシージャ アンプ\_鮮明度プロパティは、カメラの鮮明度の設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_sharpness_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_SHARPNESS_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566089" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566089)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff566080" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566080)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの鮮明度の設定を指定する LONG が。 鮮明度は、任意の単位で表されます。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_構造が鮮明度の設定を指定します。

すべてのビデオ キャプチャ ミニドライバーは、このプロパティの値の範囲と既定値を定義する必要があります。 必要な範囲は 0 ~ 100 である必要があります。 既定値は 50 である必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566089)

 

 






