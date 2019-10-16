---
title: DeviceCompanionApplications
description: DeviceCompanionApplications
ms.assetid: 3e0b21a8-aa1f-4f7a-84fc-447bba172794
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9dcb11928c0985c8c4daf2a621453d82ddb4e4
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323621"
---
# <a name="devicecompanionapplications"></a>DeviceCompanionApplications

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DeviceCompanionApplications 要素は、PC でオペレーターのモバイルブロードバンドハードウェアが検出されたときにダウンロードされるアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<DeviceCompanionApplications>
  child elements
</DeviceCompanionApplications>
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
<td><p><a href="package.md" data-raw-source="[Package](package.md)">Package</a></p></td>
<td><p>Microsoft Store デバイスアプリに使用されるパッケージを指定します。</p></td>
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
<xs:element name="DeviceCompanionApplications" type="tns:DeviceCompanionApplicationsType" />

<xs:complexType name="DeviceCompanionApplicationsType">
  <xs:sequence>
    <xs:element name="Package" type="tns:PackageType" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   DeviceCompanionApplications 要素を指定すると、Windows がオペレーターのモバイルブロードバンドハードウェアを検出すると、指定したアプリがダウンロードされます。

-   パッケージ[id](identity.md)と[アプリケーション](application-softwareinfo-schema.md)要素の構造は、アプリケーションマニフェストの構造と同じです。

-   Windows 8、Windows 8.1、および Windows 10 では、1つのパッケージと1つのアプリケーション ID のみを指定できます。 2番目のパッケージまたはアプリケーション ID は、指定した場合は無視されます。

DeviceCompanionApplications 要素は省略可能です。

 

 





