---
title: ネイティブ XML テンプレートのデータ型
description: ネイティブ XML テンプレートのデータ型
ms.assetid: a34dec46-de5d-4f12-8863-2fe6b6e5eed4
keywords:
- WDK GDL、データ型のテンプレート
- WDK GDL、プリミティブのデータ型
- ネイティブ データ型の WDK GDL
- XML_TYPE WDK GDL
- ArrayLabel ディレクティブ WDK GDL
- XMLDataType ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 719d28be12cb3adaf19fccf2a28d192689855523
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552172"
---
# <a name="native-xml-template-data-types"></a>ネイティブ XML テンプレートのデータ型


ネイティブ XML データ型が XML として定義されている\_型。

構文は、XML によって定義されます。 XML スキーマで認識される任意のデータ型を定義できます。 パーサー フィルターは現在のパーサーは何も変更せず、将来の XML データ型をサポートできるように、XML データ型に依存します。

\***DataType**:**XML\_型**テンプレートを特定の XML スキーマ定義言語の組み込みの単純データ型に関連付けます。 インスタンス データ値になります出力 XML 要素のコンテンツとして持つ**xsi:type**から派生したが、 \* **XMLDataType**このテンプレートで指定されている構造。

次のディレクティブは、XML の定義に使用\_型。

-   \*XMLDataType (必須)。 任意の XSD スキーマ組み込み単純型。 [World Wide Web Consortium (W3C)](https://go.microsoft.com/fwlink/p/?linkid=73527) XML スキーマの推奨事項は次の組み込みの単純なデータ型を認識: 文字列、normalizedString、トークン、バイト、unsignedByte、base64Binary、hexBinary、整数、positiveInteger、negativeInteger、nonNegativeInteger、nonPositiveInteger、int、unsignedInt、unsignedLong、short、unsignedShort、decimal、float、double、boolean、時間、dateTime、期間、日付、gMonth、gYear、gYearMonth、gDay、gMonthDay、名、QName、NCName、anyURI、言語、ID、IDREF、IDREFS、エンティティ、エンティティ、表記、NMTOKEN、および NMTOKENS します。 なお GDL パーサーはこれらのデータ型に限定されず、何も変更せず、将来の XML データ型を処理するために設計されています。

-   \*ArrayLabel (省略可能)。 このディレクティブを指定した場合パーサー フィルターで、値を指定した配列のラベルに続くかっこで囲む必要があります。

値の構文は、その特定のデータ型の W3C XML 標準を定義する構文に準拠する必要があります。 値 (または競合している部分のみ) で囲む必要があります XML 構文は、基本的な GDL 構文規則と競合している場合&lt;Begin/EndValue:&gt;を構築します。 複合データ型のメンバーとしてこのような互換性のない構文では、使用した XML 値または構文は、複合データ型で使用される構文と互換性がないことはできません。 開く、または終わりかっこのような文字が GDL パーサーは特殊な XML をエスケープしないことに注意してください (&lt;または&gt;) またはアンパサンド (&)。 値の作成者は、文字データの XML 構文に準拠する責任を負います。

たとえば、次のテンプレートがあるとします。

```cpp
*Template:  XML_STRING
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "string"
}
```

上記のテンプレートを使用する場合は、次の XML スキーマのエントリが作成されます。 このエントリは最初に、指定された型から派生した新しいデータ型を定義する、 \* **XMLDataType**ディレクティブが、この新しいデータ型が、スナップショットに含まれる XML 属性を追加します。 元のデータ型を使用した場合、元の定義済みの型が XML 属性を表示を許可しないため、スキーマ検証エラーが表示されるは。

```cpp
    <complexType name = "GDLW_string">
        <simpleContent>
            <extension base="string">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </simpleContent>
    </complexType>
```

次の GDL エントリを検討してください。

```cpp
*Text: Hello World
```

GDL 属性を宣言する文字列テンプレートを考えてみます\***テキスト**が、 \* **ValueType** XML で定義されている\_でテンプレートの文字列を次のコード例を示しています。

```cpp
*Template:  PHRASE
{
    *Name:  "*Text"
    *Type:  ATTRIBUTE
    *ValueType:  XML_STRING
}
```

以前 GDL エントリは、語句のテンプレートを使用して解釈されます、次の XML 出力が発生します。

```cpp
<GDL_ATTRIBUTE Name="*Text"  xsi:type="GDLW_string" >Hello World</GDL_ATTRIBUTE>
```

XML 属性**xsi:type**スキーマにこの要素の宣言が含まれていないため、この属性の要素によって保持されているデータ型を指定するために使用します。

 

 




