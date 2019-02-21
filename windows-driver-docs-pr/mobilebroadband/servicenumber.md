---
title: ServiceNumber
description: ServiceNumber
ms.assetid: 7e02557a-34e5-41f2-9a27-122a144c2ab9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc89b599bf9bc0cd4a70d1945e6178f14011e399
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528608"
---
# <a name="servicenumber"></a>ServiceNumber

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceNumber 要素には、携帯電話会社を表す一意の自動生成された GUID を指定します。 この GUID は、存在する必要があり、アカウント プロビジョニングのメタデータが、PC をそのファイルで特定した配送業者 ID で宣言されている GUID 値の一致を確実に適用される場合にチェックします。 アカウント プロビジョニングのメタデータは、モバイル ブロード バンド アプリまたは演算子の web サイトによって生成されます。 アカウント プロビジョニングのメタデータについては、「[アカウント プロビジョニング](account-provisioning.md)します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ServiceNumber>
  text
</ServiceNumber>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


文字列[GUIDType](guidtype-serviceinfo.md)します。

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
<xs:element name="ServiceNumber" type ="tns:ServiceNumberType" />

<xs:simpleType name="ServiceNumberType">
  <xs:union memberTypes="tns:GUIDType xs:string" />
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


ServiceNumber 要素が必要です。

 

 





