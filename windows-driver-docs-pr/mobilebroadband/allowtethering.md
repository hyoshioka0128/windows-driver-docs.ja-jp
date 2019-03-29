---
title: AllowTethering
description: AllowTethering
ms.assetid: f9b92c46-5e0e-447a-b571-bf549e9a749d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d65981a1967012b5fe091da6d6da90cadd90f3ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572840"
---
# <a name="allowtethering"></a>AllowTethering

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

AllowTethering 要素には、かどうか、ユーザーが常に許可されている、ことはありません許可、またはインターネット共有を使用する権利チェック後に許可されているを指定します。

**注**  場合、この要素は、権利チェック後を許可する構成を指定してください、 [DeviceNotificationHandler](devicenotificationhandler.md)権利チェックを処理するアプリでします。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<AllowTethering>
  text
</AllowTethering>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


かどうかインターネットの共有が常に許可、許可されない、または、権利チェック後に許可されていることを示す文字列。

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
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a></p></td>
<td><p>購入して、インターネットを指定するためのモバイル ブロード バンド プロファイルまたは標準ユーザーが暗証番号 (pin) を実行するかどうかの操作のロックを解除します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="name="AllowTethering" type="tns:TetheringAllowedType" minOccurs="0" />

<xs:simpleType name="TetheringAllowedType">  
  <xs:restriction base="xs:string">
    <xs:enumeration value="Never"/>
    <xs:enumeration value="Always"/>
    <xs:enumeration value="EntitlementCheckRequired"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


この要素では、Windows 8.1 および Windows 10 に適用のみです。

AllowTethering 要素は省略可能です。

 

 





