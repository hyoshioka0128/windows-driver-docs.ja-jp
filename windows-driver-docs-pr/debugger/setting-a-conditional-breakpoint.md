---
title: WinDbg および他の Windows デバッガーの条件付きブレークポイント
description: WinDbg およびその他の Windows デバッガーでの条件付きブレークポイントは、特定の条件が満たされる場合にのみ中断する必要がある場合に便利です。
ms.assetid: 9fa5b417-8904-48bc-ad5c-62ba35d70b73
keywords:
- 条件付きブレークポイント
- 条件付きブレークポイント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5687bf16b7330076ec81802772c02f9110f16a72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381984"
---
# <a name="conditional-breakpoints-in-windbg-and-other-windows-debuggers"></a>WinDbg および他の Windows デバッガーの条件付きブレークポイント


WinDbg およびその他の Windows デバッガーでの条件付きブレークポイントは、特定の条件が満たされる場合にのみ中断する必要がある場合に便利です。

## <span id="ddk_setting_a_conditional_breakpoint_dbg"></span><span id="DDK_SETTING_A_CONDITIONAL_BREAKPOINT_DBG"></span>


条件付きブレークポイントがいずれかのブレークポイントのコマンドを組み合わせることで作成された、 [ **j (を実行する場合 - その他)** ](j--execute-if---else-.md)コマンドまたは[ **.if** ](-if.md)トークン、その後に、 [ **gc (条件付きブレークポイントから移動)** ](gc--go-from-conditional-breakpoint-.md)コマンド。 このブレークポイントは、特定の条件が満たされる場合にのみに発生するブレークを発生させます。

