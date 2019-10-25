---
title: 拡張機能の引数の解析
description: 拡張機能の引数の解析
ms.assetid: 3c75fb75-50d0-48e4-abf4-e4dba9a080f9
keywords:
- EngExtCpp 拡張, 引数の解析
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e0c145b8fdd2e01b19155a4ad1727b13a68a43e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838819"
---
# <a name="parsing-extension-arguments"></a>拡張機能の引数の解析


EngExtCpp extension framework には、拡張機能に渡されるコマンドライン引数を解析するためのメソッドが用意されています。 これらのメソッドを利用するには、まず、拡張機能が[**EXT\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command)マクロでコマンドライン引数の形式を宣言する必要があります。

フレームワークによって実行されるコマンドライン引数の解析をバイパスし、拡張機能自体が引数を解析できるようにするには、コマンドラインの説明を `"{{custom}}"` に設定し、メソッド[**GetRawArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548226(v=vs.85))を使用して解析用のコマンドライン引数を取得します。

コマンドラインの説明文字列は、表示の列幅に合わせるために、印刷時に自動的に折り返されます。 ただし、改行文字は、"`\n`" を使用して新しい行を開始する、説明文字列に埋め込むことができます。

コマンドラインの説明には、 **NULL**または空の文字列を指定できます。 どちらかが発生した場合は、拡張コマンドが引数を受け取らないことを示します。

### <a name="span-idcommand_line_descriptionspanspan-idcommand_line_descriptionspancommand-line-description"></a><span id="command_line_description"></span><span id="COMMAND_LINE_DESCRIPTION"></span>コマンドラインの説明

コマンドライン引数の説明は、ディレクティブと引数という2種類のコンポーネントを含むシーケンスです。 説明には、必要に応じて各ディレクティブの1つを含めることができ、最大64個の引数を含めることができます。

### <a name="span-iddirectivesspanspan-iddirectivesspandirectives"></a><span id="directives"></span><span id="DIRECTIVES"></span>指示

ディレクティブは、引数の解析方法を指定します。 これらは、2つの中かっこ (`'{{'` および `'}}'`) で囲まれています。 各ディレクティブは、引数を説明する文字列で、任意で0回または1回出現できます。

次のディレクティブを使用できます。

<span id="custom"></span><span id="CUSTOM"></span>`custom`  
拡張機能フレームワークによって実行される解析をオフにして、拡張機能が独自の解析を実行できるようにします。

<span id="l_str"></span><span id="L_STR"></span>`l:str`  
コマンドライン引数の既定の長い説明をオーバーライドします。 拡張フレームワークは、すべての引数の完全な説明に*str*を使用します。

<span id="opt_str"></span><span id="OPT_STR"></span>`opt:str`  
名前付きコマンドの既定のプレフィックス文字をオーバーライドします。 既定値は `"/-"`であり、名前付き引数を識別するプレフィックスとして '`/`' または '`-`' を使用できます。

<span id="s_str"></span><span id="S_STR"></span>`s:str`  
コマンドライン引数の既定の短い説明をオーバーライドします。 拡張フレームワークは、すべての引数の簡単な説明に*str*を使用します。

ディレクティブの例をいくつか次に示します。 次の文字列は、独自の引数を解析する拡張コマンドによって使用されます。 また、次のように、自動 **! help**拡張コマンドで使用するための短い説明と長い説明も提供します。

```dbgcmd
{{custom}}{{s:<arg1> <arg2>}}{{l:arg1 - Argument 1\narg2 - Argument 2}}
```

次の文字列は、引数オプションのプレフィックス文字を '`/`' または '`-`' に変更します。 このディレクティブを使用すると、'`/arg`' および '`-arg`' ではなく、'`+arg`' と '`:arg`' を使用して引数が指定されます。

```dbgcmd
{{opt:+:}}
```

### <a name="span-idargumentsspanspan-idargumentsspanarguments"></a><span id="arguments"></span><span id="ARGUMENTS"></span>数値

引数には、という2つの型を指定できます。 名前のない引数は read 位置です。 どちらの種類の引数にも、ヘルプコマンドによって使用される表示名があります。

引数の記述は、1つの中かっこ (`'{'` および `'}'`) で囲まれています。

各引数の説明には、次の構文があります。

```dbgcmd
{[optname];[type[,flags]];[argname];[argdesc]}
```

この場合

<span id="optname"></span><span id="OPTNAME"></span>*optname*  
引数の名前。 これは、コマンドで使用される名前であり、名前で引数を取得するメソッドでも使用されます。 この名前は省略可能です。 引数が存在する場合、引数は "名前付き引数" になります。コマンドライン上の任意の場所に記述でき、名前で参照されます。 存在しない場合、引数は "無名の引数" になります。コマンドライン上での位置は重要であり、他の名前のない引数に対する相対的な位置によって参照されています。

<span id="type"></span><span id="TYPE"></span>*各種*  
引数の型。 これは、引数がどのように解析され、どのように取得されるかに影響します。 *型*パラメーターには、次のいずれかの値を指定できます。

<span id="b"></span><span id="B"></span>b  
ブール型。 引数が存在するか、存在しません。 名前付きブール型の引数は、 [**Hasarg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549721(v=vs.85))を使用して取得できます。

