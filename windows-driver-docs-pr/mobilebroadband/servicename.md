---
title: ServiceName
description: ServiceName
ms.assetid: 50a3c985-c798-4287-87c6-ffa9a3c2058a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41290acc4a5bae7996dd69bdb5cf436beff1ca45
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323588"
---
# <a name="servicename"></a>ServiceName

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceName 要素は現在使用されていません。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ServiceName>
  text
</ServiceName>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


長さが200文字未満の文字列。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">Serviceinfo</a>要素は、 <a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">serviceinfo XML スキーマ</a>の親要素です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ServiceName" type="tns:ServiceNameType" minOccurs="0" />

<xs:simpleType name="ServiceNameType">
  <xs:restriction base="xs:string">
    <xs:minLength value="0" />
    <xs:maxLength value="200" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ServiceName 要素は現在使用されていません。

 

 





