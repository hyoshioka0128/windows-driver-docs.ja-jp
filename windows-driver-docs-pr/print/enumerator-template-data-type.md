---
title: 列挙子テンプレート データ型
description: 列挙子テンプレート データ型
ms.assetid: deb95ca1-05a5-47f4-8e2a-1d1aa1ae2261
keywords:
- WDK GDL、データ型のテンプレート
- WDK GDL、プリミティブのデータ型
- 列挙子のデータ型の WDK GDL
- ArrayLabel ディレクティブ WDK GDL
- XMLDataType ディレクティブ WDK GDL
- EnumeratorList ディレクティブ WDK GDL
- ElementTags ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 701c13ccafed48b7367b5e9d1a9e1a5c54b4abd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324267"
---
# <a name="enumerator-template-data-type"></a>列挙子テンプレート データ型


列挙子のデータ型は、トークンのセットに限定されている値を許可しました。

\*データ型:列挙子は、列挙データ型を定義するテンプレートを指示します。 このデータ型から派生した XML スキーマ単純型の宣言としての出力がなります、**文字列**を許可されている各列挙子を指定の型の制限があります。 次のディレクティブは、列挙子のデータ型を完全に定義に使用されます。

-   \*XMLDataType (必須)。 生成された XML スキーマでこの列挙体を定義するために使用する XML データ型に割り当てる NCName。 各列挙型には、一意の NCName 必要があります。 この名前は、すべての XSD に一意である必要があります\_定義と列挙子の型。 GDL パーサーを定義するデータ型の競合を回避するで始まる NCNames を避ける必要があります"GDL\_"と"GDLW\_"。

-   \*EnumeratorList (必須)。 列挙子のトークンの一覧。 各トークンが有効な GDL シンボルでなければなりません、XSD スキーマをスキーマ コンポーネントの値を適用するその他の要件に準拠している必要があります:&lt;列挙&gt;します。

-   \*ArrayLabel (省略可能)。 パーサー フィルターでこのディレクティブが指定されている場合、値を指定した配列のラベルに続くかっこで囲む必要があります。

列挙子のデータ型は、トークンのいずれかに一致する必要がありますとして解析する値を\*ElementTags ディレクティブを定義します。

次のテンプレートを検討してください。

```cpp
*Template:  COLORS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "colors"
    *EnumeratorList: (YELLOW, MAGENTA, CYAN, BLACK, RED, GREEN, BLUE)
}
```

上記のテンプレートには、次の XML スキーマのエントリを作成するパーサー フィルターが発生します。

```cpp
    <simpleType name = "colors">
        <restriction base="string">
            <enumeration value="YELLOW"/>
            <enumeration value="MAGENTA"/>
            <enumeration value="CYAN"/>
            <enumeration value="BLACK"/>
            <enumeration value="RED"/>
            <enumeration value="GREEN"/>
            <enumeration value="BLUE"/>
        </restriction>
    </simpleType>
```

パーサー フィルターでは、対応するラップされたデータ型も作成されます。

```cpp
    <complexType name = "GDLW_colors">
        <simpleContent>
            <extension base="gdl:colors">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </simpleContent>
    </complexType>
```

次の GDL エントリを検討してください。

```cpp
*Color: GREEN
```

宣言する ACOLOR テンプレートを検討してください、 **\*色**GDL 属性、  **\*ValueType**テンプレートの色で、次のコード例として定義されています。示しています。

```cpp
*Template:  ACOLOR
{
    *Name:  "*Color"
    *Type:  ATTRIBUTE
    *ValueType:  COLORS
    *Additive: LEAST_TO_MOST_RECENT
}
```

ACOLOR テンプレートを使用して、以前の GDL エントリを解釈する場合、結果の XML 出力が発生します。

```cpp
    <GDL_ATTRIBUTE Name="*Color"  xsi:type="GDLW_colors" >GREEN</GDL_ATTRIBUTE>
```

XML 属性**xsi:type** 、GDL のこのインスタンスを定義します。\_ATTRIBUTE 要素を既定の XML 名前空間で定義されている列挙体を表す値のテンプレートで定義された型を保持します。

 

 




