---
title: ServiceCategory
description: ServiceCategory
ms.assetid: 770cb127-808f-4d77-905e-66064553d3d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d1a3b6977ae653396ba2c78986d32e570ae63db
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323649"
---
# <a name="servicecategory"></a>ServiceCategory

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceCategory 要素は、サービスに適用される機能カテゴリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ServiceCategory>
  text
</ServiceCategory>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


ServiceCategory 要素を1つ含める必要があります。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

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
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a></p></td>
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a>要素は、サービスに適用される機能カテゴリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


ここでは、サービスメタデータパッケージ内の[ServiceCategoryList](servicecategorylist.md)要素の使用について説明します。

-   [ServiceCategoryList](servicecategorylist.md)要素の最初の ServiceCategory 要素は、サービスの主な機能カテゴリを指定します。 プライマリ機能カテゴリは、サービスのアドバタイズ、パッケージ化、販売、および最終的にユーザーによって識別される方法と一致する必要があります。

-   サービスはプライマリ機能カテゴリによってのみ定義されるため、 [ServiceCategoryList](servicecategorylist.md)要素では ServiceCategory 要素のインスタンスを1つだけ指定する必要があります。

-   サービスメタデータパッケージの ServiceCategory は、次のいずれかである必要があります。

    -   Network.MobileBroadband

    -   MobileBroadband. CDMA

    -   MobileBroadband. GSM

ServiceCategory 要素が必要です。

 

 





