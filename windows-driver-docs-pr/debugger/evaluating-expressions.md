---
title: 式の評価
description: 式の評価
ms.assetid: f2fbdac1-2c20-4132-b43e-4c7a90a2f5b7
keywords:
- 式、概要
- さまざまな種類の式
- MASM の式を使用する場合
- C++ の式を使用する場合
- MASM 式, 概要
- C++ の式、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 107b2371f223bb31933bfcfc346496fcfd8d4820
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379445"
---
# <a name="evaluating-expressions"></a>式の評価


## <span id="ddk_evaluating_expressions_dbg"></span><span id="DDK_EVALUATING_EXPRESSIONS_DBG"></span>


デバッガーでは、式の 2 つの異なる形式を認識します。*MASM 式*と*C++ 式*します。

Microsoft マクロ アセンブラー (MASM) の式は、場合に特にそれ以外の場合を除き、このヘルプ ドキュメントの例で使用されます。 MASM の式では、すべてのシンボルはアドレスとして扱われます。

C++ の式は、実際の C++ コードで使用されるものと同じです。 これらの式では、シンボルは、適切なデータ型として解釈されます。

### <a name="span-idwheneachsyntaxisusedspanspan-idwheneachsyntaxisusedspanwhen-each-syntax-is-used"></a><span id="when_each_syntax_is_used"></span><span id="WHEN_EACH_SYNTAX_IS_USED"></span>各構文を使用する場合

次の方法のいずれかで、既定の式エバリュエーターを選択できます。

-   使用して、 \_NT\_EXPR\_EVAL[環境変数](general-environment-variables.md)デバッガーを開始する前にします。

-   使用して、 **ee** {**masm**|**c++**}[コマンド ライン オプション](command-line-options.md)デバッガーが開始された場合。

-   使用して、 [ **.expr (選択式エバリュエーター)** ](-expr--choose-expression-evaluator-.md)コマンドを表示またはデバッガーの実行後に、式エバリュエーターを変更します。

上記の方法のいずれかを使用しない場合、デバッガーは、MASM 式エバリュエーターを使用します。

デバッガーの状態を変更することがなく、式を評価する場合は、使用、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md)コマンド。

すべてのコマンドとデバッグ情報のウィンドウは、既定式エバリュエーターの次の例外では、その引数を解釈します。

-   [**いますか。(C++ の式の評価)** ](----evaluate-c---expression-.md)コマンドは、常に、C++ の式エバリュエーターを使用します。

-   [ウォッチ] ウィンドウには、C++ の式エバリュエーターが使用されます。

-   [[ローカル] ウィンドウ](locals-window.md)C++ の式エバリュエーターは常に使用します。

-   拡張機能のいくつかのコマンドは常に MASM 式エバリュエーターを使用して (およびその他の拡張機能のコマンドは、完全な式ではなく数値引数のみをそのまま使用)。

-   式の一部をかっこで囲まれた 2 つのアットを挿入すると (**@@**) しない通常使用されるこの場合、式エバリュエーターが式では、前に、式を評価します。

アット マークから 2 つ (**@@**) を使用すると、1 つのコマンドのさまざまなパラメーターの 2 つの異なるエバリュエーターを使用します。 また、さまざまな方法でさまざまな型の式を評価することもできます。 アット マークから 2 つを入れ子にすることができます。 アット マークから 2 つの各の外観は、その他の式エバリュエーターに切り替わります。

**警告**   C++ 式の構文は構造体と、変数を操作するために便利ですが、デバッガー コマンドのパラメーターのパーサーとして最適ではありません。 汎用目的で、デバッガー コマンドを使用しているか、デバッガーの拡張機能を使用している、ときに、既定の式エバリュエーターとして MASM 式の構文を設定してください。 C++ 式の構文を使用して、特定のパラメーターが必要な場合は、アット マーク、2 つを使用して (**@@**) 構文。

 

2 つの式のさまざまな種類の詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

### <a name="span-idnumbersinexpressionsspanspan-idnumbersinexpressionsspannumbers-in-expressions"></a><span id="numbers_in_expressions"></span><span id="NUMBERS_IN_EXPRESSIONS"></span>式内の番号

MASM の式内の番号は現在の基数に従って解釈されます。 [ **N (設定数の基本)** ](n--set-number-base-.md) 16、10、または 8 の既定の基数を設定するコマンドを使用できます。 すべてのプレフィックスが指定されていない番号は、このベースで解釈されます。 既定の基数を指定することによってオーバーライドできます、 **0 x**プレフィックス (16 進数)、 **0n**プレフィックス (10 進数)、 **0t**プレフィックス (8 進数)、または**0y**プレフィックス (バイナリ)。

C++ の式内の番号は、異なる方法で指定しない限り、10 進数として解釈されます。 16 進数の整数を指定する追加**0 x**番号の前にします。 8 進数の整数を指定する追加**0**番号の前に (0)。 (ただしでは、デバッガーの*出力*、 **0n** 10 進数のプレフィックスが使用される場合があります)。

同時に複数のベースで数値を表示する場合を使用して、 [ **(番号の形式の表示) .formats** ](-formats--show-number-formats-.md)コマンド。

### <a name="span-idsymbolsinexpressionsspanspan-idsymbolsinexpressionsspansymbols-in-expressions"></a><span id="symbols_in_expressions"></span><span id="SYMBOLS_IN_EXPRESSIONS"></span>式内のシンボル

2 種類の式の解釈が異なるシンボル。

-   MASM の式では、各シンボルは、アドレスとして解釈されます。 シンボルが参照する対象、によっては、このアドレスは、グローバル変数、ローカル変数、関数、セグメント、モジュール、またはその他の任意の認識されているラベルのアドレスです。

-   C++ の式では、各シンボルはその型に従って解釈されます。 によって、シンボルが参照する対象、整数、データ構造体、関数ポインター、またはその他の任意のデータ型として解釈可能性があります。 (変更されていないモジュール名) などの C++ データ型に対応していないシンボルは、構文エラーを作成します。

シンボルが不明確な場合、場合の前に、モジュール名と感嘆符 ( **!** ). シンボル名は、16 進数として解釈されますが場合の前に、モジュール名と感嘆符 ( **!** ) または感嘆符のみです。 ローカル シンボルはさせようとしているを指定するには、モジュール名を省略し、ドル記号と感嘆符が含まれます ( **$!** ) シンボル名の前にします。 シンボルの解釈に関する詳細については、次を参照してください。[シンボルの構文と一致するシンボル](symbol-syntax-and-symbol-matching.md)します。

### <a name="span-idoperatorsinexpressionsspanspan-idoperatorsinexpressionsspanoperators-in-expressions"></a><span id="operators_in_expressions"></span><span id="OPERATORS_IN_EXPRESSIONS"></span>式の演算子

各式の型は、演算子の別のコレクションを使用します。

MASM の式とその優先順位ルールで使用できる演算子の詳細については、次を参照してください。 [MASM 数字と演算子](masm-numbers-and-operators.md)します。

C++ の式とその優先順位ルールで使用できる演算子の詳細については、次を参照してください。 [C++ 数字と演算子](c---numbers-and-operators.md)します。

MASM の操作はバイト単位では常に、C++ の操作 (ポインターの算術演算のスケーリングを含む) C++ 型のルールに従うことに注意してください。

別の構文の例については、次を参照してください。[式の例](expression-examples.md)します。

 

 





