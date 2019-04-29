---
title: FilmColor 要素
description: 必要な FilmColor 要素には、入力ソースをスキャンするフィルムがサポートする機能を処理する色の一覧が含まれています。
ms.assetid: daea2cb8-a29f-4be8-bc58-8ed45d64870c
keywords:
- FilmColor 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FilmColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4eda96116c285245e6884ae7dbeab9c4e9aee1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323256"
---
# <a name="filmcolor-element"></a>FilmColor 要素


必要な**FilmColor**要素には、入力ソースをスキャンするフィルムがサポートする機能を処理する色の一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FilmColor>
  child elements
</wscn:FilmColor>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


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
<td><p><a href="colorentry.md" data-raw-source="[&lt;strong&gt;ColorEntry&lt;/strong&gt;](colorentry.md)"><strong>ColorEntry</strong></a></p></td>
</tr>
</tbody>
</table>

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

**FilmColor**要素には色の処理と取得、スキャナーのフィルムの入力ソースのスキャンをサポートする種類を決定するために必要な情報が含まれています。

各ピクセルの記述に必要な情報の量が特定の依存[ **ColorEntry** ](colorentry.md)キーワード。 白と黒のイメージでは、グレースケールおよびカラーの画像がはるかに多くの情報が必要ですが、1 つのビット/ピクセル (bpp) のみが必要です。 正確な情報量は、色空間とスキャン デバイスの技術的な能力によって決まります。

スキャンが返されるデータのもう 1 つの重要な側面では、取得したデータのメトリックスです。 スキャン デバイスを返すすべてのイメージ データは、白、黒が 0 で表され、空白が 1 で表される場所の上に黒にする必要があります。

## <a name="see-also"></a>関連項目


[**ColorEntry**](colorentry.md)

[**フィルム**](film.md)

 

 






