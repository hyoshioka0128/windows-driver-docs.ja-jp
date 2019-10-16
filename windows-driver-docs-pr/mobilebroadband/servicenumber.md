---
title: ServiceNumber
description: ServiceNumber
ms.assetid: 7e02557a-34e5-41f2-9a27-122a144c2ab9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc89b599bf9bc0cd4a70d1945e6178f14011e399
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323685"
---
# <a name="servicenumber"></a>ServiceNumber

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceNumber 要素は、携帯電話会社を表す一意の自己生成 GUID を指定します。 この GUID は存在する必要があり、アカウントプロビジョニングメタデータが PC に適用されると、そのファイルで識別されている通信事業者 ID で宣言された GUID 値と一致することが確認されます。 アカウントプロビジョニングメタデータは、モバイルブロードバンドアプリまたはオペレータ web サイトによって生成されます。 アカウントプロビジョニングのメタデータについては、「[アカウントのプロビジョニング](account-provisioning.md)」を参照してください。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ServiceNumber>
  text
</ServiceNumber>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


[Guidtype](guidtype-serviceinfo.md)の文字列。

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
<xs:element name="ServiceNumber" type ="tns:ServiceNumberType" />

<xs:simpleType name="ServiceNumberType">
  <xs:union memberTypes="tns:GUIDType xs:string" />
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ServiceNumber 要素が必要です。

 

 





