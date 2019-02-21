---
title: XSD のテンプレートのデータ型
description: XSD のテンプレートのデータ型
ms.assetid: 96d3a75a-fa15-47bb-8331-e3994d25c42d
keywords:
- WDK GDL、データ型のテンプレート
- WDK GDL、プリミティブのデータ型
- XSD_DEFINED データ型の WDK GDL
- ArrayLabel ディレクティブ WDK GDL
- XMLDataType ディレクティブ WDK GDL
- XSDTypeDefinition ディレクティブ WDK GDL
- ComplexType ディレクティブ WDK GDL
- WDK GDL、特殊な XML 文字のエスケープ パーサー
- WDK GDL を特別な XML をエスケープ文字します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be818179c0e27790b0b453a256355400933ae891
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549471"
---
# <a name="xsd-template-data-types"></a>XSD のテンプレートのデータ型


XSD\_定義データ型は、データ型の定義のスキーマを使用します。 任意の複合型または単純型を定義できます。

\*データ型:XSD\_定義は、標準を使用してデータ型の定義を作成します&lt;xsd:complexType&gt;または&lt;xsd:simpleType&gt; XML 要素。 インスタンス データ値が持つ xsi:type がの値で指定された XML 要素のコンテンツとして出力をされます\*XMLDataType このテンプレートに表示されます。 この出力では、XSD を使用して新しい単純または複雑な型を派生し、GDL 属性で使用することができます。

次のディレクティブを使用して、XSD を完全に定義\_定義データ型。

-   \*XMLDataType (必須)。 このテンプレートを定義する XSD データ型に割り当てられている名前 (NCName)。 この名前の値である、**名前**属性、 &lt;complexType&gt;または&lt;simpleType&gt;要素を\*XSDTypeDefinition ディレクティブを定義します。 この名前は、すべての XSD に一意である必要があります\_定義と列挙子の型。 GDL パーサーを定義するデータ型の競合を回避するには、名前が始まるを避ける必要があります"GDL\_"と"GDLW\_"。 XML 標準な NCName の構文を定義し、追加の制限を課すことがあります。

-   \*XSDTypeDefinition (必須)。 適切な形式で XSD データ型を定義します。 のみ、 &lt;complexType&gt;または&lt;simpleType&gt;要素がルートに最も近いコンテキストで記述できます。 複数&lt;complexType&gt;または&lt;simpleType&gt;うち 1 つだけでは実際に GDL 属性の値の型として参照されている場合、要素がコンテキストでは、ルートほとんどの兄弟として表示できます。 GDL 属性の値の型が含まれているものとして参照される型の名前、 \*XMLDataType ディレクティブ。 その他の内から残りのデータ型が参照のみできます&lt;complexType&gt;または&lt;simpleType&gt;定義します。

    型定義には、その他のテンプレートで定義されている他の型定義を参照できます。 内の型定義を参照するとき、 \*XSDTypeDefinition ディレクティブを使用して作成された、 \*XSDTypeDefinition ディレクティブを使用する必要あります、gdl: 名前空間プレフィックス。

    XSD は、複数の行を占有または GDL 構文規則に違反している場合で囲む必要があります&lt;Begin/EndValue&gt;区切り記号。 この区切り記号で定義されている XSD は、GDL パーサーによって生成される XSD スキーマに挿入されます。 なお、 &lt;complexType&gt; GDL 属性の値型は、任意の XML 属性を宣言できませんとして参照される定義。 GDL パーサーを生成するスキーマの XSD 名前空間は、既定の名前空間要素の名前など、 &lt;complexType&gt;または&lt;シーケンス&gt;または&lt;要素&gt;必要はありません、名前空間の修飾子です。 ターゲットの名前空間は、gdl を関連付け: プレフィックス。

-   \*ComplexType でしょうか。 (**TRUE** | **FALSE**) (省略可能)。 このディレクティブがある場合**TRUE**、GDL パーサーは、この定義を参照&lt;complexContent&gt; ; このデータ型を拡張すると、それ以外の場合、定義として参照されます&lt;simpleContent&gt;. このディレクティブが指定されていない場合、パーサーと見なします**FALSE**します。

-   \*ArrayLabel (省略可能)。 このディレクティブが指定されている場合、パーサーのフィルターには、指定した配列のラベルに続くかっこで囲むには、この型のインスタンスの値が期待しています。

このデータ型に宣言されている値のインスタンスの構文は、XSD で定義されている構文に従う必要があります\*XSDTypeDefinition ディレクティブを提供します。 パーサーは先頭を指定し、終了、要素のタグと値のインスタンスのデータ要素の内容のみを指定する必要があります。 値 (または競合している部分のみ) で囲む必要があります XML 構文は、基本的な GDL 構文規則と競合している場合&lt;Begin/EndValue:&gt;を構築します。

