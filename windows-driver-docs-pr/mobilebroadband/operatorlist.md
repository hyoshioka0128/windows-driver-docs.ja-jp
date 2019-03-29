---
title: OperatorList
description: OperatorList
ms.assetid: 28006331-aa65-4b33-ae94-a027c8a60d48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f74580ab4eca2660504b1c1b43fd588176fc4587
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582113"
---
# <a name="operatorlist"></a>OperatorList


OperatorList 要素には、APN データベースに含まれる演算子の一覧を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<OperatorList>
  child elements
</OperatorList>
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
<td><p><a href="operator.md" data-raw-source="[Operator](operator.md)">演算子</a></p></td>
<td><p>演算子の詳細を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


親要素はありません。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="OperatorList">
  <xs:complexType>
    <xs:sequence>
      <xs:element ref="Operator" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


OperatorList 要素が必要です。

 

 





