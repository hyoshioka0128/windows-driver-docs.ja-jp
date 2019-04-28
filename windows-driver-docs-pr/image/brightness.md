---
title: 明るさ要素
description: 省略可能な明るさ要素には、相対的な量を減らすか、スキャンしたドキュメントの明るさを強化するを指定します。
ms.assetid: 15b1b9a1-4735-4a25-837e-8fd9e9ecf88d
keywords:
- 明るさ要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Brightness wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a8f7e845e54a8156d8ede79f74f842fb0ac1ba0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373312"
---
# <a name="brightness-element"></a>明るさ要素


省略可能な**明るさ**要素を減らすか、スキャンしたドキュメントの明るさを強化する相対的な量を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Brightness wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Brightness wscn:Override="" wscn:UsedDefault="">
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
<p>任意。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

明るさの値は、包括的な 1000-1000 の範囲内でなければなりません。**明るさ**

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
<td><p><a href="exposuresettings.md" data-raw-source="[&lt;strong&gt;ExposureSettings&lt;/strong&gt;](exposuresettings.md)"><strong>ExposureSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**明るさ**要素が相対的な量を減らすか、スキャンしたドキュメントの明るさを強化することを示します。 値 0 は、こと、WSD スキャン サービスことは避けてくださいスキャンされた明るさの調整を示します。

すべての WSD スキャン サービスでは、1000 から-1000 などのすべての値をサポートする必要があります。 サービスが、実際にこれらの値を内部的にマップする必要があります**明るさ**スキャン デバイスをサポートする値。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、**明るさ**要素に含まれる、 [ **DocumentFinalParameters** ](documentfinalparameters.md)階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください**DocumentFinalParameters**します。

許可される値をサブセットにできる、**明るさ**要素。

## <a name="see-also"></a>関連項目


[**DocumentFinalParameters**](documentfinalparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






