---
title: PrivilegedApplications
description: PrivilegedApplications
ms.assetid: fb0c4a7e-173e-4768-b1ba-a6c5149d61aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362f95feb82243a433469dafd86f5e0c9efd8460
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323609"
---
# <a name="privilegedapplications"></a>PrivilegedApplications

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PrivilegedApplications 要素は、特権のあるモバイルブロードバンドインターフェイスへのアクセスが許可されるアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<PrivilegedApplications>
  Child elements
</PrivilegedApplications>
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
<td><p><a href="package-privapps.md" data-raw-source="[Package](package-privapps.md)">[パッケージ]</a></p></td>
<td><p>特権のあるモバイルブロードバンドインターフェイスにアクセスできる必要があるアプリ。</p></td>
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
<td><p><a href="softwareinfo.md" data-raw-source="[SoftwareInfo](softwareinfo.md)">ソフトウェア情報</a></p></td>
<td><p><a href="softwareinfo-xml-schema.md" data-raw-source="[SoftwareInfo XML schema](softwareinfo-xml-schema.md)">ソフトウェア情報 XML スキーマ</a>の親要素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   PrivilegedApplications 要素を使用すると、指定したアプリは、特権アクセス権を持つモバイルブロードバンドおよび SMS Api にアクセスできます。

-   パッケージ[id](identity-privapps.md)の構造は、アプリケーションマニフェスト構造の &lt;id&gt; 要素と同じです。 アプリケーションマニフェストから要素をコピーする必要があります。

-   複数のパッケージを指定するには、PrivilegedApplications 要素内の複数の[Package](package-privapps.md)要素を一覧表示します。

-   パッケージ名、発行元、およびアプリケーション ID は、Microsoft Store アプリの package.appxmanifest の情報と一致している必要があります。 また、パブリッシャーは、PC にインストールされている発行元の証明書と一致している必要があります。

-   [DeviceCompanionApplications](devicecompanionapplications.md)要素の下に一覧表示されている Microsoft Store アプリが SMS を含む Privileged Mobile ブロードバンドインターフェイスにアクセスできるようにするには、PrivilegedApplications 要素でそのアプリも指定する必要があります。

-   Windows デベロッパーセンターのダッシュボードにサービスメタデータパッケージを送信するときに、2つ以上の特権のあるアプリを宣言することはできません。 アプリの1つは、自動的にダウンロードされる Microsoft Store デバイスアプリのアプリ ID である必要があります。 2番目の特権を持つアプリは自動的にはダウンロードされませんが、アプリがインストールされている場合は、特権のあるモバイルブロードバンド Api にアクセスします。

PrivilegedApplications 要素は省略可能です。

 

 





