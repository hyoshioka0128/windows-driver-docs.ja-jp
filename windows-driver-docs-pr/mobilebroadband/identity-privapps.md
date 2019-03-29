---
title: Identity (SoftwareInfo - 特権アプリケーション)
description: Identity (SoftwareInfo - 特権アプリケーション)
ms.assetid: 405ec2ee-ea4a-468b-b75b-365ffce03cdb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94396720678c3baf9701ac801379e4a4a5b93a35
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464370"
---
# <a name="identity-softwareinfo---priviliged-applications"></a>Identity (SoftwareInfo - 特権アプリケーション)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Id 要素では、パブリッシャーの id とアプリケーション マニフェストのアプリの名前を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Identity Name=”tns:AsciiIdentifierType” Publisher=”tns:DistinguishedNameType” AccessCustomDriver=”xs:boolean” />
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


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
<th>型</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>名前</p></td>
<td><p>tns:AsciiIdentifierType</p></td>
<td><p>はい</p></td>
<td><p>マニフェスト ファイルをアプリで指定されているアプリの名前。</p></td>
</tr>
<tr class="even">
<td><p>パブリッシャー</p></td>
<td><p>tns:DistinguishedNameType</p></td>
<td><p>はい</p></td>
<td><p>アプリの発行元の id。</p></td>
</tr>
<tr class="odd">
<td><p>AccessCustomDriver</p></td>
<td><p>xs:boolean</p></td>
<td><p>いいえ</p></td>
<td><p>アプリは、カスタム ドライバーにアクセスする必要がある場合、は、この値を設定<strong>true</strong>します。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="package-privapps.md" data-raw-source="[Package](package-privapps.md)">[パッケージ]</a></p></td>
<td><p>特権のあるモバイル ブロード バンド インターフェイスにアクセスできる必要があります、アプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Identity" type="tns:IdentityForPrivilegedApplicationsType" />

<xs:complexType name="IdentityForPrivilegedApplicationsType">
  <xs:attribute name="Name" type="tns:PackageNameType" use="required"/>
  <xs:attribute name="Publisher" type="tns:PublisherType" use="required"/>
  <xs:attribute name="AccessCustomDriver" type="xs:boolean" />
</xs:complexType>

<xs:simpleType name="PackageNameType">
  <xs:restriction base="tns:AsciiIdentifierType">
    <xs:minLength value="3"/>
    <xs:maxLength value="50"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="PublisherType">
  <xs:restriction base="tns:DistinguishedNameType">
    <xs:maxLength value="8192"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="AsciiIdentifierType">
  <xs:restriction base="tns:AllowedAsciiCharSetType">
    <xs:pattern value="[^_ ]+"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="DistinguishedNameType">
  <xs:restriction base="tns:NonEmptyStringType">
    <xs:pattern value="(CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")(, ((CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")))*"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="NonEmptyStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1"/>
    <xs:maxLength value="32767"/>
    <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="AllowedAsciiCharSetType">
  <xs:restriction base="tns:NonEmptyStringType">
    <xs:pattern value="[-_. A-Za-z0-9]+"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


Id 要素は省略可能です。

 

 





