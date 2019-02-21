---
title: ServiceDescription1
description: ServiceDescription1
ms.assetid: 4451c429-3b89-47d6-ba21-ab30919e5ff8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73a182280237080e11e124ab6ce6397a92e3ff79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556904"
---
# <a name="servicedescription1"></a>ServiceDescription1

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceDescription1 要素には、サービスに関する説明情報を指定します。 これは、ワイヤレス ワイド エリア ネットワーク (WWAN) 接続プロファイルの説明フィールドに適用されます。 エンドユーザーにユーザー インターフェイスには表示されませんし、空白のままにする必要があります。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ServiceDescription1>
  text
</ServiceDescription1>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


長さは 1024 より小さい文字である文字列。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>要素は、親要素の<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML スキーマ</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ServiceDescription1" type="tns:ServiceDescriptionType" minOccurs="0"/>

<xs:simpleType name="ServiceDescriptionType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1"/>
    <xs:maxLength value="1024"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


ServiceDescription1 要素は、すべてのユーザー インターフェイスでエンドユーザーには表示されません。

ServiceDescription1 要素は省略可能で、空白のままにする必要があります。

 

 





