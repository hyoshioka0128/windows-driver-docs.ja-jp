---
title: MobileBroadbandProfiles
description: MobileBroadbandProfiles
ms.assetid: 251ece1e-67ec-48d3-977a-f033f1bff8c4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74e9375244be6c6acf2beaf099960118687f6218
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528337"
---
# <a name="mobilebroadbandprofiles"></a>MobileBroadbandProfiles

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MobileBroadbandProfiles 要素には、購入および使用するインターネット モバイル ブロード バンド プロファイル ファイルを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<MobileBroadbandProfiles>
  child elements
</MobileBroadbandProfiles>
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
<td><p><a href="purchase.md" data-raw-source="[Purchase](purchase.md)">購入</a></p></td>
<td><p>使用する購入モバイル ブロード バンド プロファイル ファイルを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="internet.md" data-raw-source="[Internet](internet.md)">インターネット</a></p></td>
<td><p>使用するインターネット モバイル ブロード バンド プロファイル ファイルを指定します。</p></td>
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
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a></p></td>
<td><p>購入して、インターネットを指定するためのモバイル ブロード バンド プロファイルまたは標準ユーザーが暗証番号 (pin) を実行するかどうかの操作のロックを解除します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="MobileBroadbandProfiles" type="tns:MobileBroadbandProfilesType" minOccurs="0" />

<xs:complexType name="MobileBroadbandProfilesType">
  <xs:sequence>
    <xs:element name="Purchase" type="tns:FileType" minOccurs="0" />
    <xs:element name="Internet" type="tns:FileType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


MobileBroadbandProfiles 要素は省略可能です。

 

 





