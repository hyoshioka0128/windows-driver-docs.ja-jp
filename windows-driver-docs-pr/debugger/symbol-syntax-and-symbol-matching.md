---
title: シンボルの構文とシンボルの照合
description: シンボルの構文とシンボルの照合
ms.assetid: 7fda24bf-57be-4c7d-9eff-bd688de7cf1b
keywords:
- シンボル、シンボルの構文
- シンボル、シンボルに一致します。
- シンボル、シンボルのサフィックス
- $ (ローカル シンボル識別子)、コマンドの構文規則
- $ (ローカル シンボル識別子)
- ローカル シンボル識別子 ($)
- ローカル変数は、ローカル シンボル識別子 ($)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07451ed31f6d92f26ebbadfbddadd9ca6bf6f932
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335498"
---
# <a name="symbol-syntax-and-symbol-matching"></a>シンボルの構文とシンボルの照合


## <span id="ddk_symbol_syntax_and_symbol_matching_dbg"></span><span id="DDK_SYMBOL_SYNTAX_AND_SYMBOL_MATCHING_DBG"></span>


シンボルを使用すると、デバッグ中のプログラムで使用されるトークンを直接操作できます。 関数にブレークポイントを設定するなど、**メイン**コマンドを使用して**bp メイン**、整数変数を表示または**MyInt**コマンドを使用して**ddたとえば、MyInt L1**します。

多くの場合、デバッガー コマンドのパラメーターとしてシンボルを使用できます。 これにより、ほとんどの数値パラメーターはサポートされており、いくつかのテキスト パラメーターでもサポートされます。 一般的な規則に加えてシンボルの構文については、これらの各ケースで適用されるシンボルの構文ルールもあります。

### <a name="span-idgeneralsymbolsyntaxrulesspanspan-idgeneralsymbolsyntaxrulesspangeneral-symbol-syntax-rules"></a><span id="general_symbol_syntax_rules"></span><span id="GENERAL_SYMBOL_SYNTAX_RULES"></span>一般的な記号構文規則

シンボル名の 1 つ以上の文字で構成されていますが、常に、文字で始まりアンダー スコア (**\_**)、疑問符 (**?**)、またはドル記号 (**$**).

シンボル名は、モジュール名で修飾することがあります。 感嘆符 (**!**)、モジュール名を区切る記号から (たとえば、 **mymodule! メイン**)。 モジュール名を使用しない場合、シンボルは、感嘆符の付いたがプレフィックスとしてください。 モジュール名のない、感嘆符を使用すると、パラメーターは、名前と 16 進数ではなくデバッガー コマンドに示すために、ローカル変数の場合でも、特に便利なことができます。 たとえば、変数**フェード**によって読み取られる、 [ **dt (表示の種類)** ](dt--display-type-.md)感嘆符が付いてまたは-n オプションを使用しない限り、アドレスとしてコマンドします。 ただし、シンボルがローカルであることを指定する前にドル記号 ($) と、感嘆符 (! )、うに **$! ライム**します。

シンボル名は完全に大文字です。 こうすることのプレゼンスを**myInt**と**MyInt**で、デバッガーでプログラムが正しく認識されませんこれらのいずれかを参照する任意のコマンドは、もう 1 つ、方法に関係なくアクセス可能性があります。コマンドが大文字で入力します。

### <a name="span-idsymbolsyntaxinnumericalexpressionsspanspan-idsymbolsyntaxinnumericalexpressionsspansymbol-syntax-in-numerical-expressions"></a><span id="symbol_syntax_in_numerical_expressions"></span><span id="SYMBOL_SYNTAX_IN_NUMERICAL_EXPRESSIONS"></span>数値式でのシンボルの構文

デバッガーでは、2 つの異なる種類の式を認識します。Microsoft のマクロ アセンブラー (MASM) の式は、C++ の式。 シンボルはに関しては、これら 2 つの形式の構文は次のように違いがあります。

-   MASM の式では、各シンボルは、アドレスとして解釈されます。 によって、どのようなシンボルが参照されているグローバル変数、ローカル変数、関数、セグメント、モジュール、またはその他の任意の認識されているラベルのアドレスになります。

-   C++ の式では、各シンボルはその型に従って解釈されます。 シンボルが参照する対象、によって、整数、データ構造体、関数ポインター、またはその他の任意のデータ型として解釈可能性があります。 シンボル (変更されていないモジュール名) などの C++ データ型に対応するいないと、構文エラーが発生します。

各種類の構文を使用するタイミングと方法の詳細については、次を参照してください。[を評価する式](evaluating-expressions.md)します。

MASM 式の構文、レジスタ、または 16 進数として解釈できます任意のシンボルを使用している場合 (例: **BadFeed**、 **ebX**) 常に感嘆符を付ける必要があります。 これにより、デバッガーがシンボルとして認識します。

[ **Ss (設定記号サフィックス)** ](ss--set-symbol-suffix-.md)記号のサフィックスを設定するコマンドを使用できます。 これには、デバッガーを自動的にそれを見つけられない、シンボル名に"A"または"W"を追加するように指示します。

多くの Win32 ルーチンは、ASCII および Unicode の両方のバージョンに存在します。 多くの場合、これらのルーチンがある、"A"または"W"はそれぞれ、その名前の末尾に追加されます。 記号のサフィックスを使用してこれらのシンボルを検索するときは、デバッガー、役立ちます。

サフィックス一致が既定でアクティブでないです。

### <a name="span-idsymbolsyntaxintextexpressionsspanspan-idsymbolsyntaxintextexpressionsspansymbol-syntax-in-text-expressions"></a><span id="symbol_syntax_in_text_expressions"></span><span id="SYMBOL_SYNTAX_IN_TEXT_EXPRESSIONS"></span>テキスト式の構文をシンボル

シンボルをなど、いくつかのコマンドのテキスト パラメーターに使用できます[ **bm (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)と[ **(シンボルを調べる) x**](x--examine-symbols-.md)します。

これらのテキスト パラメーターは、さまざまなワイルドカードと指定子をサポートします。 参照してください[文字列のワイルドカード構文](string-wildcard-syntax.md)詳細についてはします。 だけでなく、標準の文字列のワイルドカードとして先頭にアンダー スコアでシンボルの指定に使用されるテキスト式に付けることができます。 これをシンボルに一致した場合、デバッガーはこのとして扱います任意の分量のアンダー スコア、0 であっても。

記号は、テキスト式で一致する場合は、記号のサフィックスは使用しません。

 

 





