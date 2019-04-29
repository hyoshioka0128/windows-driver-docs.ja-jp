---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_HUE
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_HUE プロパティは、カメラの hue の設定を制御します。 このプロパティは省略可能です。
ms.assetid: 2e347a6b-c04f-41e2-841f-0d77213035e5
keywords:
- KSPROPERTY_VIDEOPROCAMP_HUE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_HUE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6912eec7de2153e42c6c261bde6315078b8d0a14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327012"
---
# <a name="kspropertyvideoprocamphue"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_HUE


KSPROPERTY\_ビデオ プロシージャ アンプ\_HUE プロパティは、カメラの hue の設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_hue_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_HUE_KS"></span>


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

 

プロパティの値 (データの操作) は、カメラの hue の設定を指定する LONG が。 Hue の設定の値は 100 倍して度で表されます。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_構造が hue の設定を指定します。

すべてのビデオ キャプチャ ミニドライバーの範囲と既定値を定義する必要があります、**値**このプロパティのメンバー。 必要な範囲は、18000 (-180 ~ +180 度) に-18000 である必要があります。 既定値は 0 である必要があります。

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

 

 






