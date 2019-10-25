---
title: エンジンの操作
description: エンジンの操作
ms.assetid: 80f5320f-ed34-4839-a16e-b3ff5d8edbfe
keywords:
- デバッガーエンジン API, 使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9e78d21cf3656f2b63c468a7c2b96a6f65c4934
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826389"
---
# <a name="interacting-with-the-engine"></a>エンジンの操作


### <a name="span-idcommands_and_expressionsspanspan-idcommands_and_expressionsspancommands-and-expressions"></a><span id="commands_and_expressions"></span><span id="COMMANDS_AND_EXPRESSIONS"></span>コマンドと式

デバッガーエンジン API は、WinDbg の[デバッガーコマンドウィンドウ](the-debugger-command-window.md)に入力されているような、コマンドを実行し、式を評価するメソッドを提供します。 デバッガーコマンドを実行するには、 [**execute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-execute)を使用します。 または、ファイル内のすべてのコマンドを実行するには、 [**ExecuteCommandFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-executecommandfile)を使用します。

メソッドの[**評価**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-evaluate)では、 C++または MASM 構文を使用して式を評価します。 **評価**メソッドなどで式を評価するためにデバッガーエンジンによって使用される構文は、 [**get式構文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexpressionsyntax)によって指定され、 [**SetExpressionSyntaxByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexpressionsyntaxbyname)と[**set 構文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexpressionsyntax)を使用して変更できます。 デバッガーによって認識されるさまざまな構文の数は、 [**Getnumber 式の構文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumberexpressionsyntaxes)によって返され、その名前は[**GetExpressionSyntaxNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexpressionsyntaxnames)によって返されます。

**Evaluate**によって返される値の型は、評価された文字列で使用されている記号と定数によって決まります。 値は、[**デバッグ\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_value)の構造体に含まれており、 [**CoerceValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-coercevalue)と[**CoerceValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-coercevalues)を使用して異なる型にキャストできます。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>エイリアス

*エイリアス*は、デバッガーのコマンドや式で使用される場合に、自動的に他の文字列に置き換えられる文字列です。 エイリアスの概要については、「 [Using alias](using-aliases.md)」を参照してください。 デバッガーエンジンには、いくつかのエイリアスのクラスがあります。

*固定名のエイリアス*は数値でインデックスが付けられ、名前は **$u 0**、 **$u 1**、...、 **$u 9**になります。 これらのエイリアスの値は、 [**Settextmacro**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-settextmacro)メソッドを使用して設定でき、 [**GetTextMacro**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-gettextmacro)メソッドを使用して取得できます。

*自動エイリアス*とユーザー名の*エイリアス*には任意の名前を付けることができます。 自動エイリアスはデバッガーエンジンによって定義され、ユーザー名のエイリアスはデバッガーコマンドまたはデバッガーエンジン API を使用してユーザーが定義します。 ユーザー名のエイリアスを定義または削除するには、 [**Settextreplacement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-settextreplacement)メソッドを使用します。 [**GetTextReplacement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-gettextreplacement)メソッドは、自動エイリアスまたはユーザー名のエイリアスの名前と値を返します。 すべてのユーザー名のエイリアスは、 [**Removetextreplacements**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removetextreplacements)メソッドを使用して削除できます。 [**Getnumber text置換**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumbertextreplacements)メソッドは、ユーザー名と自動エイリアスの数を返します。これを**GetTextReplacement**と共に使用して、これらすべてのエイリアスを反復処理できます。 [**Outputtextreplacements**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputtextreplacements)メソッドは、名前と値を含む、すべてのユーザー名付きエイリアスの一覧を出力します。

**注**   ユーザー名のエイリアスに自動エイリアスと同じ名前が指定されている場合、エイリアスの値を名前で取得するときに、ユーザー名の別名が使用されるように、ユーザー名のエイリアスによって自動エイリアスが非表示になります。

 

### <a name="span-idengine_optionsspanspan-idengine_optionsspanengine-options"></a><span id="engine_options"></span><span id="ENGINE_OPTIONS"></span>エンジンのオプション

エンジンには、その動作を制御するさまざまなオプションがあります。 これらのオプションは、 [**DEBUG\_ENGOPT\_XXX**](https://docs.microsoft.com/previous-versions/ff541475(v=vs.85))に記載されています。 これらは[**GetEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getengineoptions)によって返され、 [**SetEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setengineoptions)を使用して設定できます。 個々のオプションは、 [**AddEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-addengineoptions)を使用して設定し、 [**RemoveEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removeengineoptions)を使用して設定を解除することができます。

### <a name="span-idinterruptsspanspan-idinterruptsspaninterrupts"></a><span id="interrupts"></span><span id="INTERRUPTS"></span>中断

割り込みは、デバッガーを強制的に中断したり、現在のコマンドの処理を停止するようにエンジンに指示したりする方法です。たとえば、WinDbg で Ctrl + Break キーを押すことができます。

デバッガーの中断を要求したり、デバッガーの現在のタスクを中断したりするには、 [**Setinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setinterrupt)を使用します。 割り込みが発生したかどうかを確認するには、 [**Getinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getinterrupt)を使用します。

**注**   デバッガー拡張機能から長いタスクを実行する場合は、 **getinterrupt**を定期的にチェックし、割り込みが要求された場合に処理を停止することをお勧めします。

 

デバッガーの中断を要求するときに、エンジンは、ターゲットがブレークインを実行するのに時間がかかりすぎるとタイムアウトする場合があります。 これは、ターゲットが応答していない状態の場合、または中断要求がリソース競合によってブロックまたは遅延された場合に発生する可能性があります。 エンジンが待機する時間の長さは[**GetInterruptTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getinterrupttimeout)によって返され、 [**SetInterruptTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setinterrupttimeout)を使用して設定できます。

 

 





