---
title: リレーションシップ
description: リレーションシップ
ms.assetid: 78443a49-96c6-45d9-a4f3-8213005f82d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e6b2714071466b7bf988dd040d3dab647c32ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557253"
---
# <a name="relationships"></a>リレーションシップ

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Relationships 要素には、デバイスのメタデータ キャッシュ内のデバイス メタデータ パッケージを追跡するために使用されるデータを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Relationships>
  text
  child elements
</Relationships>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


これを指定する必要があります Relationships 要素が指定されているかどうか、 [ExperienceID](experienceid.md)要素、または[LanguageNeutralIdentifier](languageneutralidentifier.md)要素、またはその両方です。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


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
<td><p><a href="experienceid.md" data-raw-source="[ExperienceID](experienceid.md)">ExperienceID</a></p></td>
<td><p><a href="experienceid.md" data-raw-source="[ExperienceID](experienceid.md)">ExperienceID</a>要素は、Windows デベロッパー センター ダッシュ ボードで管理されている GUID を指定します。 この GUID は、パッケージのロケールに依存しない同じデバイス識別子の 1 つまたは複数のメタデータ パッケージをグループ化に使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="languageneutralidentifier.md" data-raw-source="[LanguageNeutralIdentifier](languageneutralidentifier.md)">LanguageNeutralIdentifier</a></p></td>
<td><p><a href="languageneutralidentifier.md" data-raw-source="[LanguageNeutralIdentifier](languageneutralidentifier.md)">LanguageNeutralIdentifier</a>要素がそのロケールに依存しないデバイス メタデータ パッケージを識別する GUID を指定します。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a></p></td>
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>要素は、サービス メタデータ パッケージの属性を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Relationships" type="tns:RelationshipsType" minOccurs="0" />

<xs:complexType name="RelationshipsType">
  <xs:sequence>
    <xs:element name="ExperienceID" type="tns:GUIDType" minOccurs="0" />
    <xs:element name="LanguageNeutralIdentifier" type="tns:GUIDType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded"
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


Relationships 要素の子要素 ([ExperienceID](experienceid.md)と[LanguageNeutralIdentifier](languageneutralidentifier.md)) オペレーティング システムは、デバイス メタデータのクエリを使用して別の検索キーをパッケージに提供デバイスのメタデータ キャッシュ内にインストールされます。

 

 





