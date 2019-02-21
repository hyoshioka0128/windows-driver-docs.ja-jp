---
title: 動詞
description: 動詞
ms.assetid: 38edbb37-5fd4-4301-adc0-4a66a7e8a564
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 558b59fde23828ec2464ef58cf095cdd9bd40d4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557093"
---
# <a name="verb"></a>動詞

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

動詞の要素には、アプリケーションを登録する動詞を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Verb />
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

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
<xs:element name="Verb" type="tns:VerbType" />

<xs:simpleType name="VerbType">
  <xs:restriction base="tns:AllowedAsciiCharSetType">
    <xs:pattern value="[^ ]+"/>
    <xs:maxLength value="64"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


動詞の要素は省略可能です。

 

 





