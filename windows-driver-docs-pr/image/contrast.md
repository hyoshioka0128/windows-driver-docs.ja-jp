---
title: コントラスト要素
description: 省略可能なコントラスト要素には、相対的な量を減らすか、スキャンしたドキュメントのコントラストを強化するを指定します。
ms.assetid: c40e824f-4e10-4590-a524-ff69a21a4499
keywords:
- デバイスのイメージのコントラスト要素
topic_type:
- apiref
api_name:
- wscn Contrast wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09ce7469fdffcb588e122929e669287297204f5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368553"
---
# <a name="contrast-element"></a>コントラスト要素


省略可能な**コントラスト**要素を減らすか、スキャンしたドキュメントのコントラストを強化する相対的な量を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Contrast wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Contrast wscn:Override="" wscn:UsedDefault="">
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
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

コントラスト値は、包括的な 1000-1000 の範囲内でなければなりません。

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

**コントラスト**要素を拡張またはスキャンしたドキュメントのコントラストを下げるに相対的な量を示します。 値 0 は、WSD スキャン サービスことは避けてくださいスキャンしたコントラストを調整を示します。

すべて WSD スキャン サービスする必要がありますすべての値間とサポートなど、-1000 を 1000 にします。 サービスが、実際にこれらの値を内部的にマップする必要があります**コントラスト**スキャン デバイスをサポートする値。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、**コントラスト**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**DocumentFinalParameters**](documentfinalparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






