---
title: HardwareIdList (PackageInfo)
description: HardwareIdList (PackageInfo)
ms.assetid: 32bd11f8-767f-4082-b753-efa9debf23cc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15f45b60560676e26d7c7fcd12879058d1f44646
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559101"
---
# <a name="hardwareidlist-packageinfo"></a>HardwareIdList (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

HardwareIDList 要素には、サービス メタデータ パッケージの 1 つまたは複数のハードウェアの識別文字列を指定します。 各文字列がで指定された、 [HardwareID](hardwareid.md)要素。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<HardwareIDList>
  child elements
</HardwareIDList>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


1 つ以上含める必要があります[HardwareID](hardwareid.md)要素。

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
<td><p><a href="hardwareid.md" data-raw-source="[HardwareID](hardwareid.md)">HardwareID</a></p></td>
<td><p><a href="hardwareid.md" data-raw-source="[HardwareID](hardwareid.md)">HardwareID</a>要素は、モバイル ネットワーク オペレーターを表します。</p></td>
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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>要素は、デバイス メタデータ パッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア関数の識別子。</p></li>
<li><p>言語固有のロケールをパッケージ内のテキスト文字列。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="HardwareIDList" type="tns:HardwareIDListType" />

<xs:complexType name="HardwareIDListType">
  <xs:sequence>
    <xs:element name="HardwareID" type="tns:HardwareIDType" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


HardwareIDList 要素が必要です。

 

 





