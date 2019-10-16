---
title: Test1
description: Test1
ms.assetid: 13723c21-0054-4b91-9059-c7c985e83773
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e9289ae83ed98dea4a06efa88a089581c7e108
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323601"
---
# <a name="internet"></a>Test1

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Internet 要素は、使用する購入モバイルブロードバンドプロファイルファイルを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<Internet>
  child element
</Internet>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


ServiceInformation ディレクトリ内のファイルの名前。

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
<td><p><a href="mobilebroadbandprofiles.md" data-raw-source="[MobileBroadbandProfiles](mobilebroadbandprofiles.md)">MobileBroadbandProfiles</a></p></td>
<td><p>使用する購入およびインターネットモバイルブロードバンドプロファイルファイルを指定します</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Internet" type="tns:FileType" minOccurs="0"/>

<xs:simpleType name="FileType">
  <xs:restriction base="xs:string">
    <xs:whiteSpace value="preserve"/>
    <xs:pattern value="[\p{L}\p{N}\.\-_ ]+"/>
    <xs:minLength value="1"/>
    <xs:maxLength value="260"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


インターネット要素は省略可能です。

 

 





