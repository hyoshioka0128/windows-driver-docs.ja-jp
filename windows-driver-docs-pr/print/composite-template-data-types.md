---
title: 複合テンプレート データ型
description: 複合テンプレート データ型
ms.assetid: 5fd9218a-2827-4cca-b913-eeb6484653d9
keywords:
- テンプレート WDK GDL, データ型
- データ型 WDK GDL、複合
- 複合データ型 WDK GDL
- ElementType ディレクティブ WDK GDL
- RequiredDelimiter ディレクティブ WDK GDL
- 任意の区切り記号ディレクティブ WDK GDL
- ElementTags ディレクティブ WDK GDL
- ArraySize ディレクティブ WDK GDL
- ArrayLabel ディレクティブ WDK GDL
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 12e7e1054c29bb407b2e9ddd50950d5d17f8477f
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638442"
---
# <a name="composite-template-data-types"></a>複合テンプレート データ型

複合データ型は、同じデータ型または異なるデータ型を持つ1つ以上の値で構成されます。 複合は固定または変数 (無期限) の長さを持つことができます。 このデータ型は、C lLanguage structure データ型に似ています。

** \* DATATYPE: 複合**データ型を定義する複合データ型を定義するようにテンプレートに指示します。 複合データ型のメンバーは、外側のコンテキストを表す要素に属する個々の XML 子要素として出力されます。 各子要素がデータ型のプリミティブを表す場合は、各要素の XML 属性**xsi: type**によってデータ型が定義されます。 GDL 属性が**DataType: 複合**として定義されている場合、外側のコンテキストは &lt; gdl \_ 属性要素になり &gt; ます。 各 XML 子要素の要素名は、**ディレクティブ: \* elementtags**で定義されている対応するタグになります。

複合がそれ自体が別の複合データ型のメンバーである場合は、その外側のコンテキストを表す要素が作成されます。 この親要素の名前は、それを囲む複合データ型に対応するテンプレートによって割り当てられる、対応するタグになります。

複合データ型を定義するには、次のディレクティブを使用します。

- ** \* ElementType** (必須)。 各要素のデータ型を定義するテンプレートの名前。 要素ごとに1つのデータ型を指定する必要があります。 1つ以上の要素のデータ型を同じにすることができます。 指定される ElementTypes の数は、arraysize によっ** \* て指定さ**れる Arraysize または Max の値と同じである必要があります。

- ** \* Requireddelimiter** (必須)。 次の各複合要素を構文的に区切る文字列。 2つの連続する区切り記号は、省略された要素として解釈されます。 末尾の要素が省略されていることを示すために区切り記号は必要ありません。

    区切り記号として空白文字を使用する場合、または区切り記号文字列の一部として使用する場合は、十分に注意してください。 たとえば、パーサーは、省略された要素を示すように余分な空白文字を解釈します。また、余分な空白が表示されない場合があるため、予期しない解析エラーが発生する可能性があります。 また、余分な空白はソースファイルから定期的に削除され、多くの場合、プリプロセッサ、マクロ、およびコメント処理の結果として入力ストリームに追加されます。 したがって、実際に解析される文字列には、最初に指定したものとはまったく異なる数の空白文字が含まれる場合があります。 タブ文字は、入力処理中にスペース文字に定期的に変換されるため、必要な区切り記号文字列の一部として使用しないでください。

- オプションの** \* 区切り記号**(省略可能)。 必須の区切り記号の文字列の隣にある、任意の** \* 区切り記号**で指定された文字で構成される文字列は、区切り記号の一部と見なされます。 ** \* **

- ** \* Elementtags** (必須)。 指定するタグの数は、arraysize によっ** \* て指定さ**れた Arraysize または Max の値と同じである必要があります。 各メンバーには、対応するタグがタグ付けされます。 このタグ付けは、1つ以上の要素が省略されている場合に便利です。 複合要素を省略した場合、省略された要素に対応するタグは使用されません。 クライアントの混乱を避けるために、GDL スナップショットの予約済み要素名をタグ名として使用しないでください。 これらの予約名は、構成要素、属性、およびパーソナリティです。

- ** \* Arraysize** (省略可能)。 このディレクティブを省略した場合は、固定サイズの複合が想定されます。 サイズは、 ** \* ElementType**のテンプレート名の数と同じになります。

    2つの整数を使用して、可変サイズの複合の最小値と最大許容サイズを指定します。 最小サイズには0が許可されていることに注意してください。 無制限のサイズの複合データ型は許可されません。 GPD ワイルドカード文字 () を使用して \* サイズまたは最大サイズを指定することはできません。

- ** \* Arraylabel** (省略可能)。 このディレクティブを指定する場合は、複合要素のリストをかっこで囲み、 ** \* arraylabel**ラベルの前に付ける必要があります。 このディレクティブでラベルが指定されていない場合、かっこは省略可能であり、前にラベルを付けることはできません。

次のテンプレートについて考えてみましょう。

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

上記のテンプレートは、2つのシンボルデータ型と1つの整数を持つ固定サイズの複合型を定義します。 複合はラベル付けされていません。 複合内の各要素には、一意の ElementTag が割り当てられます。 これらのタグは、クライアントを支援するために XML 出力の各要素にラベルを付けます。 各要素は、次に1つのピリオド (.) で区切られます。その他の文字は、区切り記号の一部と見なされません。 ** \* Arraysize**が指定されていないため、固定の複合サイズが想定されます。 複合サイズは固定されているため、メンバーを省略することはできません。

** \* DATATYPE: 複合**テンプレートは対応するスキーマを生成しません。 ** \* ElementType**ディレクティブで指定されているテンプレートのスキーマが代わりに使用されます。

たとえば、次のように定義されているシンボルテンプレートについて考えてみます。

```cpp
*Template:  SYMBOL
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "SYMBOLNAME"
}
```

次の GDL エントリについて考えてみましょう。

```cpp
*rcNameID:     ( RESDLL.stdname.467 )  
```

または、省略可能なかっこを含まない次の GDL エントリについて考えてみます。

```cpp
*rcNameID:     RESDLL.stdname.467
```

GDL エントリが次の RC NAME ID テンプレートを使用して解釈されるとし \_ \_ ます。

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

次の例では、時間間隔を表す日付データ型のペアを保持する INTERVAL データ型を使用して、入れ子になった複合データ型を示します。 各日付データ型は、月、日、および年のデータ型の複合型です。 INTERVAL データ型は、従業員が存在しない可能性のある期間を表すために、休暇の GDL 属性によって使用されます。 次のテンプレートのコレクションによって、この状況が実現されます。

## <a name="month-template"></a>月テンプレート

```cpp
*Template:  MONTHS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "months"
    *EnumeratorList: (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec)
}
```

## <a name="day-template"></a>日テンプレート

```cpp
*Template:  DAY
{
*Inherits: INTEGER
*MinValue: 1
*MaxValue: 31
}
```

## <a name="year-template"></a>年テンプレート

```cpp
*Template:  YEAR
{
*Inherits: INTEGER
*MinValue: 1900
*MaxValue: 2100
}
```

## <a name="date-template"></a>日付テンプレート

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

## <a name="interval-template"></a>間隔テンプレート

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

## <a name="vacation-template"></a>休暇テンプレート

```cpp
*Template:  VACATION
{
    *Name:  "*VacationDates"
    *Type:  ATTRIBUTE
    *ValueType:  INTERVAL
}
```

次の GDL エントリを考えてみましょう。

```cpp
*VacationDates:  Dec-20-2001 to Jan-3-2002
```

この GDL エントリが休暇テンプレートを使用して解釈される場合、結果の XML 出力は次のようになります。

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
