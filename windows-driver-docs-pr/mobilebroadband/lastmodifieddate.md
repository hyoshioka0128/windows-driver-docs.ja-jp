---
title: LastModifiedDate
description: LastModifiedDate
ms.assetid: e0ef7ca0-0c3d-4e71-af2e-ead90013e561
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f688bf5d02d98787157e897488532211244c7f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549410"
---
# <a name="lastmodifieddate"></a>LastModifiedDate

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LastModifiedDate 要素には、サービス メタデータ パッケージを最後に変更されたタイムスタンプを指定します。 この情報に基づいて、オペレーティング システムを選択し、最新のサービス メタデータ パッケージのバージョンを読み込みます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<LastModifiedDate>
  text
</LastModifiedDate>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


タイムスタンプ値は、協定世界時 (UTC) 形式で表されます。

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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>要素は、デバイス メタデータ パッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア関数の識別子。</p></li>
<li><p>言語固有のロケールをパッケージ内のテキスト文字列。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="LastModifiedDate" type="xs:dateTime" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


-   LastModifiedDate 要素の値は、メタデータ パッケージが最後に変更された実際の時間を表す必要があります。

-   Windows メタデータとインターネット サービス (WMIS) から配布するため、Windows ハードウェア デベロッパー センター ダッシュするためにサービス メタデータ パッケージを送信するたびに、パッケージの検証後に、LastModifiedDate 要素が更新されます。

LastModifiedDate 要素が必要です。

 

 