複合データ型のメンバーとしてこのような互換性のない構文では、使用した XML 値または構文が複合データ型を使用する、構文と互換性がないことはできません。 開く、または終わりかっこのような文字が GDL パーサーは特殊な XML をエスケープしないことに注意してください (&lt;または&gt;) またはアンパサンド (&)。 値のインスタンスの作成者は、文字データの XML 構文に準拠する責任を負います。

たとえば、次のテンプレートがあるとします。

```cpp
*Template:  USAddress
{
    *Type:  DATATYPE
    *DataType:   XSD_DEFINED
    *ComplexType?: TRUE
    *XMLDataType: "USAddress"
    *XSDTypeDefinition:<BeginValue:XSD>
    <complexType name="USAddress">
        <sequence>
            <element name="name"   type="string"/>
            <element name="street" type="string"/>
            <element name="city"   type="string"/>
            <element name="state"  type="string"/>
            <element name="zip"    type="gdl:zipCode"/>
        </sequence>
    </complexType>

<simpleType name="zipCode">
 <restriction base="integer">
  <minInclusive value="10000"/>
  <maxInclusive value="99999"/>
 </restriction>
</simpleType><EndValue:XSD>
}
```

前の例では、XSD 定義の型の ValueType として GDL 属性によって参照されていることができます"USAddress"という名前を定義します。 実際には、この XSD の例には、2 つのデータ型が定義します。**USAddress**と**zipCode**します。 **ZipCode**型 GDL 属性で参照することはできませんし、別の XSD データ型の定義内からのみ参照できます。

次の例では、 **zipCode**の宣言で型が参照されている、 &lt;zip&gt;要素。 Gdl を使用して、参照されていることに注意してください。 名前空間プレフィックス。 **zipCode**別のテンプレートでの XSD データ型の定義から参照することもできます。

上記のテンプレートの定義と、次の XML スキーマ エントリの作成 (の値は\*XSDTypeDefinition 変更なし)。

```cpp
    <complexType name="USAddress">
        <sequence>
            <element name="name"   type="string"/>
            <element name="street" type="string"/>
            <element name="city"   type="string"/>
            <element name="state"  type="string"/>
            <element name="zip"    type="gdl:zipCode"/>
        </sequence>
    </complexType>

    <simpleType name="zipCode">
        <restriction base="integer">
            <minInclusive value="10000"/>
            <maxInclusive value="99999"/>
        </restriction>
    </simpleType>
```

パーサーから派生した新しい型を定義する別のデータ型を自動的に構築します、 **USAddress**型、それがスナップショットに表示される XML 属性を追加します。 元のデータ型を使用する場合に表示される任意の XML 属性の元の型は許可されませんでした、スキーマ検証エラーが表示されるは。 この方法により、ライタがありませんが、テンプレートにハード コード パーサー合成 XML 属性に、既存のテンプレートを変更する必要はありません、追加の属性を追加する、スナップショットの将来のバージョンの場合。

次のコード例では、追加のデータ型の定義を示します。

```cpp
    <complexType name = "GDLW_USAddress">
        <complexContent>
            <extension base="gdl:USAddress">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </complexContent>
    </complexType>
```

**注**   、 **GDLW\_USAddress**としてデータ型が宣言されている&lt;complexContent&gt;ためのテンプレートを**USAddress**設定\*ComplexType:**TRUE**します。

 

次の GDL エントリを検討してください。

```cpp
*Address: <BeginValue:XML> 
   <name>Alice Smith</name>
   <street>123 Maple Street</street>
   <city>Mill Valley</city>
   <state>CA</state>
   <zip>90952</zip>
<EndValue:XML>
```

宣言するアドレス テンプレートを検討してください、\*がアドレス GDL aAttribute、\*テンプレートで定義されている ValueType **USAddress**次のコード例に示すように、します。

```cpp
*Template:  ADDRESS
{
    *Name: "*Address"
    *Type:  ATTRIBUTE
    *ValueType:  USAddress
}
```

アドレスのテンプレートを使用して、以前の GDL エントリを解釈する場合、結果の XML 出力が発生します。

```cpp
    <GDL_ATTRIBUTE Name="*Address"  xsi:type="GDLW_USAddress" >
    <name>Ben Smith</name>
    <street>123 Maple Street</street>
    <city>Mill Valley</city>
    <state>CA</state>
    <zip>90952</zip>
    </GDL_ATTRIBUTE>
```

という名前の XSD 定義データ型を保持する属性の要素のこのインスタンスを定義する XML 属性の xsi:type **GDLW\_USAddress**します。 要素コンテンツとして GDL 属性のインスタンスの値全体が挿入される、 &lt;GDL\_属性&gt;変更しなくても XML スナップショット内の要素。 したがって、値は有効な XML である必要があります、特殊文字の表現のように、すべての XML 構文規則に従う必要があります。

 

 




