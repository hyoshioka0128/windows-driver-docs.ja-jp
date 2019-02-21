---
title: ColorEntry 要素
description: 必要な ColorEntry 要素には、スキャナーの入力ソースをサポートする 1 つの色処理モードについて説明します。
ms.assetid: a25c6da6-058e-4d10-895c-4507f0562ee8
keywords:
- ColorEntry 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ColorEntry
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 922af823ba1849dba65dc99846dbbe6493d16fea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536502"
---
# <a name="colorentry-element"></a>ColorEntry 要素


必要な**ColorEntry**要素は、スキャナーの入力ソースをサポートする 1 つの色処理モードをについて説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ColorEntry>
  text
</wscn:ColorEntry>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 次のキーワードのいずれか:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="BlackAndWhite1"></span><span id="blackandwhite1"></span><span id="BLACKANDWHITE1"></span>BlackAndWhite1</p></td>
<td><p>黒と白のイメージピクセル (bpp) と 1 つのチャネルあたり 1 ビット</p></td>
</tr>
<tr class="even">
<td><p><span id="Grayscale4"></span><span id="grayscale4"></span><span id="GRAYSCALE4"></span>Grayscale4</p></td>
<td><p>グレースケールの画像。4 bpp と 1 つのチャンネル</p></td>
</tr>
<tr class="odd">
<td><p><span id="Grayscale8"></span><span id="grayscale8"></span><span id="GRAYSCALE8"></span>Grayscale8</p></td>
<td><p>グレースケールの画像。8 ビット/ピクセルと 1 つのチャンネル</p></td>
</tr>
<tr class="even">
<td><p><span id="Grayscale16"></span><span id="grayscale16"></span><span id="GRAYSCALE16"></span>Grayscale16</p></td>
<td><p>グレースケールの画像。16 bpp と 1 つのチャンネル</p></td>
</tr>
<tr class="odd">
<td><p><span id="RGB24"></span><span id="rgb24"></span>RGB24</p></td>
<td><p>色の RGB でエンコードされたイメージです。24 ビット/ピクセルは、それぞれ 8 ビットの 3 つのチャネルの間で分割</p></td>
</tr>
<tr class="even">
<td><p><span id="RGB48"></span><span id="rgb48"></span>RGB48</p></td>
<td><p>色の RGB でエンコードされたイメージです。48 ビット/ピクセルは、それぞれ 16 ビットの 3 つのチャネルの間で分割</p></td>
</tr>
<tr class="odd">
<td><p><span id="RGBa32"></span><span id="rgba32"></span><span id="RGBA32"></span>RGBa32</p></td>
<td><p>アルファ チャネル; を持つ色の RGB でエンコードされたイメージ32 ビットのビット/ピクセルにそれぞれ 8 ビットの 4 つのチャネルの間で分割</p></td>
</tr>
<tr class="even">
<td><p><span id="RGBa64"></span><span id="rgba64"></span><span id="RGBA64"></span>RGBa64</p></td>
<td><p>アルファ チャネル; を持つ色の RGB でエンコードされたイメージ64 ビット/ピクセルは、それぞれ 16 ビットの 4 つのチャネルの間で分割</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="adfcolor.md" data-raw-source="[&lt;strong&gt;ADFColor&lt;/strong&gt;](adfcolor.md)"><strong>ADFColor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="filmcolor.md" data-raw-source="[&lt;strong&gt;FilmColor&lt;/strong&gt;](filmcolor.md)"><strong>FilmColor</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platencolor.md" data-raw-source="[&lt;strong&gt;PlatenColor&lt;/strong&gt;](platencolor.md)"><strong>PlatenColor</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

各キーワードの値には、データ型し、ビット深さ、およびチャネルあたりのビット数のエンコード、色がについて説明します。 次の表では、値のキーワードが処理のプロパティ、スキャナーの色にマップする方法を示します。

| キーワード        | ピクセル ビット深度 | チャネルあたりのビット数 |
|----------------|-----------------|------------------|
| BlackAndWhite1 | 1               | 1                |
| Grayscale4     | 4               | {4}              |
| Grayscale8     | 8               | {8}              |
| Grayscale16    | 16              | {16}             |
| RGB24          | 24              | {8,8,8}          |
| RGB48          | 48              | {16,16,16}       |
| RGBa32         | 32              | {8,8,8,8}        |
| RGBa64         | 64              | {16,16,16,16}    |

 

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**ADFColor**](adfcolor.md)

[**FilmColor**](filmcolor.md)

[**PlatenColor**](platencolor.md)

 

 






