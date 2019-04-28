---
title: 複数パーソナリティ テンプレート データ型
description: 複数パーソナリティ テンプレート データ型
ms.assetid: ee550416-9185-41fa-b113-6a1d22c3aa96
keywords:
- WDK GDL、データ型のテンプレート
- データ型、複合 WDK GDL
- MULTIPLE_PERSONALITY データ型の WDK GDL
- ElementType ディレクティブ WDK GDL
- ElementTags ディレクティブ WDK GDL
- WDK GDL 共用体
- GDL WDK、共用体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c3d34adb0c002da6fdd019ad85f9e37dd5edce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372468"
---
# <a name="multiple-personality-template-data-types"></a>複数パーソナリティ テンプレート データ型


倍数\_パーソナリティのデータ型が異なる時刻でさまざまなデータ型を保持できる値を表します。 このデータ型は、C 言語のような**共用体**データ型。

\*データ型:複数\_パーソナリティをいくつかの異なるデータ型は、C 言語と同様に属している値を受け入れることができるデータ型を定義するテンプレートを指示する**共用体**データ型。 複数\_パーソナリティのデータ型は、id を確認しようとしています (データ型) 値の値は、識別されたデータ型に属しているテンプレートで明示的に定義されたかのように、同じ XML を出力します。 つまり場合、複数\_パーソナリティのデータ型が文字列または整数またはシンボルを保持するために定義され、される整数データ型の値に整数が実際に保持されている場合、XML が出力されます。

性格タグの属性はクライアントが生成される値のデータ型の決定をできるようにも出力されます。 フィルターは、各潜在的なデータ型を使用して、値を解析することによって、値のデータ型を決定します。 入力値の最大量を正常に一致するデータ型が選択されます。 同数の場合が発生した場合、一覧の先頭に表示される要素の型が選択されます。

**注**  できますこの評価のアルゴリズムをだましてすることに注意を一覧表示する要素の型を選択すると、値の構文を構築することができます。 種類は、解析アルゴリズムで十分と区別することである必要があります。 たとえば、パーサー フィルターが任意の XML 構文を認識しないため、区別できない 2 つの XML\_データ型。 ただし、このような場合は、候補のデータ型の定義含めることができます、\*パーサーを区別するのに役立つ ArrayLabel ディレクティブ。

 

次のディレクティブは、複数の定義に使用\_パーソナリティのデータ型。

-   \*ElementType (必須)。 この値を想定している可能性があるデータ型を定義するテンプレート名の一覧。

-   \*ElementTags (必須)。 クライアントが、値を実際に割り当てられているデータ型を識別するタグの一覧。 提供されているタグの数が記載されているテンプレートの数と等しくなります\*ElementType します。 値を表す、生成された XML 要素内のパーソナリティ属性でタグが表示されます。 たとえば、データ型は、データの複数のパーソナリティの種類の配列、配列の個々 のメンバーを表す要素にはパーソナリティ属性が含まれます。 配列自体に定義済みのパーソナリティ; があるないためには、配列全体を表す要素はパーソナリティ属性を含まない。代わりに、配列の個々 のメンバーは、独自個別パーソナリティ属性の値を持ちます。

次のテンプレートを検討してください。

```cpp
*Template:  INT_OR_QUALNAME_EX
{
    *Type:  DATATYPE
    *DataType:   MULTIPLE_PERSONALITY
    *ElementType:  (INTEGER, QUALNAME_EX, QUOTEDSTRING)
    *ElementTags: (integer, QualNameEx, QuotedString)
}
```

このテンプレートは、QUALNAME、整数値を保持できるデータ型を定義します。\_EX 値、または QUOTEDSTRING 値。 どのデータ型が選択されているは、対応するユーザー定義 ElementTag で識別します。

次の GDL エントリを検討してください。

```cpp
*rcNameID:     ( RESDLL.stdname.467 )  
*rcNameID:      (0x117 )  
```

次の RC を検討してください\_名前\_ID2 テンプレート。

```cpp
*Template:  RC_NAME_ID2
{
    *Name:  "*rcNameID"
    *Type:  ATTRIBUTE
    *ValueType:  INT_OR_QUALNAME_EX
    *Additive: LEAST_TO_MOST_RECENT
}
```

GDL エントリは、上記のテンプレートで解釈される、結果の XML 出力が次のようになります。

```cpp
<GDL_ATTRIBUTE Name="*rcNameID"  Personality="QualNameEx" >
   <feature  xsi:type="GDLW_string">RESDLL</feature>
   <option  xsi:type="GDLW_string">stdname</option>
   <resourceID  xsi:type="GDLW_int">467</resourceID>
</GDL_ATTRIBUTE>
<GDL_ATTRIBUTE Name="*rcNameID"  Personality="integer" 
xsi:type="GDLW_int" >279</GDL_ATTRIBUTE>
```

唯一の違い、複数から生成される XML 出力\_パーソナリティの種類と実際の型が値の実際のデータ型のクライアントに通知に追加される追加のパーソナリティ タグ属性。

たとえば、配列の各メンバーが倍数が配列を作成できます\_パーソナリティ入力と、次のようにします。

```cpp
*Template:  DT_ARRAY_OF_MP
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  INT_OR_QUALNAME_EX
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (ArrayMember)
    *ArraySize: *
}
*Template:  ARRAY_OF_MP
{
    *Name:  "*rcNameID_List"
    *Type:  ATTRIBUTE
    *ValueType:  DT_ARRAY_OF_MP
}
```

上記のテンプレートを使用して、次のインスタンスのデータはさまざまな性格を含んでいる場合の 3 つの複数のパーソナリティ オブジェクトを含む配列を処理することができます。

```cpp
*rcNameID_List:( RESDLL.stdname.467, 0x117, "Quote" )
```

この処理では、次の XML のスナップショットを生成します。

```cpp
    <GDL_ATTRIBUTE Name="*rcNameID_List"  >
        <ArrayMember  Personality="QualNameEx">
            <feature  xsi:type="GDLW_string">RESDLL</feature>
            <option  xsi:type="GDLW_string">stdname</option>
            <resourceID  xsi:type="GDLW_int">467</resourceID>
        </ArrayMember>
        <ArrayMember  Personality="integer" xsi:type="GDLW_int">279</ArrayMember>
        <ArrayMember  Personality="QuotedString" xsi:type="GDLW_string">Quote</ArrayMember>
    </GDL_ATTRIBUTE>
```

スナップショットに示すよう、パーサーがそれぞれ 3 つの配列メンバーの適切な性格を特定し、パーソナリティ属性を適切な性格を示すために、各メンバーの要素に設定します。

 

 




