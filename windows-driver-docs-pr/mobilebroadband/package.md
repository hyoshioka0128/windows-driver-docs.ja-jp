---
title: パッケージ (SoftwareInfo)
description: パッケージ (SoftwareInfo)
ms.assetid: f15f0ffe-593d-4007-8002-4d593d18dd9a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 612d0a90275e67c0988c8254682a6f7b3cb2d065
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538883"
---
# <a name="package-softwareinfo"></a>パッケージ (SoftwareInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

パッケージ要素では、PC にオペレーターのモバイル ブロード バンド ハードウェアが検出されたときにダウンロードされるアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Package>
  child elements
</Package>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

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
<td><p><a href="identity.md" data-raw-source="[Identity](identity.md)">Id</a></p></td>
<td><p>アプリの発行元を識別します。</p></td>
</tr>
<tr class="even">
<td><p><a href="applications.md" data-raw-source="[Applications](applications.md)">アプリケーション</a></p></td>
<td><p>このアプリは、モバイル ブロード バンド ハードウェア デバイスが検出されたときに、ダウンロードになります。</p></td>
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
<td><p><a href="softwareinfo.md" data-raw-source="[SoftwareInfo](softwareinfo.md)">SoftwareInfo</a></p></td>
<td><p>親要素、 <a href="softwareinfo-xml-schema.md" data-raw-source="[SoftwareInfo XML schema](softwareinfo-xml-schema.md)">SoftwareInfo XML スキーマ</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Package" type="tns:PackageType" maxOccurs="unbounded" />

<xs:complexType name="PackageType">
    <xs:sequence>
        <xs:element name="Identity" type="tns:IdentityType" />
        <xs:element name="Applications" type="tns:ApplicationsType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


パッケージ要素は省略可能です。

 

 





