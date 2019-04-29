---
title: 要素の高さ
description: 高さ要素には、スキャナーの構成要素を高さを必要とするデバイスのスキャンをサポートする高さの値を指定します。
ms.assetid: 1161c92e-e135-4921-b55d-b27e98d5caec
keywords:
- デバイスのイメージの高さ要素
topic_type:
- apiref
api_name:
- wscn Height wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c4690d6ff1a964e37038e1a8a0b7f135108475a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330271"
---
# <a name="height-element"></a>要素の高さ


**高さ**要素の高さを必要とする構成要素をスキャナー スキャン デバイスをサポートする高さの値を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Height wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Height wscn:Override="" wscn:UsedDefault="">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>上書き</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>任意。 ブール値は 0、false、1、または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

必須。 使用可能な値は、特定の親要素を参照してください。

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
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>高さ</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="inputmediasize.md" data-raw-source="[&lt;strong&gt;InputMediaSize&lt;/strong&gt;](inputmediasize.md)"><strong>InputMediaSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenmaximumsize.md" data-raw-source="[&lt;strong&gt;PlatenMaximumSize&lt;/strong&gt;](platenmaximumsize.md)"><strong>PlatenMaximumSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="platenminimumsize.md" data-raw-source="[&lt;strong&gt;PlatenMinimumSize&lt;/strong&gt;](platenminimumsize.md)"><strong>PlatenMinimumSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenopticalresolution.md" data-raw-source="[&lt;strong&gt;PlatenOpticalResolution&lt;/strong&gt;](platenopticalresolution.md)"><strong>PlatenOpticalResolution</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

値、**高さ**要素がその親要素に依存します。 かどうかの詳細については**高さ**必須またはオプションであり、その値の詳細については、適切な親の値を参照してください。

[**DocumentFinalParameters**](documentfinalparameters.md)

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、**高さ**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**DocumentFinalParameters**](documentfinalparameters.md)

[**高さ**](heights.md)

[**InputMediaSize**](inputmediasize.md)

[**PlatenMaximumSize**](platenmaximumsize.md)

[**PlatenMinimumSize**](platenminimumsize.md)

[**PlatenOpticalResolution**](platenopticalresolution.md)

[**幅**](width.md)

 

 






