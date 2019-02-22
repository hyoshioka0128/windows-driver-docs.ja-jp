---
title: GDL 値マクロ
description: GDL 値マクロ
ms.assetid: 171245ef-d9ab-4c1d-86b9-f53ae10033b3
keywords:
- GDL WDK、マクロ
- マクロ WDK GDL、値マクロ
- WDK GDL マクロを値します。
- WDK GDL、マクロの値を値します。
- WDK GDL のマクロ ディレクティブ
- マクロ WDK GDL、例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db551f8988ea4714ee24e524138b61173de1c82c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529985"
---
# <a name="gdl-value-macros"></a>GDL 値マクロ


*マクロを値*値の全部または一部を表すために使用します。 定義されている、\*マクロを作成します。 1 つのコンス トラクター内で複数のマクロを定義することができます。

内の各エントリ、\*マクロ コンストラクトが別のマクロをします。 エントリのキーワード、値マクロの名前になり、エントリの値がその値のマクロの内容になります。 マクロ名は、シンボル名の種類である必要があります。 値の有効な GDL 構文に準拠した任意の値マクロの内容を指定できます。

マクロの値は、その他のマクロの値を参照できます。 インスタンス名、\*マクロ コンストラクトは、かっこで囲まれた仮引数リストが続くタグを保持できます。 マクロの定義では、仮引数への参照、\*マクロ コンストラクトがシンボル値マクロが実際に参照されているときに渡される対応するパラメーターで交換してください。

**注**  宣言と値のマクロの参照を渡すために使用される引数の参照が引数の型が値マクロであることを示すに等号 (=) でプレフィックスとして付加されます。
マクロの値に対するすべての参照では、参照がブロック マクロではなく値マクロを示すために等号 (=) もが付きます。 値、マクロ名、等号 (=) の直後に、間に空白が許可されません。 マクロの値への参照には、任意の深さのパラメーター リストが入れ子にできます。

 

### <a href="" id="macro-examples"></a> マクロの例

すべての値のマクロ定義は、完全な有効な値のエンティティとして認識する必要があります。

次のコード例では、マクロの値を使用する方法を示します。

```cpp
*Macros:
{
    InvalidMacro: "First Half of a string
}
```

二重引用符を引用符で囲まれた文字列のコンテキストを終了する必要があるために、InvalidMacro が無効です。 この終端文字なし文字列は、完全な値ではありません。

不完全な値のエンティティを表す場合は、次のコード例を使用します。

```cpp
*Macros:
{
    FirstHalf: <BeginValue:Q>"This is the first half <EndValue:Q>
    SecondHalf:  <BeginValue:Q>of the string."<EndValue:Q>
}
*FullString: =FirstHalf=SecondHalf
*%  *FullString now expands to generate the complete string:
*FullString: "This is the first half of the string."
```

次のコードでは、マクロの引数を使用する方法を示します。

```cpp
*Macros: FormalArgs(=arg1, =arg2)
{
result1: disappointed
result2: pleased
result3: impressed
result4: awestruck
result5: restrained


adverb1: very =arg1 and =arg2
   adverb2: while remaining =arg1
   String1:  The audience was =arg1 with today's performance.
}
```

次のコードでは、パラメーターを含むマクロの参照を使用する方法を示します。

```cpp
*BadOutput: =String1(=result1)
*GoodOutput: =String1(=adverb1(=adverb1(=result2, =result3), =adverb2(=result5)))
```

パーサーには、次のコードを生成するために上記のマクロの参照が展開されます。

```cpp
*BadOutput: The audience was disappointed with today's performance.
*GoodOutput: The audience was very very pleased and impressed and while remaining restrained with today's performance.
```

マクロ参照の値は、すべての値のコンテキストでは認識されません。 たとえば、マクロの値は任意の値の中で認識またはコンテキストの文字列を引用符で囲まれたされません。 ただし、マクロの値が引用符で囲まれた文字列のコンテキスト内にある 16 進文字列のコンテキスト内で認識されます。

GPD との下位互換性を提供するには、パーセント記号 (%)として解釈するパーセント記号値のマクロ定義の内容の中の非リテラルの空白値のコンテキストを使用すると、コマンド パラメーターのコンテキストが導入されています。 つまり、回避値マクロ定義内でパーセント記号を使用して、コマンド パラメーターを定義するか、パーセント記号が、リテラルの空白のコンテキスト内でなどに含まれる場合を除き、 &lt;Begin/EndValue&gt;します。

マクロが、マクロ定義の外部で参照されている場合にのみ、マクロ定義の内容が実際に解釈されます。 その時点で参照されているマクロは、その内容に置き換え、内容が実際に解釈されます。 内容にマクロの参照が含まれている場合は、その参照はその内容によって置き換えられ、解釈がそのマクロの内容に移ります。

パーサーの 1 つの入力ストリームで動作すると考える必要があります。 マクロの参照が、マクロ定義外で検出されると、マクロの参照が入力ストリームから削除され、その内容で置き換えし、入力ストリームの解析は、マクロの内容を続行します。

次のマクロを検討してください。

```cpp
*Macros:
{
quote: <BeginValue:x>"<EndValue:x>
first_half: =quote This is enclosed
second_half:  by quotes.=quote
whole_string: =first_half <not a hex string!> =second_half
}
*Print1: =quote
*Print2: =first_half
*Print3: =second_half
*Print4: =whole_string
```

上記のマクロには、次のコードが展開されます。

```cpp
*Print1:  "
*Print2:  " This is enclosed
*Print3:  by quotes."
*Print4:  " This is enclosed <not a hex string!> by quotes."
```

展開結果が構文的に法的 GDL でないことに注意してください。

 

 




