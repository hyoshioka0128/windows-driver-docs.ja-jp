---
title: LanguageNeutralIdentifier
description: LanguageNeutralIdentifier
ms.assetid: 38713565-464c-4b12-9076-331ae43e01e8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4ea9d3ace366695c79f423281f3c98bc7ab7ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535664"
---
# <a name="languageneutralidentifier"></a>LanguageNeutralIdentifier

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LanguageNeutralIdentifier 要素には、そのロケールに依存しないサービス メタデータ パッケージを識別する GUID を指定します。 LanguageNeutralIdentifier 要素には、同じ GUID を同じサービスのサービス メタデータ パッケージの 1 つ以上のローカライズされたバージョンを識別するために使用することができます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<LanguageNeutralIdentifier>
  text
</LanguageNeutralIdentifier>
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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a>要素は、デバイスのメタデータ キャッシュ内のデバイス メタデータ パッケージを追跡するために使用されるデータを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="LanguageNeutralIdentifier" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


LanguageNeutralIdentifier 要素では、同じデバイスのデバイス メタデータ パッケージの 1 つ以上のローカライズされたバージョンで使用される同じ GUID を使用します。

たとえば、次の 3 つのロケールのデバイスを解放する場合 (EN-US など、JA-JP、AR-SA)、ロケールごとにデバイスを別のメタデータ パッケージを作成することができます。 これらのパッケージの LanguageNeutralIdentifier 要素の一般的な GUID を使用して簡単に検索できますデバイスのメタデータ パッケージの PackageInfo XML ドキュメントを参照します。

**重要な**   LanguageNeutralIdentifier 要素は、オペレーティング システムのすべてのコンポーネントでは使用されません。 OEM が使用するために予約されて独立系ハードウェア ベンダー (IHV) および独立系ソフトウェア ベンダー (ISV)。\]

 

LanguageNeutralIdentifier 要素は省略可能です。

 

 





