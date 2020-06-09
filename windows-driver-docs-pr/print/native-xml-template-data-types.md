---
title: ネイティブ XML テンプレート データ型
description: ネイティブ XML テンプレート データ型
ms.assetid: a34dec46-de5d-4f12-8863-2fe6b6e5eed4
keywords:
- テンプレート WDK GDL, データ型
- データ型 WDK GDL、プリミティブ
- ネイティブデータ型 WDK GDL
- XML_TYPE WDK GDL
- ArrayLabel ディレクティブ WDK GDL
- XMLDataType ディレクティブ WDK GDL
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8724ec1b6ce9e7f50657fd35141e35a0504011ab
ms.sourcegitcommit: d71024c0c782b5c013192d960700802eafc120f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507099"
---
# <a name="native-xml-template-data-types"></a>ネイティブ XML テンプレート データ型

ネイティブ XML データ型は、XML 型として定義されて \_ います。

構文は XML によって定義されます。 XML スキーマによって認識される任意のデータ型を定義できます。 パーサーフィルターは XML データ型に依存しないため、現在のパーサーは将来の XML データ型を変更せずにサポートできます。

\***DataType**: **xml \_ 型**により、特定の xml スキーマ定義言語の組み込みの単純データ型にテンプレートが関連付けられます。 インスタンスデータ値は、 **xsi:type** \* このテンプレートによって指定された**xmldatatype**コンストラクトから派生した XSI: type を持つ XML 要素のコンテンツとして出力されます。

XML 型のデータ型を定義するには、次のディレクティブを使用し \_ ます。

- \*XMLDataType (必須)。 任意の XSD スキーマ組み込みの単純型。 XML スキーマの[World Wide Web コンソーシアム (W3C)](https://www.w3.org/XML/Schema#dev)勧告では、String、normalizedString、token、Byte、unsignedByte、Base64Binary、hexBinary、Integer、PositiveInteger、NegativeInteger、NonNegativeInteger、nonPositiveInteger、int の各組み込みの単純データ型が認識されます。 unsignedInt、Long、unsignedbyte、Short、Unsignedbyte、decimal、float、double、boolean、Time、dateTime、duration、date、Gmonth、Gmonth、GYearMonth、gmonth、Gmonth Day、Name、QName、NCName、anyURI、LANGUAGE、ID、IDREF、IDREFS、ENTITY、ENTITIES、NOTATION、NMTOKEN、および NMTOKENS。 GDL パーサーは、これらのデータ型に限定されておらず、将来の XML データ型を変更せずに処理するように設計されていることに注意してください。

- \*ArrayLabel (省略可能)。 このディレクティブを指定した場合、パーサーフィルターでは、指定された配列ラベルを前に付けた値がかっこで囲まれている必要があります。

値の構文は、W3C XML 標準で定義されている特定のデータ型に対して定義されている構文に従う必要があります。 XML 構文が基本的な GDL 構文規則と競合する場合、値 (または競合する部分のみ) を <Begin/EndValue: > コンストラクト内で囲む必要があります。 このような互換性のない構文を持つ XML 値、または、複合データ型によって使用される構文と互換性のない構文を持つ XML 値は、複合データ型のメンバーとして表示できません。 また、GDL パーサーは、開始角かっこ (< または >) やアンパサンド (&) などの特殊な XML 文字をエスケープしません。 値の作成者は、文字データの XML 構文に準拠する役割を担います。

たとえば、次のテンプレートについて考えてみます。

```console
*Template:  XML_STRING
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "string"
}
```

上記のテンプレートを使用すると、次の XML スキーマエントリが作成されます。 このエントリは、最初に xmldatatype ディレクティブによって指定された型から派生する新しいデータ型を定義し \* **XMLDataType**ますが、この新しいデータ型には、スナップショットに表示できる追加の XML 属性が含まれています。 元のデータ型を使用した場合、スキーマ検証エラーが発生します。これは、元の定義済みの型では XML 属性を表示できないためです。

```xml
    <complexType name = "GDLW_string">
        <simpleContent>
            <extension base="string">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </simpleContent>
    </complexType>
```

次の GDL エントリを考えてみましょう。

```console
*Text: Hello World
```

\* **Text** \* **ValueType** \_ 次のコード例に示すように、XML 文字列テンプレートによって定義された ValueType を持つように GDL 属性テキストを宣言する語句テンプレートについて考えてみます。

```console
*Template:  PHRASE
{
    *Name:  "*Text"
    *Type:  ATTRIBUTE
    *ValueType:  XML_STRING
}
```

前の GDL エントリが語句テンプレートを使用して解釈された場合、次の XML 出力が発生します。

```xml
<GDL_ATTRIBUTE Name="*Text"  xsi:type="GDLW_string" >Hello World</GDL_ATTRIBUTE>
```

XML 属性**xsi: type**は、この属性要素によって保持されるデータ型を指定するために使用されます。これは、スキーマにこの要素の宣言が含まれていないためです。
