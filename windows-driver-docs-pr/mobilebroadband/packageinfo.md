---
title: PackageInfo
description: PackageInfo
ms.assetid: b74bfc2a-6779-4f53-9e46-71ca8ae26fda
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab8f1afddc41fd561a0baa09ac9a69d08a814019
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323611"
---
# <a name="packageinfo"></a>PackageInfo

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PackageInfo 要素は、 [PACKAGEINFO XML スキーマ](packageinfo-xml-schema.md)の親要素です。 PackageInfo 要素の子要素は、サービスメタデータパッケージの属性を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<PackageInfo>
  child elements
</PackageInfo>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

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
<td><p><a href="metadatabuilderinformation.md" data-raw-source="[MetadataBuilderInformation](metadatabuilderinformation.md)">MetadataBuilderInformation</a></p></td>
<td><p><a href="metadatabuilderinformation.md" data-raw-source="[MetadataBuilderInformation](metadatabuilderinformation.md)">MetadataBuilderInformation</a>要素は、サービスメタデータパッケージを作成したアプリケーションに関する情報を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">Metadatakey</a>要素は、サービスメタデータパッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア機能の識別子。</p></li>
<li><p>パッケージ内のテキスト文字列の言語固有のロケール。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a></p></td>
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">Packagestructure</a>要素は、サービスメタデータパッケージによって参照される XML スキーマを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a>要素は、子要素を介して、デバイスメタデータキャッシュ内のサービスメタデータパッケージを追跡するために使用されるデータを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


親要素はありません。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="PackageInfo" type="tns:PackageInfoType" />

<xs:complexType name="PackageInfoType">
  <xs:sequence>
    <xs:element name="MetadataKey" type="tns:MetadataKeyType" />
    <xs:element name="PackageStructure" type="tns:PackageStructureType" />
    <xs:element name="Relationships" type="tns:RelationshipsType" minOccurs="0" />
    <xs:element name="MetadataBuilderInformation" type="tns:MetadataBuilderInformationType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0"
      maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


PackageInfo 要素には、 [Metadatakey](metadatakey.md)、 [packageinfo](packagestructure.md)、および[リレーションシップ](relationships.md)要素の1つのインスタンスが含まれている必要があります。

 

 





