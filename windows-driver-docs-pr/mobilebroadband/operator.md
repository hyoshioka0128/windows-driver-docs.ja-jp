---
title: 演算子
description: 演算子
ms.assetid: 770ad50d-d42d-49ad-a302-e839a0ca1fb4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbcdd8a09ec6e0235d0be7dbdb76115614ac561c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375748"
---
# <a name="operator"></a>演算子


演算子要素には、APN データベースに含まれている演算子の詳細を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Operator name=”xs:string” AccountExperienceURL=”xs:anyURI” OperatorGUID=”GUID”>
  child elements
</Operator>
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
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p>名前と演算子の国/地域。</p>
<p>以下に例を示します。Contoso (アルゼンチン)</p></td>
</tr>
<tr class="even">
<td><p>AccountExperienceURL</p></td>
<td><p>xs:anyURI</p></td>
<td><p>X</p></td>
<td><p>モバイル ブロード バンドを構成するために使用するオペレーターの web サイトの URL。</p></td>
</tr>
<tr class="odd">
<td><p>OperatorGUID</p></td>
<td><p>GUID</p></td>
<td><p>X</p></td>
<td><p>演算子を識別するために使用される GUID。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="hardwareidlist-apnxml.md" data-raw-source="[HardwareIdList](hardwareidlist-apnxml.md)">HardwareIdList</a></p></td>
<td><p>ハードウェア、オペレーターに割り当てられている Id の一覧。</p></td>
</tr>
<tr class="even">
<td><p><a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a></p></td>
<td><p>アクセス文字列のリスト。</p></td>
</tr>
<tr class="odd">
<td><p><a href="trustedcertificatelist.md" data-raw-source="[TrustedCertificateList](trustedcertificatelist.md)">TrustedCertificateList</a></p></td>
<td><p>演算子によって所有されている購入 web サイトによってアカウントのプロビジョニングを提供することを検証に使用される信頼された証明書の一覧。</p></td>
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
<td><p><a href="operatorlist.md" data-raw-source="[OperatorList](operatorlist.md)">OperatorList</a></p></td>
<td><p>親要素、 <a href="apn-xml-schema.md" data-raw-source="[APN XML schema](apn-xml-schema.md)">APN の XML スキーマ</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Operator">
  <xs:complexType>
    <xs:sequence>
      <xs:element ref="HardwareIdList"/>
      <xs:element ref="ConnectionInfoList"/>
      <xs:element ref="TrustedCertificateList" minOccurs="0"/>
    </xs:sequence>
    <xs:attribute name="name" type="xs:string" use="required"/>
    <xs:attribute name="AccountExperienceURL" type="xs:anyURI" use="optional"/>
    <xs:attribute name="OperatorGUID" type="GUID" use="optional"/>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


演算子の要素が必要です。

 

 





