---
title: 複合テンプレート データ型
description: 複合テンプレート データ型
ms.assetid: 5fd9218a-2827-4cca-b913-eeb6484653d9
keywords:
- WDK GDL、データ型のテンプレート
- データ型、複合 WDK GDL
- 複合データ型の WDK GDL
- ElementType ディレクティブ WDK GDL
- RequiredDelimiter ディレクティブ WDK GDL
- OptionalDelimiter ディレクティブ WDK GDL
- ElementTags ディレクティブ WDK GDL
- ArraySize ディレクティブ WDK GDL
- ArrayLabel ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24943c647dca4a7a9fd0ab7dd5f414ad7d0bb39e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353120"
---
# <a name="composite-template-data-types"></a>複合テンプレート データ型


複合データ型は、同じまたは異なるデータ型を持つ 1 つまたは複数の値で構成されます。 合成には、固定または可変 (ただし、いない無期限) の長さを持つことができます。 このデータ型は、C lLanguage 構造体のデータ型に似ています。

**\*データ型:複合**異なるデータ型のメンバーを持つができる、複合データ型を定義するテンプレートに指示します。 複合データ型のメンバーは、それを囲むコンテキストを表す要素に属する個々 の XML 子要素として出力されます。 各子要素は、データ型のプリミティブを表している場合、データ型は、XML 属性で定義されます**xsi:type**各要素にします。 GDL 属性として定義されている場合**データ型。複合**、それを囲むコンテキストになります、 &lt;GDL\_属性&gt;要素。 各 XML 子要素の要素名で定義されている、対応するタグになります**ディレクティブ。\*ElementTags**します。

複合自体が別の複合データ型のメンバーである場合はその外側のコンテキストを表す要素が作成されます。 この親要素の名前は、外側の複合データ型に対応するテンプレートによって割り当てられている、対応するタグになります。

次のディレクティブは、複合データ型の定義に使用されます。

-   **\*ElementType** (必須)。 各要素のデータ型を定義するテンプレートの名前。 1 つのデータ型は、各要素に対して指定する必要があります。 1 つまたは複数の要素には、同じデータ型を持つことができます。 提供される ElementTypes 数が、ArraySize を等しく必要がありますまたは最大値を **\*ArraySize**を指定します。

-   **\*RequiredDelimiter** (必須)。 次の構文的に各複合要素を区別する文字列。 2 つの連続する区切り記号は省略すると、要素として解釈されます。 区切り記号は、後続の要素の省略を示す必要はありません。

    区切り記号として、または区切り記号の文字列の一部として空白を使用する場合は十分に注意があります。 など、パーサーは余分な空白文字と解釈を示す省略された要素。奇妙な解析エラーが発生する余分な空白が表示されないためです。 余分な空白が定期的にソース ファイルから削除されます。 また、空白文字は多くの場合と、プリプロセッサはマクロ、コメントの処理の結果として、入力ストリームに追加します。 そのため、解析される実際の文字列には、最初に指定されたよりも、空白文字数がまったく異なる場合があります。 定期的に入力の処理中に空白文字に変換するため、タブ文字、必要な区切り記号の文字列の一部として使用しないでください。

-   **\*OptionalDelimiter** (省略可能)。 任意の文字列で指定されている文字から成る **\*OptionalDelimiter**の隣に表示される、  **\*RequiredDelimiter**文字列の一部と見なされるされます区切り記号。

-   **\*ElementTags** (必須)。 提供されているタグの数が、ArraySize を等しく必要がありますまたは最大値を **\*ArraySize**を指定します。 各メンバーに対応するタグとタグ付けされます。 このタグ付けは、1 つまたは複数の要素を省略した場合に便利です。 複合要素は省略すると、省略された要素に対応するタグは使用されません。 クライアントの混乱を避けるためには、タグの名前として、GDL スナップショットが予約されている要素の名前を使用しないでください。 これらの予約済みの名前は、構成要素、属性、およびパーソナリティは。

-   **\*ArraySize** (省略可能)。 このディレクティブを省略すると、固定サイズの合成が想定されます。 サイズのテンプレート名の数と等しくなります **\*ElementType**します。

    2 つの整数を使用すると、最小値と最大サイズを可変サイズの複合を指定します。 0 は最小サイズは許可されています。 無制限のサイズの複合データ型を指定することはできません。 GPD ワイルドカード文字を使用することはできません (\*) サイズまたは最大サイズを指定します。

-   **\*ArrayLabel** (省略可能)。 複合要素のリストはかっこで囲む必要があり、前に付けるこのディレクティブが指定されている場合、  **\*ArrayLabel**ラベル。 このディレクティブでラベルが指定されていない場合は、かっこは省略され、前に付けるラベルは許可されません。

