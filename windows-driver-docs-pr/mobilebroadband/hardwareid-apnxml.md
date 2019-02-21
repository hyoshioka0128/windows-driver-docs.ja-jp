---
title: HardwareId (APN 要素)
description: HardwareId (APN 要素)
ms.assetid: 9c09915c-d0f6-4ddf-b2e1-79f00599c3a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63c8c0e1d6b997622f6118369835d3cea6870fc4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561055"
---
# <a name="hardwareid-apn-element"></a>HardwareId (APN 要素)


HardwareId 要素は、指定したオペレーターの HWID を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<HardwareId>
...insert text here
</HardwareId>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


エンコードされたハードウェア ID を表す文字列です。 適切なハードウェア ID の値を生成するには、複雑なアルゴリズムが含まれます。 Mbidgenerator.exe を使用して、ハードウェア Id を生成することをお勧めします。

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
<td><p><a href="hardwareidlist-apnxml.md" data-raw-source="[HardwareIdList](hardwareidlist-apnxml.md)">HardwareIdList</a></p></td>
<td><p>演算子のハードウェア Id の一覧を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element ref="HardwareId" maxOccurs="unbounded"/>

<xs:element name="HardwareId">
  <xs:complexType>
    <xs:attribute name="id" type="xs:string" use="required"/>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


HardwareId 要素には、次のいずれかを表す必要があります。

-   GSM ネットワーク:IMSI 範囲

-   GSM ネットワーク:ICCID の範囲

-   CDMA ネットワーク:プロバイダー名の値

-   CDMA ネットワーク:プロバイダー ID の値 (SID とも呼ばれます)

HardwareId 要素が必要です。

 

 





