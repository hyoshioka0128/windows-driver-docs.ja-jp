---
title: LastModifiedDate
description: LastModifiedDate
ms.assetid: e0ef7ca0-0c3d-4e71-af2e-ead90013e561
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f688bf5d02d98787157e897488532211244c7f7
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323656"
---
# <a name="lastmodifieddate"></a>LastModifiedDate

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LastModifiedDate 要素は、サービスメタデータパッケージが最後に変更されたタイムスタンプを指定します。 この情報に基づいて、オペレーティングシステムは最新のサービスメタデータパッケージのバージョンを選択して読み込みます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<LastModifiedDate>
  text
</LastModifiedDate>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


タイムスタンプ値は、協定世界時 (UTC) 形式で表されます。

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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">Metadatakey</a>要素は、デバイスメタデータパッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア機能の識別子。</p></li>
<li><p>パッケージ内のテキスト文字列の言語固有のロケール。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="LastModifiedDate" type="xs:dateTime" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   LastModifiedDate 要素の値は、メタデータパッケージが最後に変更された日時を表している必要があります。

-   Windows のメタデータとインターネットサービス (WMIS) を使用して配布するためにサービスメタデータパッケージを Windows Hardware Dev Center ダッシュボードに送信するたびに、パッケージの検証後に LastModifiedDate 要素が更新されます。

LastModifiedDate 要素が必要です。

 

 





