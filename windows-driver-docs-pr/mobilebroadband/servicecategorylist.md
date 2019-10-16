---
title: ServiceCategoryList
description: ServiceCategoryList
ms.assetid: 69ea35aa-c658-49ed-86bd-815392d157f6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b49386c37c64f7064f9a072061682d78aa3d39a
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323647"
---
# <a name="servicecategorylist"></a>ServiceCategoryList

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceCategoryList 要素は、サービスに適用される1つ以上の機能カテゴリを指定します。 各機能カテゴリは、 [ServiceCategory](servicecategory.md)要素によって指定されます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ServiceCategorylist>
  child element
</ServiceCategorylist>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


[ServiceCategory](servicecategory.md)要素を1つ含める必要があります。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


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
<td><p><a href="servicecategory.md" data-raw-source="[ServiceCategory](servicecategory.md)">ServiceCategory</a></p></td>
<td><p>サービスに適用される1つ以上の機能カテゴリを指定します。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">Serviceinfo</a>要素は、 <a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">serviceinfo XML スキーマ</a>の親要素です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ServiceCategoryList" type="tns:ServiceCategoryListType" />

<xs:complexType name="ServiceCategoryListType">
  <xs:sequence>
    <xs:element name="ServiceCategory" type="tns:ServiceCategoryType" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ここでは、サービスメタデータパッケージ内の ServiceCategoryList 要素の使用について説明します。

-   ServiceCategoryList 要素の最初の[ServiceCategory](servicecategory.md)要素は、サービスの主な機能カテゴリを指定します。 プライマリ機能カテゴリは、サービスのアドバタイズ、パッケージ化、販売、および最終的にユーザーによって識別される方法と一致する必要があります。

-   サービスはプライマリ機能カテゴリによってのみ定義されるため、ServiceCategoryList 要素では[ServiceCategory](servicecategory.md)要素のインスタンスを1つだけ指定する必要があります。

-   サービスメタデータパッケージの[ServiceCategory](servicecategory.md)は、次のいずれかである必要があります。

    -   Network.MobileBroadband

    -   MobileBroadband. CDMA

    -   MobileBroadband. GSM

ServiceCategoryList 要素が必要です。

 

 





