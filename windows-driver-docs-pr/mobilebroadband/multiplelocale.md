---
title: MultipleLocale
description: MultipleLocale
ms.assetid: 95590875-2797-4a73-a211-6102305098f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d21291b9e41d76e14ce03e5f5dd7e60096a57027
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574556"
---
# <a name="multiplelocale"></a>MultipleLocale

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MultipleLocale 要素では、サービス メタデータ パッケージに複数のロケールがサポートしているかどうかを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<MultipleLocale>
  text
</MultipleLocale>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


サービス メタデータ パッケージは、複数のロケールをサポートしている場合は true になるブール値。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>要素は、デバイス メタデータ パッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア関数の識別子。</p></li>
<li><p>言語固有のロケールをパッケージ内のテキスト文字列。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="MultipleLocale" type ="xs:boolean" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   サービス メタデータ パッケージに複数のロケールをサポートするために MultipleLocale 要素を設定**true**します。 この要素は、Windows 7 ではサポートされていません。 この要素が指定されていない場合は既定値は true です。

-   Windows に 1 つのロケールのサービス メタデータ パッケージとユーザーのコンピューターに複数のロケールのサービス メタデータ パッケージの両方が、他のすべての順位値が同じ場合、複数のロケールのサービス メタデータ パッケージを使用します。

 

 





