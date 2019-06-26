---
title: 拡張機能の引数の解析
description: 拡張機能の引数の解析
ms.assetid: 3c75fb75-50d0-48e4-abf4-e4dba9a080f9
keywords:
- 引数の解析、EngExtCpp 拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5413c3ddcce566300e6f96f4ca0f0892dfbda85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366452"
---
# <a name="parsing-extension-arguments"></a>拡張機能の引数の解析


EngExtCpp の拡張機能フレームワークでは、拡張機能に渡されるコマンドライン引数の解析で支援するメソッドを提供します。 これらのメソッドを利用する、拡張する必要があります最初の形式を宣言でコマンドライン引数、 [ **EXT\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nf-engextcpp-ext_command)マクロ。

コマンドライン引数の解析、フレームワークによって実行をバイパスし、拡張機能自体、引数の解析、コマンドラインの説明に設定できるように`"{{custom}}"`メソッドを使用して[ **GetRawArgStr** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548226(v=vs.85))を解析するためのコマンドライン引数を取得します。

表示の列の幅に合わせて、印刷時に、コマンドラインの説明文字列が自動的にラップされます。 ただし、改行文字を使用して、説明文字列に埋め込むことできます '`\n`' - 新しい行を開始します。

コマンド ライン説明できます**NULL**または空の文字列。 いずれかが発生した場合は、拡張機能のコマンドは、任意の引数を受け取らないことを示します。

### <a name="span-idcommandlinedescriptionspanspan-idcommandlinedescriptionspancommand-line-description"></a><span id="command_line_description"></span><span id="COMMAND_LINE_DESCRIPTION"></span>コマンドラインの説明

コマンドライン引数の説明は、2 種類のコンポーネントを含むシーケンス。 ディレクティブと引数。 説明は、必要に応じて各ディレクティブのいずれかを含めることができ、最大 64 個の引数を含めることができます。

### <a name="span-iddirectivesspanspan-iddirectivesspandirectives"></a><span id="directives"></span><span id="DIRECTIVES"></span>ディレクティブ

ディレクティブは、引数の解析方法を指定します。 二重中かっこで囲まれていますが (`'{{'`と`'}}'`)。 各ディレクティブにゼロが表示されることができます必要に応じて 1 回、文字列の説明または引数します。

次のディレクティブを使用できます。

<span id="custom"></span><span id="CUSTOM"></span>`custom`  
拡張機能フレームワークによって実行、解析をオフにでき、拡張機能を独自の解析を実行できます。

<span id="l_str"></span><span id="L_STR"></span>`l:str`  
コマンドライン引数の既定の長い説明をオーバーライドします。 拡張フレームワークを使用して*str*のすべての引数の詳細について説明します。

<span id="opt_str"></span><span id="OPT_STR"></span>`opt:str`  
名前付きコマンドの既定のプレフィックス文字を上書きします。 既定値は`"/-"`できるので、'`/`'または'`-`' プレフィックスを識別する名前付き引数として使用します。

<span id="s_str"></span><span id="S_STR"></span>`s:str`  
コマンドライン引数の既定の短い説明をオーバーライドします。 拡張機能フレームワークを使用して*str*のすべての引数の短い説明。

ディレクティブの例をいくつかを示します。 次の文字列は、自身の引数を解析する拡張機能コマンドによって使用されます。 自動で使用するための短期および長期の説明も提供 **! ヘルプ**拡張機能コマンド。

```dbgcmd
{{custom}}{{s:<arg1> <arg2>}}{{l:arg1 - Argument 1\narg2 - Argument 2}}
```

次の文字列の変更、引数のオプションのプレフィックス文字を '`/`'または'`-`'。 このディレクティブを指定された引数は指定を使用して '`+arg`'と'`:arg`' の代わりに '`/arg`'と'`-arg`'。

```dbgcmd
{{opt:+:}}
```

### <a name="span-idargumentsspanspan-idargumentsspanarguments"></a><span id="arguments"></span><span id="ARGUMENTS"></span>引数

2 つの型の引数を指定できます: という名前のないです。 名前のない引数が位置読み取られます。 両方の種類の引数には、ヘルプ コマンドで使用される表示名もがあります。

引数の説明については、1 つの中かっこで囲まれています (`'{'`と`'}'`)。

各引数の説明では、次の構文があります。

```dbgcmd
{[optname];[type[,flags]];[argname];[argdesc]}
```

それぞれの文字の説明は次のとおりです。

<span id="optname"></span><span id="OPTNAME"></span>*optname*  
引数の名前。 これは、名前でコマンドと引数をフェッチするメソッドを使用する名前です。 この名前は省略可能です。 引数が「名前付き引数;」になりますが存在する場合コマンドラインで任意の場所に表示されることができ、名前で参照されます。 引数が「名前なし引数;」になりますが存在しない場合コマンドライン上での位置が重要と名前のない他の引数に対する相対位置を使用して参照されています。

<span id="type"></span><span id="TYPE"></span>*型*  
引数の型。 これは、引数を解析する方法とを取得する方法に影響します。 *型*パラメーターには、次の値の 1 つには。

<span id="b"></span><span id="B"></span>B  
ブール型。 引数では存在するか、存在しません。 使用してブール型の名前付き引数を取得できる[ **HasArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549721(v=vs.85))します。

