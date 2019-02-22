---
title: MediaSides 要素
description: 省略可能な MediaSides 要素には、スキャンしたメディアの各物理側に固有のパラメーターが含まれています。
ms.assetid: 9bd3de21-4b2c-4cea-add6-51240ad6c19f
keywords:
- MediaSides 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn MediaSides wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 270514ab08bfc3d0461919d0814935ac7ea5450c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556786"
---
# <a name="mediasides-element"></a>MediaSides 要素


省略可能な**MediaSides**要素には、スキャンしたメディアの各物理側に固有のパラメーターが含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:MediaSides wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:MediaSides wscn:MustHonor="">
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
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="mediaback.md" data-raw-source="[&lt;strong&gt;MediaBack&lt;/strong&gt;](mediaback.md)"><strong>MediaBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

二重モード対応スキャナーが多く、リージョンの別のスキャン、色の処理の各物理側、スキャンしたメディアの解像度を設定できます。 **MediaSides**要素には、メディアのフロント エンドとバックエンドの辺の別のデータが含まれています。 スキャンのすべてのジョブは、メディア前面のパラメーターを指定できます。

[ **MediaBack** ](mediaback.md)要素が無効にすると、スキャナーとのみをサポート双方向のスキャンでは、現在[**指定**](inputsource.md)は**ADFDuplex**します。

場合**指定**は**ADFDuplex**と**MediaBack**要素がありません、すべてのパラメーターで指定されている**MediaFront**されますスキャンも背面に適用されます。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **MediaSides**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **MediaSides**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**指定**](inputsource.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

 

 