<span id="e_d__s__bits_"></span><span id="E_D__S__BITS_"></span>e\[d\]\[s\]\[ビット\]  
式の型。 引数には数値が含まれています。 名前付きの式の引数は、 [**GetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545596(v=vs.85))を使用して取得できます。名前のない式の引数は、 [**GetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549465(v=vs.85))を使用して取得できます。

<span id="d"></span><span id="D"></span>a  
式は、引数文字列内の次の空白文字に制限されます。 この値が指定されていない場合、式エバリュエーターは、式の末尾に到達するまでコマンドラインから文字を使用します。

<span id="s"></span><span id="S"></span>2$s  
式の値が署名されています。 それ以外の場合、式の値は符号なしになります。

<span id="bits"></span><span id="BITS"></span>列  
引数の値のビット数。 *ビット*の最大値は64です。

<span id="s"></span><span id="S"></span>2$s  
文字列型。 文字列は、次の空白文字に制限されます。 名前付き文字列引数は、 [**GetArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545586(v=vs.85))を使用して取得できます。また、名前のない文字列引数は、 [**Getunnamedargstr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549464(v=vs.85))を使用して取得できます。

<span id="x"></span><span id="X"></span>閉じる  
文字列型。 引数は、コマンドラインの残りの部分です。 引数は、s 文字列型と同様に、 **GetArgStr**または**Getunnamedargstr**を使用して取得されます。

<span id="flags"></span><span id="FLAGS"></span>*示す*  
引数フラグ。 これらは、引数がパーサーによってどのように処理されるかを決定します。 *Flags*パラメーターには、次のいずれかの値を指定できます。

<span id="d_expr"></span><span id="D_EXPR"></span>d = expr  
引数の既定値。 引数がコマンドラインに存在しない場合、引数は*expr*に設定されます。 既定値は、引数の型に従って解析される文字列です。

<span id="ds"></span><span id="DS"></span>ds  
既定値は、ヘルプで指定されている引数の説明には表示されません。

<span id="o"></span><span id="O"></span>i/o  
引数は省略可能です。 これは、名前付き引数の既定値です。

<span id="r"></span><span id="R"></span>\r\n\r\n  
引数は必須です。 これは、名前のない引数の既定値です。

<span id="argname"></span><span id="ARGNAME"></span>*argname*  
引数の表示名。 これは、自動 **! help**拡張コマンドによって使用される名前であり、自動 **/?** または **-?** コマンドライン引数。 コマンドラインオプションの概要を印刷するときに使用します。

<span id="argdesc"></span><span id="ARGDESC"></span>*argdesc*  
引数の説明。 これは、自動 **! ヘルプ**拡張機能と自動 " **/?** " によって出力された説明です。 または " **-?** " コマンドライン引数。

引数の説明の例をいくつか次に示します。 次の式は、1つの省略可能な式引数を受け取るコマンドを定義します。 引数は32ビットに収める必要があります。 引数がコマンドラインに存在しない場合は、既定値の0x100 が使用されます。

```dbgcmd
{;e32,o,d=0x100;flags;Flags to control command}
```

次の式では、省略可能なブール値の " **/v**" 引数と、必須の名前のない文字列引数を持つコマンドを定義しています。

```dbgcmd
{v;b;;Verbose mode}{;s;name;Name of object}
```

次の式では、省略可能な名前付きの式の引数 **/oname** *expr*と省略可能な名前付きの文字列引数 **/eol** *str*を持つコマンドを定義しています。 **/Eol**が存在する場合、その値はコマンドラインの残りの部分に設定され、それ以上の引数は解析されません。

```dbgcmd
{oname;e;expr;Address of object}{eol;x;str;Commands to use}
```

### <a name="span-idcommand_linespanspan-idcommand_linespancommand-line"></a><span id="command_line"></span><span id="COMMAND_LINE"></span>コマンドライン

コマンドラインで引数を解析するいくつかの方法の一覧を次に示します。

-   名前付きの式と文字列の引数の値は、コマンドラインでの名前の後に続きます。 たとえば、 **/name** *expr*や **/name** *str*などです。

-   名前付きブール値の引数の場合、名前がコマンドラインに表示される場合、値は true になります。それ以外の場合は false。

-   コマンドラインでは、複数の単一文字の名前付き Boolean オプションをグループ化できます。 たとえば、"/a/b/c" は、"abc" という名前の引数が既に存在しない限り、短縮形 "/abc" を使用して記述できます。

-   コマンドラインに名前付き引数 "?" が含まれている場合 (例: "/?") and "-?" -引数の解析が終了し、拡張機能のヘルプテキストが表示されます。

### <a name="span-idparsing_internalsspanspan-idparsing_internalsspanparsing-internals"></a><span id="parsing_internals"></span><span id="PARSING_INTERNALS"></span>内部の解析

引数パーサーは引数を設定するために、いくつかのメソッドを使用します。

[**Setunnamedarg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556876(v=vs.85))メソッドによって、名前のない引数の値が変更されます。 また、便宜上、 [**Setunnamedargstr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556878(v=vs.85))メソッドと[**SetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556879(v=vs.85))メソッドは、名前のない文字列と式の引数をそれぞれ設定します。

名前付き引数にも同様のメソッドが存在します。 [**Setarg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556614(v=vs.85))は、名前付き引数と[**setargstr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556618(v=vs.85))の値を変更するために使用されます。また、 [**SetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556622(v=vs.85))は、名前付き文字列引数と式引数にそれぞれ使用されます。

 

 





