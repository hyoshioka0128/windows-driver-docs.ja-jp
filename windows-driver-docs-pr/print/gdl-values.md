---
title: GDL 値
description: GDL 値
ms.assetid: 0e634646-d334-4b9c-b9d2-36026f617575
keywords:
- GDL WDK、値
- 値 WDK GDL、GDL 値について
- WDK GDL、文字の値
- GDL WDK、コンテキスト
- GDL WDK、マクロの値の参照
- マクロの値は、WDK GDL を参照します。
- WDK GDL、例の値
- WDK GDL のコンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9f785d9bffeba2ec6746b39d9de9f60626bdc38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560106"
---
# <a name="gdl-values"></a>GDL 値


A *GDL 値*コロン区切り記号の後が検出され、通常終了時 linebreak シーケンス GDL 属性の最初の空白以外の文字で始まる文字の文字列またはコンストラクトの区切り記号に到達します。

いくつかあります[GDL コンテキスト](gdl-contexts.md)とき linebreak シーケンスまたはコンストラクトの区切り記号は終了しません値。 これらの特殊なコンテキストを含める場合。

-   構成要素の区切り記号の文字は、コメントの一部として発生します。

-   終了文字が引用符で囲まれた文字列の一部として発生します。

-   内で発生する終了文字を[入れ子になったコンテキスト](gdl-nested-contexts.md)します。

-   終了文字が内で発生する[任意の値](gdl-arbitrary-value-contexts.md)します。

値は 0、1、またはこれらの特殊なコンテキストの詳細を含めることができます。 1 つのコンテキストの型は、1 つの値に複数回を表示できます。 前の特別なコンテキストのいずれかのことができます、他の任意のコンテキスト外でも表示されます。 一部のコンテキストが別のコンテキスト内で表示されます。このような場合は、各コンテキストの説明に記載されています。 Linebreak シーケンスまたはコンストラクトの区切り記号のいずれかによって、値を終了する前に、すべてのコンテキストを終了する必要があります。

Linebreak の終端文字のシーケンスまたはコンストラクトの区切り記号には、値の一部はありません。

値は省略可能で、 [GDL 属性](gdl-attributes.md)します。

*マクロの参照を値*任意の場所が表示される GDL 値でリテラルでない空白が許可されています。 等号 (=) でこれらの参照を開始します。 このようなコンテキストで等号を使用すると、値マクロのリファレンスを紹介するものではありません、等号 (=) は非記号文字 (空白) などで後にする必要があります。 マクロの値の詳細については、次を参照してください。 [GDL 値マクロ](gdl-value-macros.md)します。

GDL コンテキストの詳細については、次を参照してください。 [GDL コンテキスト](gdl-contexts.md)します。

次のコード例では、GDL パーサーに許容される値を示します。

```cpp
*Value: *%  Null Value - only a comment

*Value: "Quoted String"

*Value: "Quoted String with Hex substring: <48 65 78> see?"

*Value: "Hex substring with comment and macro reference <48 *% comment
65 78 =MacroRef > see?"   *% note continuation linebreak was automatically assumed

*Value: tokens (parenthesis context) [followed by square brackets context] "ending in quoted string"

*Value: tokens (parenthesis context {with nested curly braces context})

*Value:  tokens <BeginValue:anything> no special characters or contexts recognized within an arbitrary value context.  " } ) * % < > anything goes, sorry  =MacroRefs not recognized
*Keyword:  looks like a new entry but its still within the Arbitrary Value context.
+  not continuation chars, *% this is not a comment  <EndValue:anything>
```

 

 