<span id="e_d__s__bits_"></span><span id="E_D__S__BITS_"></span>e\[d\]\[s\]\[ビット\]  
式の型。 引数には、数値の値があります。 使用して名前付きの式の引数を取得できる[ **GetArgU64** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545596(v=vs.85))と名前のない式の引数を使用して取得できる[ **GetUnnamedArgU64** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549465(v=vs.85)).

<span id="d"></span><span id="D"></span>D  
式では、引数文字列に次の空白文字に制限されています。 これが存在しない場合、式の末尾に達したことを決定するまで、式エバリュエーターは、コマンドラインからの文字を消費します。

<span id="s"></span><span id="S"></span>s  
式の値が署名されています。 それ以外の場合、式の値は、符号付きではありません。

<span id="bits"></span><span id="BITS"></span>Bits  
引数の値のビット数。 最大値*ビット*64 です。

<span id="s"></span><span id="S"></span>s  
型の文字列を指定します。 文字列は、次の空白文字に制限されます。 使用して名前付きの文字列引数を取得できる[ **GetArgStr** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545586(v=vs.85))と名前のない文字列引数を使用して取得できる[ **GetUnnamedArgStr** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549464(v=vs.85)).

<span id="x"></span><span id="X"></span>X  
型の文字列を指定します。 引数では、コマンドラインの残りの部分です。 使用して、引数を取得**GetArgStr**または**GetUnnamedArgStr**文字列型と同様に、します。

<span id="flags"></span><span id="FLAGS"></span>*フラグ*  
引数のフラグ。 これらは、パーサーによっての引数の処理方法を決定します。 *フラグ*パラメーターには、次の値の 1 つには。

<span id="d_expr"></span><span id="D_EXPR"></span>d=expr  
引数の既定値。 引数がコマンドライン上に存在するかどうかは、引数に設定されている*expr*します。 既定値は、引数の型に従って解析される文字列です。

<span id="ds"></span><span id="DS"></span>ds  
既定値は、ヘルプで提供される引数の説明では表示されません。

<span id="o"></span><span id="O"></span>O  
引数は省略可能です。 これは、名前付き引数の既定値です。

<span id="r"></span><span id="R"></span>r  
引数が必要です。 これは、名前のない引数の既定値です。

<span id="argname"></span><span id="ARGNAME"></span>*argname*  
引数の表示名。 これは、自動で使用される名前 **! ヘルプ**コマンドと、自動拡張 **/でしょうか。** または **-でしょうか。** コマンドライン引数。 コマンド ライン オプションの概要を印刷するときに使用されます。

<span id="argdesc"></span><span id="ARGDESC"></span>*argdesc*  
引数の説明です。 これは、自動で印刷される説明 **! ヘルプ**拡張機能と、自動で" **/でしょうか**"。 または" **-?** " コマンドライン引数。

引数の説明のいくつかの例を示します。 次の式では、1 つの省略可能な式の引数を取るコマンドを定義します。 引数は、32 ビットに収まる必要があります。 コマンドラインで引数がない場合 0x100 の既定値が使用されます。

```dbgcmd
{;e32,o,d=0x100;flags;Flags to control command}
```

次の式は、省略可能なブール値を持つコマンドを定義します" **/v**"引数と名前のない文字列が必要な引数。

```dbgcmd
{v;b;;Verbose mode}{;s;name;Name of object}
```

次の式を持つ式引数をという名前で、省略可能なコマンドを定義する **/oname** *expr*と省略可能な文字列引数を名前付き **/eol** *str*します。 場合 **/eol**が存在する場合は、その値は、コマンドラインの残りの部分を設定して、さらに引数を解析できません。

```dbgcmd
{oname;e;expr;Address of object}{eol;x;str;Commands to use}
```

### <a name="span-idcommandlinespanspan-idcommandlinespancommand-line"></a><span id="command_line"></span><span id="COMMAND_LINE"></span>コマンド ライン

次のコマンドラインで引数を解析する方法をいくつか示します。

-   名前付きの式と文字列引数の値では、コマンドラインで、名前に従います。 たとえば、 **/name** *expr*または **/name** *str*します。

-   名前付きのブール型引数の値が true の場合、名前、コマンドラインに表示されます。false それ以外の場合。

-   複数の単一の文字で名前付きのブール型オプションは、コマンドラインで化できます。 短縮形表記を使用して"/a/b/c"を書き込むことが、"/abc"("abc"という名前の引数がまだない) 場合。

-   コマンド ラインには、名前付き引数が含まれている場合"?"、「/?」 "のでしょうか"。 -引数解析が終了し、拡張機能のヘルプ テキストが表示されます。

### <a name="span-idparsinginternalsspanspan-idparsinginternalsspanparsing-internals"></a><span id="parsing_internals"></span><span id="PARSING_INTERNALS"></span>内部の解析

いくつかのメソッドは、引数を設定する引数のパーサーによって使用されます。

メソッド[ **SetUnnamedArg** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556876(v=vs.85))名前なし引数の値が変更されます。 利便性のため、メソッド、 [ **SetUnnamedArgStr** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556878(v=vs.85))と[ **SetUnnamedArgU64** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556879(v=vs.85))名前のない文字列と式に設定されます引数それぞれします。

名前付き引数の同様のメソッドが存在します。 [**SetArg** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556614(v=vs.85))名前付き引数の値を変更するために使用し、 [ **SetArgStr** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556618(v=vs.85))と[ **SetArgU64** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556622(v=vs.85))文字列と式の名前付き引数のそれぞれ使用します。

 

 





