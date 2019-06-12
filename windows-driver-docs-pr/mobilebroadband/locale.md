---
title: ロケール
description: ロケール
ms.assetid: 1cf8d075-a1b3-4554-83d5-71fd5059c1c4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42334d8726a9139214122d3b5d5fbed867171e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558563"
---
# <a name="locale"></a>ロケール

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ロケールの要素には、サービス メタデータ パッケージのロケールを指定します。 サービス メタデータ パッケージは、1 つまたは複数のロケールを指定できます。 複数のロケールを使用するに設定する必要があります、 [MultipleLocale](multiplelocale.md)要素**true**します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Locale
  default = "xs:boolean">
  text
</Locale>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>既定</strong></p></td>
<td><p>xs:boolean</p></td>
<td><p>〇</p></td>
<td><p>True (1) または false (0) である必要があります。 かどうかの既定の属性は、このデバイス メタデータ パッケージのコンピューターの現在のロケールの既定値として、オペレーティング システムとは、true に設定します。</p></td>
</tr>
</tbody>
</table>

 

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
<xs:element name="Locale" type="tns:LocaleType" />

<xs:complexType name="LocaleType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="default" type="xs:boolean" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


-   ロケールの要素にできる *&lt;言語&gt;* - *&lt;リージョン&gt;* (EN-US) など、または *&lt;言語&gt;* (EN) など。 場合、 *&lt;言語&gt;* が設定された場合、パッケージがすべてに適用されます *&lt;言語&gt;* ロケール。 たとえば、英語は EN-US と EN BR. に適用されます。

-   コンピューターの現在のロケールの既定値としてメタデータ パッケージを指定するには、設定、**既定**属性を**true** (1)。

    **注**  サービス パッケージを 1 つだけのメタデータを設定する必要があります、**既定**属性を**true** (1)。 それ以外の場合、オペレーティング システムでは、ランダムにサービス メタデータ パッケージを選択します。

     

-   オペレーティング システムでは、表示するサービス メタデータ パッケージを選択するときは、次のように、ロケールの要素を使用します。

    1.  オペレーティング システムでは、システムが優先する言語と地域を取得します。 これは通常、Windows セットアップ中に構成します。

    2.  オペレーティング システムがサービスのパッケージを選択し、アイコンが使用されますサービス メタデータ パッケージのロケールの要素には、システムが優先する言語と地域が一致すると、および**ServiceProvider** (ServiceInfo.xml) から値をその言語と地域と一致します。

    3.  オペレーティング システムが言語中立的なアイコンに適用されます、サービス メタデータ パッケージが、推奨システムの言語に一致するロケールの要素を持たない場合、 **ServiceProvider**格納されている (ServiceInfo.xml) からの値サービス メタデータ パッケージのルート。

ロケールの要素が必要です。

 

 





