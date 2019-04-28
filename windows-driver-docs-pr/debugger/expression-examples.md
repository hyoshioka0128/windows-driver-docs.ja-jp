---
title: 式の例
description: 式の例
ms.assetid: a4915678-a83f-48f1-8b29-50cf530f9246
keywords:
- 式では、例
- 例の MASM 式
- C++ の式の例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed6c9a91302443231dfda10146aee8c4e9fba2f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379742"
---
# <a name="expression-examples"></a>式の例


## <span id="ddk_expression_examples_dbg"></span><span id="DDK_EXPRESSION_EXAMPLES_DBG"></span>


このトピックには、さまざまなコマンドで使用される、MASM および C++ の式の例が含まれています。

このヘルプ ドキュメントの他のすべてのセクションは、(ない場合に限る) の例は、の MASM 式の構文を使用します。 C++ 式の構文は構造体と、変数を操作するのに便利ですが、非常にうまくデバッガー コマンドのパラメーターを解析ことはできません。

一般的な目的のデバッガー コマンドを使用してまたはデバッガーの拡張機能を使用する場合は、既定の構文として MASM 式の構文を設定してください。 C++ 式の構文を使用する特定のパラメーターが必要な場合は、使用、 **@ ()** 構文。

### <a name="span-idconditionalbreakpointsspanspan-idconditionalbreakpointsspanconditional-breakpoints"></a><span id="conditional_breakpoints"></span><span id="CONDITIONAL_BREAKPOINTS"></span>条件付きブレークポイント

比較演算子を使用するには作成する[条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。 次のコード例では、MASM 式の構文を使用します。 この例では、現在の既定の基数は 16 であるため、 **0n**プレフィックス数 20 は、10 進数と考えるようにします。

```dbgcmd
0:000> bp MyFunction+0x43 "j ( poi(MyVar)>0n20 ) ''; 'gc' " 
```

前の例では、 **MyVar**は C ソース内の整数です。 例では、必要があります、MASM パーサーでは、すべてのシンボルを扱うアドレスとして、ため、 **poi**を逆参照演算子**MyVar**します。

### <a name="span-idconditionalexpressionsspanspan-idconditionalexpressionsspanconditional-expressions"></a><span id="conditional_expressions"></span><span id="CONDITIONAL_EXPRESSIONS"></span>条件式

次の例の値を出力する**ecx**場合**eax**がより大きい**ebx**, 7 場合**eax**がより小さい**ebx**、3 つの場合**eax** equals **ebx**します。 この例は、ので、等号 (=) 比較演算子、代入演算子ではなく、MASM 式エバリュエーターを使用します。

```dbgcmd
0:000> ? ecx*(eax>ebx) + 7*(eax<ebx) + 3*(eax=ebx) 
```

C++ 構文では、 **@** 記号がレジスタを示します、二重の等号 (= =) は、比較演算子、およびコードは、BOOL から明示的にキャストする必要があります**int**します。そのため、C++ 構文では前のコマンドは、次のなります。

```dbgcmd
0:000> ?? @ecx*(int)(@eax>@ebx) + 7*(int)(@eax<@ebx) + 3*(int)(@eax==@ebx) 
```

### <a name="span-idcexpressionexamplesspanspan-idcexpressionexamplesspanc-expression-examples"></a><span id="c___expression_examples"></span><span id="C___EXPRESSION_EXAMPLES"></span>C++ 式の例

場合**myInt** ULONG32 値は、次の 2 つの例の値を表示する MASM 式エバリュエーターを使用している場合**MyInt**します。

```dbgcmd
0:000> ?? myInt 
0:000> dd myInt L1 
```

ただし、次の例を示しています、*アドレス*の**myInt**します。

```dbgcmd
0:000> ? myInt 
```

### <a name="span-idmixedexpressionexamplesspanspan-idmixedexpressionexamplesspanmixed-expression-examples"></a><span id="mixed_expression_examples"></span><span id="MIXED_EXPRESSION_EXAMPLES"></span>混合式の例

C++ の式でソース行の式を使用することはできません。 次の例では、 **@ ()** C++ の式内の MASM 式の入れ子にする構文。 この例では設定**MyPtr** Myfile.c ファイルの 43 行のアドレスと一致しません。

```dbgcmd
0:000> ?? MyPtr = @@( `myfile.c:43` )
```

次の例では、既定の式エバリュエーターを MASM に設定し、評価*Expression2*として C++ の式を評価および*Expression1*と*Expression3*として MASM 式。

```dbgcmd
0:000> .expr /s masm 
0:000> bp Expression1 + @@( Expression2 ) + Expression3 
```

場合**myInt** ULONG64 値は、別 ULONG64 によってメモリ内でこの値の後にする場合は、ブレークポイントを設定できます、アクセスその場所で次の例のいずれかを使用します。 (ポインターの算術演算の使用に注意してください)。

```dbgcmd
0:000> ba r8 @@( &myInt + 1 ) 
0:000> ba r8 myInt + 8 
```

### <a name="span-idstructuresspanspan-idstructuresspanstructures"></a><span id="structures"></span><span id="STRUCTURES"></span>構造体

C++ の式エバリュエーターは、擬似レジスタ、適切な型にキャストします。 たとえば、 **$teb** 、TEB としてキャスト\*します。 次の例は、プロセス ID を表示します。

```dbgcmd
kd> ??  @$teb->ClientId.UniqueProcess 
```

 

 





