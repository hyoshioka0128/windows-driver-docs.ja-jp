---
title: エンジンの操作
description: エンジンの操作
ms.assetid: 80f5320f-ed34-4839-a16e-b3ff5d8edbfe
keywords:
- デバッガー エンジン API を使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3bd91da45431dca72433f3b9b12c8f5f338d90e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361319"
---
# <a name="interacting-with-the-engine"></a>エンジンの操作


### <a name="span-idcommandsandexpressionsspanspan-idcommandsandexpressionsspancommands-and-expressions"></a><span id="commands_and_expressions"></span><span id="COMMANDS_AND_EXPRESSIONS"></span>コマンドと式

デバッガー エンジン API は、コマンドを実行し、WinDbg に型指定されたように、式の評価のメソッドを提供します。[デバッガー コマンド ウィンドウ](the-debugger-command-window.md)します。 デバッガー コマンドを実行するには使用[ **Execute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-execute)します。 または、ファイルでは、すべてのコマンドを実行を使用して[ **ExecuteCommandFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-executecommandfile)します。

メソッド[ **Evaluate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-evaluate) C++ または MASM の構文を使用して式を評価します。 などの--式を評価するデバッガー エンジンによって使用される構文、 **Evaluate**メソッド--がで指定された[ **GetExpressionSyntax** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexpressionsyntax) を使用して変更できます[**SetExpressionSyntaxByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexpressionsyntaxbyname)と[ **SetExpressionSyntax**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexpressionsyntax)します。 デバッガーによって認識される構文の数がによって返される[ **GetNumberExpressionSyntaxes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberexpressionsyntaxes)、その名前がによって返されると[ **GetExpressionSyntaxNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexpressionsyntaxnames)します。

によって返される値の型**Evaluate**シンボルと評価された文字列で使用される定数によって決定されます。 値が含まれている、 [**デバッグ\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_value)構造体し、を使用して別の型にキャストできる[ **CoerceValue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-coercevalue)[ **CoerceValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-coercevalues)します。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>エイリアス

*エイリアス*は他のデバッガー コマンドと式で使用する場合は、文字の文字列に自動的に置き換え、文字の文字列。 エイリアスの概要については、次を参照してください。 [Using エイリアス](using-aliases.md)します。 デバッガー エンジンでは、エイリアスのいくつかのクラスがあります。

*固定名のエイリアス*番号でインデックスが作成され、名前を持つ**ドル u0**、 **$u1**,...,**ドル u9**します。 使用して、これらの別名の値を設定することができます、 [ **SetTextMacro** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-settextmacro)メソッドを使用して取得できると[ **GetTextMacro** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-gettextmacro)メソッド。

*自動エイリアス*と*という名前のユーザーのエイリアス*任意の名前を持つことができます。 自動のエイリアスはデバッガー エンジンによって定義され、ユーザーのデバッガー コマンドまたはデバッガー エンジン API を実行してという名前のユーザーのエイリアスが定義されています。 を定義またはという名前のユーザーのエイリアスを削除するには使用、 [ **SetTextReplacement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-settextreplacement)メソッド。 [ **GetTextReplacement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-gettextreplacement)メソッド名と自動のエイリアスまたはという名前のユーザーの別名の値を返します。 使用してという名前のユーザーのすべてのエイリアスを削除することができます、 [ **RemoveTextReplacements** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removetextreplacements)メソッド。 [ **GetNumberTextReplacements** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumbertextreplacements)メソッドでは、ユーザー名と自動の別名の数を返しますこれは、で使用できる**GetTextReplacement**をすべて反復処理する。これらの別名。 [ **OutputTextReplacements** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputtextreplacements)メソッドがすべてという名前のユーザーのエイリアスなどの名前と値の一覧に表示されます。

**注**  という名前のユーザーのエイリアスが自動のエイリアスを非表示という名前のユーザーのエイリアスが自動的にエイリアスと同じ名前を指定した場合という名前のユーザーのエイリアスが使用される名前でエイリアスの値を取得するときにできるようにします。

 

### <a name="span-idengineoptionsspanspan-idengineoptionsspanengine-options"></a><span id="engine_options"></span><span id="ENGINE_OPTIONS"></span>エンジンのオプション

エンジンでは、さまざまな動作を制御するオプションがあります。 これらのオプションは、「 [**デバッグ\_ENGOPT\_XXX**](https://docs.microsoft.com/previous-versions/ff541475(v=vs.85))します。 によって返される[ **GetEngineOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getengineoptions)を使用して設定できる[ **SetEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setengineoptions)します。 使用して個々 のオプションを設定できる[ **AddEngineOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-addengineoptions)設定解除を使用して、 [ **RemoveEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removeengineoptions)します。

### <a name="span-idinterruptsspanspan-idinterruptsspaninterrupts"></a><span id="interrupts"></span><span id="INTERRUPTS"></span>割り込み

割り込みは、デバッガーにブレークを実行したり、WinDbg で ctrl キーを押しながら Break キーを押して現在コマンドの処理を停止するエンジンに通知する手段です。

デバッガーにブレークを要求する、またはデバッガーの現在のタスクを中断するを使用して、 [ **SetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setinterrupt)します。 確認するには、割り込みがあったがかどうかを使用して、 [ **GetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getinterrupt)します。

**注**  デバッガー拡張機能からの時間のかかるタスクを実行する場合は、拡張機能を確認することをお勧め**GetInterrupt**定期的に割り込みが要求されている場合の処理を停止するとします。

 

デバッガーに中断を要求すると、エンジンは、侵入を実行する対象の時間がかかる場合に、タイムアウトが可能性があります。 これは、ターゲットが応答しない状態の場合、または侵入要求がブロックされているか、リソースの競合で遅延が発生した場合に発生することができます。 エンジンが待機する時間の長さがによって返される[ **GetInterruptTimeout** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getinterrupttimeout)を使用して設定できる[ **SetInterruptTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setinterrupttimeout)します。

 

 





