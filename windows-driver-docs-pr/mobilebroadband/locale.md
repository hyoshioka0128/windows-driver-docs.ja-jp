---
title: Locale
description: Locale
ms.assetid: 1cf8d075-a1b3-4554-83d5-71fd5059c1c4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42334d8726a9139214122d3b5d5fbed867171e2
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323629"
---
# <a name="locale"></a>Locale

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Locale 要素は、サービスメタデータパッケージのロケールを指定します。 サービスメタデータパッケージは、1つまたは複数のロケールを指定できます。 複数のロケールを使用するには、複数の[ロケール](multiplelocale.md)要素を**true**に設定する必要があります。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<Locale
  default = "xs:boolean">
  text
</Locale>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>タスクバーの検索ボックスに</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>既定</strong></p></td>
<td><p>xs:boolean</p></td>
<td><p>[はい]</p></td>
<td><p>True (1) または false (0) にする必要があります。 Default 属性が true に設定されている場合、オペレーティングシステムは、このデバイスメタデータパッケージをコンピューターの現在のロケールの既定値として使用します。</p></td>
</tr>
</tbody>
</table>

 

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
<xs:element name="Locale" type="tns:LocaleType" />

<xs:complexType name="LocaleType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="default" type="xs:boolean" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   Locale 要素には *&lt;Language @ no__t-2*- *&lt;region @ no__t-6* (en-us など) または *&lt;LANGUAGE @ no__t* (en など) を指定できます。 *@No__t-1Language @ no__t*が設定されている場合、パッケージはすべて *&lt;language @ no__t-5*ロケールに適用されます。 たとえば、en は EN-US と EN に適用されます。

-   コンピューターの現在のロケールの既定値としてメタデータパッケージを指定するには、 **default**属性を**true** (1) に設定します。

    **注**   サービスに対して1つのメタデータパッケージのみが**既定**の属性を**true** (1) に設定する必要があります。 それ以外の場合、オペレーティングシステムはサービスのメタデータパッケージをランダムに選択します。

     

-   オペレーティングシステムは、表示するサービスメタデータパッケージを選択すると、次のように Locale 要素を使用します。

    1.  オペレーティングシステムは、システムの優先言語と地域を取得します。 通常、これは Windows セットアップ中に構成されます。

    2.  サービスメタデータパッケージの Locale 要素がシステムの優先言語と地域に一致する場合、オペレーティングシステムはサービスのパッケージを選択し、その言語に対応する icon と**ServiceProvider**の値 (serviceinfo .xml) を使用します。およびリージョン。

    3.  サービスメタデータパッケージに、システムの優先言語と一致する Locale 要素がない場合、オペレーティングシステムは、のルートに格納されている言語に依存しないアイコンと**ServiceProvider**の値 (serviceinfo .xml) を適用します。サービスメタデータパッケージ。

Locale 要素が必要です。

 

 





