---
title: 購入
description: 購入
ms.assetid: e753ba12-650e-4116-bb2e-dc17fc7bddee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05263c70ac4b905fe8b4c67d2bc9ad3017ed018d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335285"
---
# <a name="purchase"></a>購入

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

購入要素では、使用する購入モバイル ブロード バンド プロファイル ファイルを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Purchase>
  child element
</Purchase>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


ServiceInformation ディレクトリ内のファイルの名前。

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
<td><p><a href="mobilebroadbandprofiles.md" data-raw-source="[MobileBroadbandProfiles](mobilebroadbandprofiles.md)">MobileBroadbandProfiles</a></p></td>
<td><p>購入および使用するインターネット モバイル ブロード バンド プロファイル ファイルを指定します</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Purchase" type="tns:FileType" minOccurs="0"/>

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


購入要素は省略可能です。

 

 





