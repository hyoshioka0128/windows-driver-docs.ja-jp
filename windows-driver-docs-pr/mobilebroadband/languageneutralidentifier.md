---
title: LanguageNeutralIdentifier
description: LanguageNeutralIdentifier
ms.assetid: 38713565-464c-4b12-9076-331ae43e01e8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4ea9d3ace366695c79f423281f3c98bc7ab7ba
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323657"
---
# <a name="languageneutralidentifier"></a>LanguageNeutralIdentifier

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LanguageNeutralIdentifier 要素は、ロケールに依存しないサービスメタデータパッケージを識別する GUID を指定します。 LanguageNeutralIdentifier 要素を使用すると、同じサービスのサービスメタデータパッケージの1つ以上のローカライズされたバージョンを識別するために同じ GUID を使用できます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<LanguageNeutralIdentifier>
  text
</LanguageNeutralIdentifier>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a>要素は、デバイスメタデータキャッシュ内のデバイスメタデータパッケージを追跡するために使用されるデータを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="LanguageNeutralIdentifier" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


LanguageNeutralIdentifier 要素を使用すると、同じデバイスのデバイスメタデータパッケージの1つまたは複数のローカライズされたバージョンで同じ GUID を使用できます。

たとえば、3つのロケール (EN-US、JA-JP、AR など) のデバイスをリリースする場合は、ロケールごとにデバイス用に個別のメタデータパッケージを作成できます。 これらのパッケージの LanguageNeutralIdentifier 要素に共通の GUID を使用することにより、PackageInfo XML ドキュメントを参照して、デバイスのメタデータパッケージを簡単に検索できます。

**重要**   LanguageNeutralIdentifier 要素は、オペレーティングシステムのどのコンポーネントでも使用されません。 OEM、独立系ハードウェアベンダー (IHV)、および独立系ソフトウェアベンダー (ISV) が使用するために予約されています。\]

 

LanguageNeutralIdentifier 要素は省略可能です。

 

 





