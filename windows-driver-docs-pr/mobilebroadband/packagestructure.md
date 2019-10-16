---
title: PackageStructure
description: PackageStructure
ms.assetid: 44be9d7d-79b0-49b6-b427-e729efadb88c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ecc7da5a6be2dbb76eecebf1371c4a7b94777d
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323607"
---
# <a name="packagestructure"></a>PackageStructure

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PackageStructure 要素は、サービスメタデータパッケージによって参照される XML スキーマを指定します。 各 XML スキーマは、 [Metadata](metadata-service-schema.md)要素によって指定されます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<PackageStructure>
  text
  child elements
</PackageStructure>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


4つ以上の[メタデータ](metadata-service-schema.md)要素が必要です。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


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
<td><p><a href="metadata-service-schema.md" data-raw-source="[Metadata](metadata-service-schema.md)">Metadata</a></p></td>
<td><p><a href="metadata-service-schema.md" data-raw-source="[Metadata](metadata-service-schema.md)">Metadata</a>要素は、デバイスメタデータパッケージを通じて参照される XML スキーマを指定します。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a></p></td>
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">Packageinfo</a>要素は、 <a href="packageinfo-xml-schema.md" data-raw-source="[PackageInfo XML schema](packageinfo-xml-schema.md)">packageinfo XML スキーマ</a>の親要素です。 PackageInfo 要素の子要素は、デバイスメタデータパッケージの属性を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


PackageStructure 要素内では、少なくとも4つの[メタデータ](metadata-service-schema.md)要素を指定する必要があります。 各インスタンスでは、サービスメタデータパッケージの作成に使用される必要な XML スキーマのいずれかを指定する必要があります。

-   [PackageInfo XML スキーマ](packageinfo-xml-schema.md)

-   [ServiceInfo XML スキーマ](serviceinfo-xml-schema.md)

-   [ソフトウェア情報 XML スキーマ](softwareinfo-xml-schema.md)

-   [MobileBroadbandInfo XML スキーマ](mobilebroadbandinfo-xml-schema.md)

PackageStructure 要素が必要です。

 

 





