---
title: AutoplayType
description: AutoplayType
ms.assetid: 06097d2a-7883-416e-a81d-3a8abccc620b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53f7e8c9e9044c3f21ddc7918be79c63a4088a39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531759"
---
# <a name="autoplaytype"></a>AutoplayType

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

AutoplayType 要素は、自動再生イベントがデバイス イベントまたはコンテンツのイベントであるかどうかを指定します。 自動再生では、デバイスの種類を決定し、ボリューム以外のデバイスのデバイスのイベントまたはボリュームのデバイスのコンテンツのイベントを発生させます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<AutoplayType>
  type
</AutoplayType>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


「コンテンツ」、"Device"の値または値を持つ文字列。

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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>ユーザーはデバイスをプラグインと、推奨される自動再生操作として表示される UWP デバイス アプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="AutoplayType" type="tns:AutoplayTypeType" />

<xs:simpleType name="AutoplayTypeType">
  <xs:restriction base="xs:string">
     <xs:enumeration value="Device" />
     <xs:enumeration value="Content" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


AutoplayType 要素は省略可能です。

 

 