使用して条件付きブレークポイントの基本的な構文、 **j**コマンドを次に示します。

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'gc' "
```

使用して条件付きブレークポイントの基本的な構文、 **.if**トークンのとおりです。

```dbgcmd
0:000> bp Address ".if (Condition) {OptionalCommands} .else {gc}"
```

条件付きブレークポイントは最適な例を示します。 次のコマンド ライン 143 Mysource.cpp ソース ファイルのブレークポイントを設定します。 このブレークポイントのヒット時は、変数**MyVar**をテストします。 場合、この変数は、20 未満の実行は続行されます。20 を超える場合は、実行を停止します。

```dbgcmd
0:000> bp `mysource.cpp:143` "j (poi(MyVar)>0n20) ''; 'gc' " 
0:000> bp `mysource.cpp:143` ".if (poi(MyVar)>0n20) {} .else {gc}"
```

上記のコマンドでは、次の要素を含む非常に複雑な構文があります。

-   [ **Bp (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドにブレークポイントを設定します。 前の例は、bp コマンドを使用して、使用することも、 **bu (未解決のブレークポイントの設定)** コマンド。 間の相違点の詳細については**bp**と**bu**、ブレークポイントに基本的な概要については、次を参照してください。 と[を使用してブレークポイント](using-breakpoints.md)します。

-   グレーブ アクセント記号を使用してソース行番号を指定 ( **\`** )。 詳細については、次を参照してください。[ソース行構文](source-line-syntax.md)します。

-   ブレークポイントにヒットすると、二重引用符内のコマンド ( **"** ) を実行します。 このコマンドは、この例で、 [ **j (を実行する場合 - その他)** ](j--execute-if---else-.md)コマンドまたは[ **.if** ](-if.md)トークンは、かっこで囲まれた式をテストします。

-   ソース プログラムで、 **MyVar**は整数です。 C++ の式の構文を使用している場合**MyVar**は整数として解釈されます。 ただし、この例 (とデバッガーの既定の構成)、MASM 式の構文が使用されます。 MASM 式、 **MyVar**アドレスとして扱われます。 そのため、使用する必要があります、 **poi**逆参照演算子。 (実際には、変数に C ポインターの場合必要がありますを 2 回 - 逆参照することなど**poi(poi(MyPtr))**)。**0n**プレフィックスは、この数値が 10 進数であるを指定します。 構文の詳細については、次を参照してください。 [MASM 数字と演算子](masm-numbers-and-operators.md)します。

-   かっこ内の式には単一引用符で囲まれた 2 つのコマンドが続きます ( **'** ) の**j**コマンドと中かっこ ( {} ) の **.if**トークンです。 式が true の場合は、最初のコマンドが実行されます。 この例ではありません最初のコマンドは、コマンドの実行が終了すると、コントロールはデバッガーと共にとどまります。 かっこで囲まれた式が false の場合は、2 番目のコマンドが実行されます。 2 番目のコマンドではほぼ常に、 [ **gc (条件付きブレークポイントから移動)** ](gc--go-from-conditional-breakpoint-.md)コマンド、このコマンドによって、実行、ブレークポイントの前に発生しているのと同じ方法で再開するため(ステップ実行、トレース、または無料の実行) がヒットしました。

ブレークポイントが渡されるたびにメッセージを表示する場合、または最後に達した場合は、単一引用符や中かっこ内の他のコマンドを使用できます。 次に、例を示します。

```dbgcmd
0:000> bp `:143` "j (poi(MyVar)>5) '.echo MyVar Too Big'; '.echo MyVar Acceptable; gc' " 
0:000> bp `:143` ".if (poi(MyVar)>5) {.echo MyVar Too Big} .else {.echo MyVar Acceptable; gc} " 
```

これらのコメントは、デバッガーは、標準が表示されないため、同時に実行されているこのようないくつかのブレークポイントがある場合に特に便利です"ブレークポイント*n*ヒット"メッセージをでコマンド文字列を使用しているときに**bp**コマンド。

### <a name="span-idconditionalbreakpointbasedonstringcomparisonspanspan-idconditionalbreakpointbasedonstringcomparisonspanspan-idconditionalbreakpointbasedonstringcomparisonspanconditional-breakpoint-based-on-string-comparison"></a><span id="Conditional_Breakpoint_Based_on_String_Comparison"></span><span id="conditional_breakpoint_based_on_string_comparison"></span><span id="CONDITIONAL_BREAKPOINT_BASED_ON_STRING_COMPARISON"></span>文字列比較に基づく条件付きブレークポイント

状況によっては、文字列変数パターンに一致する場合にのみ、デバッガーを中断する可能性があります。 たとえば、kernel32 にブレークポイントを設定するとします。CreateEventW 場合にのみ、 *lpName*引数がパターンに一致する文字列を指す"Global\*"。 次の例では、条件付きブレークポイントを作成する方法を示します。

```dbgcmd
bp kernel32!CreateEventW "$$<c:\\commands.txt"
```

上記の[ **bp** ](bp--bu--bm--set-breakpoint-.md)コマンド ベースの条件と commands.txt をという名前のスクリプト ファイル内にある省略可能なコマンドのブレークポイントを作成します。 スクリプト ファイルには、次のステートメントが含まれています。

```dbgcmd
.if (@r9 != 0) { as /mu ${/v:EventName} @r9 } .else { ad /q ${/v:EventName} }
.if ($spat(@"${EventName}", "Global*") == 0)  { gc } .else { .echo EventName }
```

*LpName*に渡される引数、 **CreateEventW** (x64 プロセッサー) r9 レジスタに格納されているために、関数は 4 番目の引数。 スクリプトでは、次の手順を実行します。

1.  場合*lpName*は not NULL を使用して[**として**](as--as--set-alias-.md)と[ **${}**  ](-------alias-interpreter-.md)という名前のエイリアスを作成するにはEventName します。 EventName に、null で終わる Unicode 文字列を開始位置が指すアドレスを割り当てる*lpName*します。 その一方で場合、 *lpName*が null の場合、使用[ **ad** ](ad--delete-alias-.md) EventName という名前の既存の任意のエイリアスを削除します。

2.  使用[ **$spat** ](masm-numbers-and-operators.md)パターン EventName によって表される文字列を比較する"グローバル\*"。 文字列がパターンに一致しない場合は、使用[ **gc** ](gc--go-from-conditional-breakpoint-.md)互換性に影響なしで続行します。 文字列のパターンが一致し、中断、EventName によって表される文字列を表示します。

**注**  [**$spat** ](masm-numbers-and-operators.md)大文字と小文字を実行します。

**注**  (spat(@"${EventName}"specifies that the string represented by EventName is to be interpreted literally; that is, a backslash ( \\ ) $ の文字 @)、アンパサンドがエスケープではなく、円記号として扱われる文字。

### <a name="span-idconditionalbreakpointsandregistersignextensionspanspan-idconditionalbreakpointsandregistersignextensionspanconditional-breakpoints-and-register-sign-extension"></a><span id="conditional_breakpoints_and_register_sign_extension"></span><span id="CONDITIONAL_BREAKPOINTS_AND_REGISTER_SIGN_EXTENSION"></span>条件付きブレークポイントやレジスタの符号拡張

レジスタ値の条件付きブレークポイントを設定できます。

先頭に次のコマンドが中断されます、 **myFunction**関数の場合、 **eax**レジスタが 0xA3 と等しい。

```dbgcmd
0:000> bp mydriver!myFunction "j @eax = 0xa3  '';'gc'" 
0:000> bp mydriver!myFunction ".if @eax = 0xa3  {} .else {gc}"
```

ただし、次のようなコマンドが必ずしも中断されないときに**eax** 0xC0004321 に等しい。

```dbgcmd
0:000> bp mydriver!myFunction "j @eax = 0xc0004321  '';'gc'" 
0:000> bp mydriver!myFunction ".if @eax = 0xc0004321  {} .else {gc}"
```

上記のコマンドは失敗理由は、MASM 式エバリュエーター符号拡張されているレジスタが、高ビットが 1 つです。 ときに**eax** 0xC0004321 の値を持つ 0 xffffffff として扱われます\`--の計算で C0004321 にもかかわらず**eax** 0xC0004321 として引き続き表示されます。 ただし、数字の**0xc0004321**符号拡張は、カーネル モードでは、ユーザー モードではなく。 そのため、上記のコマンドはで正しく動作しないユーザー モードです。 上位ビットをマスクする場合**eax**、カーネル モード - で、コマンドが正しく機能が、それをユーザー モードでは失敗するようになりました。

両方のモードでの符号拡張に対する防御のため、コマンドを作成する必要があります。 上記のコマンドで行うことができますのコマンドは、防御 0x00000000 と組み合わせて使用する AND 演算を使用して、32 ビット レジスタの上位ビットをマスクすることによって\`FFFFFFFF アクサン グラーブ (を含めることによって、数値型定数の上位ビットをマスクすることによって、**\`**  ) その構文内で。

次のコマンドはユーザー モードとカーネル モードで正常に動作します。

```dbgcmd
0:000> bp mydriver!myFunction "j (@eax & 0x0`ffffffff) = 0x0`c0004321  '';'gc'" 
0:000> bp mydriver!myFunction ".if (@eax & 0x0`ffffffff) = 0x0`c0004321  {} .else {gc}"
```

詳細については、デバッガーによって符号拡張が番号については、次を参照してください。[符号拡張](sign-extension.md)します。

### <a name="span-idconditionalbreakpointsinwindbgspanspan-idconditionalbreakpointsinwindbgspanconditional-breakpoints-in-windbg"></a><span id="conditional_breakpoints_in_windbg"></span><span id="CONDITIONAL_BREAKPOINTS_IN_WINDBG"></span>WinDbg で条件付きブレークポイント

WinDbg をクリックして条件付きブレークポイントを作成できます[ブレークポイント](edit---breakpoints.md)から、**編集**に新しいブレークポイント アドレスを入力する メニュー、**コマンド**ボックス、および入力します。条件を**条件**ボックス。

たとえば、入力**mymod! myFunc + 0x3A**に、**コマンド**ボックスと**myVar &lt; 7**に、**条件**ボックスは、次のコマンドを実行に相当します。

```dbgcmd
0:000> bu mymod!myFunc+0x3A "j(myVar<7) '.echo "Breakpoint hit, condition myVar<7"'; 'gc'" 
0:000> bu mymod!myFunc+0x3A ".if(myVar<7) {.echo "Breakpoint hit, condition myVar<7"} .else {gc}" 
```

### <a name="span-idrestrictionsonconditionalbreakpointsspanspan-idrestrictionsonconditionalbreakpointsspanrestrictions-on-conditional-breakpoints"></a><span id="restrictions_on_conditional_breakpoints"></span><span id="RESTRICTIONS_ON_CONDITIONAL_BREAKPOINTS"></span>条件付きブレークポイントに関する制限事項

場合[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)、条件付きブレークポイントを使用することはできませんまたは文字列を他のコマンドのブレークポイントが含まれています、 [ **gc (条件からの移動ブレークポイント)** ](gc--go-from-conditional-breakpoint-.md)または[ **g (移動)** ](g--go-.md)コマンド。 これらのコマンドを使用する場合は、シリアル インターフェイスで、ブレークポイントの回数を対応できないし、CDB を分割することはできません。

 

 





