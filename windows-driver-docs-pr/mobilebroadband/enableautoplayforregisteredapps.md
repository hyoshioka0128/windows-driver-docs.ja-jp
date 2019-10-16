---
title: EnableAutoPlayForRegisteredApps
description: EnableAutoPlayForRegisteredApps
ms.assetid: 8f4b1a6a-262a-4ebc-808b-8e998fd78f99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fb00401b4b604928d027cdb606e1c0cfacb7f6a
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323615"
---
# <a name="enableautoplayforregisteredapps"></a>EnableAutoPlayForRegisteredApps

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

EnableAutoPlayForRegisteredApps 要素は、登録されているアプリに対して自動再生を有効にするかどうかを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<EnableAutoPlayForRegisteredApps>
  text
</EnableAutoPlayForRegisteredApps>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


"True" または "false" のいずれかのブール値。

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
<td><p><a href="windowsinfo.md" data-raw-source="[WindowsInfo](windowsinfo.md)">WindowsInfo</a></p></td>
<td><p><a href="windowsinfo-xml-schema.md" data-raw-source="[WindowsInfo XML schema](windowsinfo-xml-schema.md)">Windowsinfo XML スキーマ</a>の親要素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="EnableAutoPlayForRegisteredApps" type ="xs:boolean" default="false"/>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


この要素は、Windows 8.1 と Windows 10 にのみ適用されます。

EnableAutoPlayForRegisteredApps 要素は省略可能です。

 

 





