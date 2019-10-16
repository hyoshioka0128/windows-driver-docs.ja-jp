---
title: MultipleLocale
description: MultipleLocale
ms.assetid: 95590875-2797-4a73-a211-6102305098f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d21291b9e41d76e14ce03e5f5dd7e60096a57027
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323661"
---
# <a name="multiplelocale"></a>MultipleLocale

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

複数のロケール要素は、サービスメタデータパッケージが複数のロケールをサポートするかどうかを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<MultipleLocale>
  text
</MultipleLocale>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


サービスメタデータパッケージが複数のロケールをサポートしている場合に true になるブール値です。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">Metadatakey</a>要素は、デバイスメタデータパッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア機能の識別子。</p></li>
<li><p>パッケージ内のテキスト文字列の言語固有のロケール。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="MultipleLocale" type ="xs:boolean" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   サービスメタデータパッケージ内の複数のロケールをサポートするには、複数のロケール要素を**true**に設定します。 この要素は、Windows 7 ではサポートされていません。 この要素が指定されていない場合、既定値は true です。

-   1つのロケールのサービスメタデータパッケージと、ユーザーのコンピューターに複数のロケールのサービスメタデータパッケージの両方がある場合、他のすべての順位値が同じ場合、Windows はマルチロケールサービスメタデータパッケージを使用します。

 

 





