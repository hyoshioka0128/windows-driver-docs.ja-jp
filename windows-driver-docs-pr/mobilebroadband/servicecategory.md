---
title: ServiceCategory
description: ServiceCategory
ms.assetid: 770cb127-808f-4d77-905e-66064553d3d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d1a3b6977ae653396ba2c78986d32e570ae63db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580502"
---
# <a name="servicecategory"></a>ServiceCategory

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceCategory 要素には、サービスに適用される機能のカテゴリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ServiceCategory>
  text
</ServiceCategory>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


1 つの ServiceCategory 要素を含める必要があります。

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
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a></p></td>
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a>要素は、サービスに適用される機能のカテゴリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ServiceCategory" type="tns:ServiceCategoryType" maxOccurs="unbounded" />

<xs:simpleType name="ServiceCategoryType">
    <xs:union memberTypes="tns:ServiceCategoryTypeEnumeration xs:string"/>
</xs:simpleType>

<xs:simpleType name="ServiceCategoryTypeEnumeration">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Network"/>
    <xs:enumeration value="Network.MobileBroadband"/>
    <xs:enumeration value="Other"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


次の使用について説明して、 [ServiceCategoryList](servicecategorylist.md)サービス メタデータ パッケージ内の要素。

-   最初の ServiceCategory 要素、 [ServiceCategoryList](servicecategorylist.md)要素が、サービスの主な機能のカテゴリを指定します。 主な機能のカテゴリは、方法、サービスが提供、パッケージ化、販売、および最終的にユーザーによって識別と一致する必要があります。

-   サービスは、その主な機能のカテゴリによってのみ定義される、ため ServiceCategory 要素の 1 つだけのインスタンスを指定する必要があります、 [ServiceCategoryList](servicecategorylist.md)要素。

-   サービス メタデータ パッケージの ServiceCategory は、次のいずれかである必要があります。

    -   Network.MobileBroadband

    -   Network.MobileBroadband.CDMA

    -   Network.MobileBroadband.GSM

ServiceCategory 要素が必要です。

 

 





