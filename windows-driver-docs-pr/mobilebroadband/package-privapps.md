---
title: パッケージ (SoftwareInfo - priviliged アプリケーション)
description: パッケージ (SoftwareInfo - priviliged アプリケーション)
ms.assetid: c9b22498-a7b6-4e17-9688-536883aa5844
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 152ed8306f713279a042a91c60ff68517758335c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560947"
---
# <a name="package-softwareinfo---priviliged-applications"></a>パッケージ (SoftwareInfo - priviliged アプリケーション)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

パッケージ要素では、特権を持つモバイル ブロード バンド インターフェイスにアクセスできる必要があります、アプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Package>
  child element
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
<td><p><a href="identity-privapps.md" data-raw-source="[Identity](identity-privapps.md)">Id</a></p></td>
<td><p>アプリの発行元を識別します。</p></td>
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
<td><p><a href="privilegedapplications.md" data-raw-source="[PrivilegedApplications](privilegedapplications.md)">PrivilegedApplications</a></p></td>
<td><p>このアプリは、特権を持つモバイル ブロード バンド インターフェイスにアクセスを指定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Package" type="tns:PackageForPrivilegedApplications" maxOccurs="unbounded" />

<xs:complexType name="PackageForPrivilegedApplications">
  <xs:sequence>
    <xs:element name="Identity" type="tns:IdentityForPrivilegedApplicationsType" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


パッケージ要素は省略可能です。

 

 





