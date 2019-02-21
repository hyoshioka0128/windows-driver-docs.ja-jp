---
title: DeviceCompanionApplications
description: DeviceCompanionApplications
ms.assetid: 3e0b21a8-aa1f-4f7a-84fc-447bba172794
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9dcb11928c0985c8c4daf2a621453d82ddb4e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539725"
---
# <a name="devicecompanionapplications"></a>DeviceCompanionApplications

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DeviceCompanionApplications 要素には、PC にオペレーターのモバイル ブロード バンド ハードウェアが検出されたときにダウンロードされるアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<DeviceCompanionApplications>
  child elements
</DeviceCompanionApplications>
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
<td><p><a href="package.md" data-raw-source="[Package](package.md)">パッケージ</a></p></td>
<td><p>Microsoft Store のデバイスのアプリのために使用するパッケージを指定します。</p></td>
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
<xs:element name="DeviceCompanionApplications" type="tns:DeviceCompanionApplicationsType" />

<xs:complexType name="DeviceCompanionApplicationsType">
  <xs:sequence>
    <xs:element name="Package" type="tns:PackageType" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


-   DeviceCompanionApplications 要素を指定する場合は、Windows が演算子のモバイル ブロード バンド ハードウェアを検出すると、指定したアプリがダウンロードされます。

-   パッケージの構造体[Identity](identity.md)と[アプリケーション](application-softwareinfo-schema.md)要素は、アプリケーション マニフェストの構造と同じです。

-   Windows 8、Windows 8.1、および Windows 10、1 つのパッケージと 1 つのアプリケーション ID を指定できます。 指定した場合、2 つ目のパッケージまたはアプリケーション ID は無視されます。

DeviceCompanionApplications 要素は省略可能です。

 

 





