---
title: MetadataBuilderInformation
description: MetadataBuilderInformation
ms.assetid: 94403994-2165-405e-bfa0-974af8e241fe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6e5f20a8fc4a03a74c32846298d0b4365af7827
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530085"
---
# <a name="metadatabuilderinformation"></a>MetadataBuilderInformation

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MetadataBuilderInformation 要素には、デバイス メタデータ パッケージを作成したアプリケーションに関する情報を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<MetadataBuilderInformation>
  text
  child elements
</MetadataBuilderInformation>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


1 ~ 256 印刷可能な文字範囲を含む文字列。

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
<td><p><a href="application-service-schema.md" data-raw-source="[Application](application-service-schema.md)">アプリケーション</a></p></td>
<td><p><a href="application-service-schema.md" data-raw-source="[Application](application-service-schema.md)">アプリケーション</a>要素は、サービス メタデータ パッケージを作成したアプリケーション ソフトウェアの名前を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="version.md" data-raw-source="[Version](version.md)">バージョン</a></p></td>
<td><p><a href="version.md" data-raw-source="[Version](version.md)">バージョン</a>要素は、サービス メタデータ パッケージを作成したアプリケーション ソフトウェアのバージョンを指定します。</p></td>
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
<xs:element name="MetadataBuilderInformation" type="tns:MetadataBuilderInformationType" minOccurs="0" /> 

<xs:complexType name="MetadataBuilderInformationType">
  <xs:sequence>
  <xs:element name="Application" type="tns:ApplicationType" />
  <xs:element name="Version" type="tns:VersionType" />
  <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType> 

<xs:simpleType name="ApplicationType">
  <xs:restriction base="xs:string">
  <xs:minLength value="1" />
  <xs:maxLength value="256" />
  </xs:restriction>
</xs:simpleType> 

<xs:simpleType name="VersionType">
   <xs:restriction base="xs:string">
     <xs:minLength value="1" />
     <xs:maxLength value="256" />
   </xs:restriction> 
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


MetadataBuilderInformation 要素は、オペレーティング システムのすべてのコンポーネントでは使用されません。 OEM、IHV、ISV によって使用するために予約されています。

 

 





