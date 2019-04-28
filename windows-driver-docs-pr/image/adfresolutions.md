---
title: ADFResolutions 要素
description: 必要な ADFResolutions 要素には、スキャナーの自動ドキュメント フィーダー (ADF) の前または後ろの側をスキャンできます解像度の一覧が含まれています。
ms.assetid: 6747b4d9-3333-4f06-9c1e-043dde24273c
keywords:
- ADFResolutions 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADFResolutions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe90400bf7ce104e2b574f9404b102ac119acad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367080"
---
# <a name="adfresolutions-element"></a>ADFResolutions 要素


必要な**ADFResolutions**要素には、スキャナーの自動ドキュメント フィーダー (ADF) の前または後ろの側をスキャンできます解像度の一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADFResolutions>
  child elements
</wscn:ADFResolutions>
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
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>高さ</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="widths.md" data-raw-source="[&lt;strong&gt;Widths&lt;/strong&gt;](widths.md)"><strong>幅</strong></a></p></td>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

として解像度が指定されて、 [**幅**](width.md) x [**高さ**](height.md)のペアを両方**幅**と**高さ**1 インチあたりのピクセル単位で指定されます。

場合の親要素、 **ADFResolutions**要素は[ **ADFFront**](adffront.md)ADF の正面に指定の解像度が適用されますそれ以外の場合、親要素は、。[ **ADFBack** ](adfback.md)解像度は、ADF の背面に適用されます。

WSD スキャン サービス内でスキャン デバイスをサポートするすべての設定可能な幅が一覧表示されます、**幅**子要素と内でスキャン デバイスをサポートするすべての可能な高さ、**高さ**子要素。 すべて**幅**と**高さ**値は、互いに依存しないと、ほとんどのデバイス サポート内の任意の組み合わせでペアになって、 [ **ScanTicket**](scanticket.md)要素。

## <a name="see-also"></a>関連項目


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**高さ**](heights.md)

[**ScanTicket**](scanticket.md)

[**幅**](width.md)

[**幅**](widths.md)

 

 






