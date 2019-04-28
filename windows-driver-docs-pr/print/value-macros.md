---
title: 値マクロ
description: 値マクロ
ms.assetid: 265b2d35-5e91-4c47-a145-1e9f8c497c2c
keywords:
- 値マクロ WDK GPD ファイル
- マクロを参照します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9911ddbd5c1638367dc204bcf03eaa1ec0ad3fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380526"
---
# <a name="value-macros"></a>値マクロ





値のマクロを使用して、個別に挿入する 1 つまたは複数の値の and GPD ファイルに繰り返しを指定します。 値には、いずれかを指定できます、 [GPD 値型](gpd-value-types.md)します。

次の規則は、値のマクロの使用に適用されます。

-   GPD ファイル内で値マクロの定義への参照を任意の前にある必要があります。

-   ルート レベルで定義されている値マクロ (つまり、中かっこ内ではなく) を定義している、定義後 GPD ファイルを通じて利用できます。 それ以外の場合、値のマクロのスコープは、その定義を含む左と右かっこのセットです。

-   値マクロは、のいずれかに解決する必要があります、 [GPD 値型](gpd-value-types.md)します。

-   値マクロの定義は、すべての値は、テキスト文字列が値マクロは、それ自体を参照できない場合、その他の値を以前に定義されたマクロを参照できます。

-   マクロの値には、引数は受け入れません。

-   同じ名前の 2 つのマクロの値を作成する場合、最初の定義が有効で GPD パーサーが 2 番目の定義を検出するまで。 2 番目の定義には、最初が置き換えられます。 2 番目の定義のスコープが終了した場合は、最初の定義が再開されます。

### <a name="value-macro-format"></a>マクロの値の形式

GPD ファイル内の 1 つまたは複数の値のマクロを定義するには、次の形式を使用します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* マクロ:<em>ValueMacroGroupName</em> { <em>ValueMacroBody</em> }</p></td>
</tr>
</tbody>
</table>

 

場所*ValueMacroGroupName*一意の名前を指定すると*ValueMacroBody*一意の値の名前と関連付けられている値のセットを次に示します。

*ValueMacroName* :*MacroValue*

場所*ValueMacroName*マクロの一意の名前を指定し、 *MacroValue*を表します、 [GPD 値型](gpd-value-types.md)。 (*MacroValue*解決済みの文字列が GPD 値の型を表す場合に限り、以前に定義された値のマクロへの参照を含めることができます)。

たとえば、次のように、一連のプレフィックスを頻繁に使用されるコマンド用のマクロの値を定義可能性があります。

```cpp
*Macros: HP4L
{
    LetterCmdPrefix: "<1B>&l2a8c1E<1B>*p0x0Y"
    A4CmdPrefix: "<1B>&l26a8c1E<1B>*p0x0Y"
    Env10CmdPrefix: "<1B>&l81a8c1E<1B>*p0x0Y"
}
```

なお*ValueMacroGroupName* (この例では HP4L) は省略可能で、処理され、コメントとして。

### <a name="referencing-value-macros"></a>参照元の値マクロ

値マクロを参照するには、次の形式を使用します。

= *ValueMacroName*

場所*ValueMacroName*に指定されている、一意の名前、\*マクロ エントリ マクロを定義します。

たとえば、コマンド仕様の中で HP4L マクロのいずれかの参照には、次のエントリを使用できます。

```cpp
*Command: CmdSelect
{
    *Cmd: =LetterCmdPrefix "<1B>*c0t5760x7680Y"
}
```

Nonmacro 値とマクロの参照を組み合わせることによって値を代入するは、すべてのマクロ定義とその他の値の例に示すようにテキストまたはコマンドの部分文字列を表している場合だけです。 その他のすべてのケースでマクロ参照に割り当てられる値全体を表す必要があります。

 

 




