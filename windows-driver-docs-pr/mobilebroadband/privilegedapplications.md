---
title: PrivilegedApplications
description: PrivilegedApplications
ms.assetid: fb0c4a7e-173e-4768-b1ba-a6c5149d61aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362f95feb82243a433469dafd86f5e0c9efd8460
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528854"
---
# <a name="privilegedapplications"></a>PrivilegedApplications

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PrivilegedApplications 要素には、特権を持つモバイル ブロード バンド インターフェイスへのアクセスを許可するアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<PrivilegedApplications>
  Child elements
</PrivilegedApplications>
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
<td><p><a href="package-privapps.md" data-raw-source="[Package](package-privapps.md)">パッケージ</a></p></td>
<td><p>このアプリは、特権を持つモバイル ブロード バンド インターフェイスにアクセスを指定する必要があります。</p></td>
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
<xs:element name="PrivilegedApplications" type="tns:PrivilegedApplicationsType" minOccurs="0" />

<xs:complexType name="PrivilegedApplicationsType">
  <xs:choice>
    <xs:element name="AnyApplication" type="tns:AnyApplicationType" />
    <xs:element name="Package" type="tns:PackageForPrivilegedApplications" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:choice>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


-   PrivilegedApplications 要素により、指定した特権で、モバイル ブロード バンドと SMS Api にアクセスするアプリのアクセス権。

-   パッケージの構造体[Identity](identity-privapps.md)は同じですが、 &lt;Identity&gt;アプリケーション マニフェストの構造内の要素。 アプリケーション マニフェストからの要素をコピーする必要があります。

-   複数のパッケージを指定するには、複数を一覧表示[パッケージ](package-privapps.md)PrivilegedApplications 要素内の要素。

-   パッケージ名、パブリッシャー、およびアプリケーション ID は、Microsoft Store アプリの package.appxmanifest 内の情報と一致する必要があります。 パブリッシャーは、PC にインストールされている発行元証明書も一致する必要があります。

-   Microsoft Store アプリの下に表示されます、 [DeviceCompanionApplications](devicecompanionapplications.md) PrivilegedApplications でも SMS、そのアプリを含むモバイル ブロード バンド インターフェイス特権にアクセスする要素を指定する必要があります要素。

-   Windows デベロッパー センター ダッシュ ボードに、サービス メタデータ パッケージを送信するときに、2 つ以上の特権を持つアプリを宣言できません。 アプリの 1 つには、自動的にダウンロードされる Microsoft Store デバイス アプリのアプリ ID があります。 2 つ目の特権を持つアプリが自動的にダウンロードされませんが、特権を持つモバイル ブロード バンド Api へのアクセスは、アプリがインストールされている場合は。

PrivilegedApplications 要素は省略可能です。

 

 





