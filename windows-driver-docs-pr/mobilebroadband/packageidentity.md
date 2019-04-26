---
title: PackageIdentity
description: PackageIdentity
ms.assetid: b5533962-ea42-416e-bbd8-ce9dce1a9a40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb842736555a1b824dcefd98ee0bd1590179cba5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344293"
---
# <a name="packageidentity"></a>PackageIdentity

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PackageIdentity 要素には、ユーザーはデバイスをプラグインと、推奨される自動再生操作として表示される UWP デバイス アプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<PackageIdentity Name=”tns:PackageNameType” Publisher=”tns:PublisherType” />
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
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>名前</p></td>
<td><p>tns:PackageNameType</p></td>
<td><p>〇</p></td>
<td><p>この要素は、「解説」で説明されている、アプリ マニフェストの Identity 要素の Name 属性からコピーします。</p></td>
</tr>
<tr class="even">
<td><p>発行元</p></td>
<td><p>tns:PublisherType</p></td>
<td><p>〇</p></td>
<td><p>この要素は、「解説」で説明されている、アプリ マニフェストの Identity 要素の Publisher 属性からコピーします。</p></td>
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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>ユーザーはデバイスをプラグインと、推奨される自動再生操作として表示される UWP デバイス アプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="PackageIdentity" type="tns:PackageIdentityType" />

  <xs:complexType name="PackageIdentityType">
    <xs:attribute name="Name" type="tns:PackageNameType" use="required" />
    <xs:attribute name="Publisher" type="tns:PublisherType" use="required" />
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
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


アプリケーション マニフェストの名前とパブリッシャーの属性をコピー &lt;Identity&gt;要素の後、アプリを関連付けるプロセスは、アプリ マニフェストを更新するため、アプリは Microsoft Store に関連付けられた要素。

方法の例を次に示します&lt;Identity&gt;要素は、アプリ マニフェスト内になります。

``` syntax
<Identity Name="64022FABRIKAM.FabrikamDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" Version="1.0.0.0" />
```

PackageIdentity 要素は省略可能です。

 

 





