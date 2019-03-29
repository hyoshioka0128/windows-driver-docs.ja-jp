---
title: PackageStructure
description: PackageStructure
ms.assetid: 44be9d7d-79b0-49b6-b427-e729efadb88c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ecc7da5a6be2dbb76eecebf1371c4a7b94777d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570870"
---
# <a name="packagestructure"></a>PackageStructure

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PackageStructure 要素には、サービス メタデータ パッケージによって参照される XML スキーマを指定します。 使用して各 XML スキーマを指定、[メタデータ](metadata-service-schema.md)要素。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<PackageStructure>
  text
  child elements
</PackageStructure>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


次の 4 つまたは複数[メタデータ](metadata-service-schema.md)要素が必要です。

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
<td><p><a href="metadata-service-schema.md" data-raw-source="[Metadata](metadata-service-schema.md)">メタデータ</a></p></td>
<td><p><a href="metadata-service-schema.md" data-raw-source="[Metadata](metadata-service-schema.md)">メタデータ</a>要素は、デバイス メタデータ パッケージを通じて参照されている XML スキーマを指定します。</p></td>
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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>要素は、親要素の<a href="packageinfo-xml-schema.md" data-raw-source="[PackageInfo XML schema](packageinfo-xml-schema.md)">PackageInfo XML スキーマ</a>します。 PackageInfo の要素の子要素は、デバイス メタデータ パッケージの属性を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="PackageStructure" type="tns:PackageStructureType" />

<xs:complexType name="PackageStructureType">
  <xs:sequence>
    <xs:element name="Metadata" type="tns:MetadataType" minOccurs="2" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


4 つのインスタンスの最小値、[メタデータ](metadata-service-schema.md)PackageStructure 要素内に要素を指定する必要があります。 各インスタンスは、サービス メタデータ パッケージの作成に使用される必須の XML スキーマのいずれかを指定する必要があります。

-   [PackageInfo の XML スキーマ](packageinfo-xml-schema.md)

-   [ServiceInfo XML スキーマ](serviceinfo-xml-schema.md)

-   [SoftwareInfo XML スキーマ](softwareinfo-xml-schema.md)

-   [MobileBroadbandInfo XML スキーマ](mobilebroadbandinfo-xml-schema.md)

PackageStructure 要素が必要です。

 

 