次のテンプレートを検討してください。

```cpp
*Template:  QUALNAME_EX
{
    *Type:  DATATYPE
    *DataType:   COMPOSITE
    *ElementType: (SYMBOL, SYMBOL, INTEGER)
    *RequiredDelimiter: "."
    *ElementTags: (feature, option, resourceID)
}
```

上記のテンプレートは、固定サイズ、シンボルの 2 つのデータ型と整数の 1 つの複合を定義します。 複合は、ラベル付きではありません。 複合内の各要素には、一意の ElementTag が割り当てられます。 これらのタグは、クライアントのヘルプへの出力を XML 内の各要素にラベルを付けます。 各要素は正確に 1 つのピリオド (.); によって、次から分離します。その他の文字は、区切り記号の一部を考慮されません。 **\*ArraySize**が指定されていないため、固定の複合サイズが使用されます。 複合のサイズが固定であるために、メンバーの省略は許可されません。

**\*データ型:複合**テンプレートは、対応するスキーマを生成しません。 名前がテンプレートのスキーマ、  **\*ElementType**ディレクティブが代わりに使用されます。

たとえば、次のように定義されているシンボルのテンプレートがあるとします。

```cpp
*Template:  SYMBOL
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "SYMBOLNAME"
}
```

次の GDL エントリを検討してください。

```cpp
*rcNameID:     ( RESDLL.stdname.467 )  
```

または、省略可能なかっこがない、次の GDL エントリを検討してください。

```cpp
*rcNameID:     RESDLL.stdname.467 
```

GDL エントリが次の RC を使用して解釈されることを前提としています\_名前\_テンプレートの ID。

```cpp
*Template:  RC_NAME_ID
{
    *Name:  "*rcNameID"
    *Type:  ATTRIBUTE
    *ValueType:  QUALNAME_EX
    *Additive: LEAST_TO_MOST_RECENT
}
```

結果の XML 出力は次のようになります。

```cpp
    <GDL_ATTRIBUTE Name="*rcNameID"  >
        <feature  xsi:type="GDLW_string">RESDLL</feature>
        <option  xsi:type="GDLW_string">stdname</option>
        <resourceID  xsi:type="GDLW_int">467</resourceID>
    </GDL_ATTRIBUTE>
```

次の例では、時間間隔を表す日付データ型のペアを保持する期間のデータ型を使用して入れ子になった複合データ型を示します。 各日付データ型では、月、日、年のデータ型のコンポジットです。 INTERVAL データ型は、従業員は存在しない場合になる可能性がある期間を express に休暇 GDL 属性によって使用されます。 テンプレートの次のコレクションには、このような状況を行うとします。

### <a name="month-template"></a>1 か月のテンプレート

```cpp
*Template:  MONTHS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "months"
    *EnumeratorList: (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec)
}
```

### <a name="day-template"></a>1 日のテンプレート

```cpp
*Template:  DAY
{
*Inherits: INTEGER
*MinValue: 1
*MaxValue: 31
}
```

### <a name="year-template"></a>年のテンプレート

```cpp
*Template:  YEAR
{
*Inherits: INTEGER
*MinValue: 1900
*MaxValue: 2100
}
```

### <a name="date-template"></a>日付テンプレート

```cpp
*Template:  DATE
{
    *Type:  DATATYPE
    *DataType:   COMPOSITE
    *ElementType: (MONTHS, DAY, YEAR)
    *RequiredDelimiter: "-"
    *ElementTags: (month, day, year)
}
```

### <a name="interval-template"></a>間隔のテンプレート

```cpp
*Template:  INTERVAL
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  DATE
    *RequiredDelimiter: "to"
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (start_date, end_date)
    *ArraySize: 2
}
```

### <a name="vacation-template"></a>休暇のテンプレート

```cpp
*Template:  VACATION
{
    *Name:  "*VacationDates"
    *Type:  ATTRIBUTE
    *ValueType:  INTERVAL
}
```

次の GDL エントリを検討してください。

```cpp
*VacationDates:  Dec-20-2001 to Jan-3-2002
```

休暇テンプレートを使用して、この GDL エントリを解釈する場合、結果の XML 出力はようになります。

```cpp
    <GDL_ATTRIBUTE Name="*VacationDates"  >
        <start_date >
            <month  xsi:type="GDLW_months">Dec</month>
            <day  xsi:type="GDLW_int">20</day>
            <year  xsi:type="GDLW_int">2001</year>
        </start_date>
        <end_date >
            <month  xsi:type="GDLW_months">Jan</month>
            <day  xsi:type="GDLW_int">3</day>
            <year  xsi:type="GDLW_int">2002</year>
        </end_date>
    </GDL_ATTRIBUTE>
```

 

 




