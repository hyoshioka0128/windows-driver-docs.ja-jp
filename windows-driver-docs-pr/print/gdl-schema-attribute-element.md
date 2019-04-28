---
title: GDL スキーマの属性要素
description: GDL スキーマの属性要素
ms.assetid: b46c0c6c-28af-4121-9182-65dc23b0ce7d
keywords:
- GDL WDK、要素
- GDL WDK、スキーマ
- WDK GDL 要素を属性します。
- GDL_ATTRIBUTE WDK GDL
- GDL_UntypedAtt WDK GDL
- 型指定されていない属性 WDK GDL
- スナップショット WDK GDL、構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff08d7b1f570dc8f52d67260c996251feeac2f71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380166"
---
# <a name="gdl-schema-attribute-element"></a>GDL スキーマの属性要素


すべてのデータ型&lt;GDL\_属性&gt;を使用して、インスタンスごとの要素が指定された**xsi:type**します。 特定のデータ型の定義は、汎用の属性要素のインスタンスを指定せずに属性 (&lt;GDL\_UntypedAtt&gt;)、次のように GDL で生成されたスキーマで定義します。

```cpp
    <complexType name="GDL_UntypedAtt"  mixed="true">
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
        <attribute name="Name" type="string" use="required"/>
        <attribute name="Personality" type="string" use="optional"/>
    </complexType>
```

この汎用的なデータ型は、属性のコンテンツがより具体的なデータ型で記述されていないときに使用されます。 汎用的なデータ型では、表示される要素のコンテンツは制限されません。 実際の要素の内容は、GDL データの種類のテンプレートによって決定されます。

&lt;GDL\_UntypedAtt&gt;に 2 つの属性があります。**名前**と**パーソナリティ**します。 **名前**は必須であり、GDL 属性のキーワードの名前を保持します。 **性格**は省略可能で、として、属性が定義されている場合は、性格タグを指定します、\*データ型。複数\_パーソナリティします。

定義のデータ型によって参照されている場合は、XSD スキーマで、値の GDL のデータ型が定義されている具体的には、 **xsi:type**属性。 XML\_型、列挙子、および XSD\_定義データ型は、XSD スキーマで新しいデータ型を作成します。

GDL 複合データ型は、汎用的なデータ型で表されます。 複合データ型のインスタンスには、他の子要素を含む可能性がある子要素または単純な XML データ型を表す文字コンテンツが含まれます。 子要素の名前がによって定義されている、  **\*ElementTags**データ型のテンプレートのディレクティブ。

定義済みのデータ型を持たないまたはテンプレートに関連付けられていないか、指定したデータ型に対して想定される構文に準拠していない GDL 属性の値がによって表される、 &lt;CDATA&gt;セクション、 &lt;GDL\_属性&gt;要素。 このセクションでは、必要に応じて値を処理するには、クライアントまたは他のパーサー フィルターができます。 このような未知のデータ型にが含まれていない、 **xsi:type**属性。 1 つ以上&lt;CDATA&gt;セクションは、値には、文字列が含まれている場合、値を表す必要があります"\]\]&gt;"。

 

 




