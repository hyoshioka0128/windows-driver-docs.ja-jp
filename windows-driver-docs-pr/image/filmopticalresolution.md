---
title: FilmOpticalResolution 要素
description: 必要な FilmOpticalResolution 要素には、入力ソースをスキャンするフィルムをスキャンできます最大解像を指定します。
ms.assetid: 85e3b737-d5b0-4262-ab86-32b6aaf56e26
keywords:
- FilmOpticalResolution 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FilmOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f67dde69cd576ac54057594eb2d3fbb6683513
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530477"
---
# <a name="filmopticalresolution-element"></a>FilmOpticalResolution 要素


必要な**FilmOpticalResolution**要素が入力ソースをスキャンするフィルムをスキャンできます最大光の解像度を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FilmOpticalResolution/>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>フィルム</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

として解像度が指定されて、 [**幅**](width.md) x [**高さ**](height.md)のペアを両方**幅**と**高さ**1 インチあたりのピクセル単位で指定されます。

場合**高さ**が存在しない場合は、WSD スキャン サービスは、正方形の画像の解像度を想定してください。 のみの場合など、**幅**100 の要素が指定されて、解像度が正方形 1 インチあたりの 100 x 100 ピクセルであると仮定します。

## <a name="see-also"></a>関連項目


[**フィルム**](film.md)

[**Height**](height.md)

[**幅**](width.md)

 

 






