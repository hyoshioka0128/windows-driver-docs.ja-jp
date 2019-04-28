---
title: エンジンの操作
description: エンジンの操作
ms.assetid: 80f5320f-ed34-4839-a16e-b3ff5d8edbfe
keywords:
- デバッガー エンジン API を使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c24df40a70030dfed450ba60a37f98a58f48928
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376830"
---
# <a name="interacting-with-the-engine"></a>エンジンの操作


### <a name="span-idcommandsandexpressionsspanspan-idcommandsandexpressionsspancommands-and-expressions"></a><span id="commands_and_expressions"></span><span id="COMMANDS_AND_EXPRESSIONS"></span>コマンドと式

デバッガー エンジン API は、コマンドを実行し、WinDbg に型指定されたように、式の評価のメソッドを提供します。[デバッガー コマンド ウィンドウ](the-debugger-command-window.md)します。 デバッガー コマンドを実行するには使用[ **Execute**](https://msdn.microsoft.com/library/windows/hardware/ff543208)します。 または、ファイルでは、すべてのコマンドを実行を使用して[ **ExecuteCommandFile**](https://msdn.microsoft.com/library/windows/hardware/ff543215)します。

メソッド[ **Evaluate** ](https://msdn.microsoft.com/library/windows/hardware/ff543046) C++ または MASM の構文を使用して式を評価します。 などの--式を評価するデバッガー エンジンによって使用される構文、 **Evaluate**メソッド--がで指定された[ **GetExpressionSyntax** ](https://msdn.microsoft.com/library/windows/hardware/ff546701) を使用して変更できます[**SetExpressionSyntaxByName** ](https://msdn.microsoft.com/library/windows/hardware/ff556697)と[ **SetExpressionSyntax**](https://msdn.microsoft.com/library/windows/hardware/ff556696)します。 デバッガーによって認識される構文の数がによって返される[ **GetNumberExpressionSyntaxes**](https://msdn.microsoft.com/library/windows/hardware/ff547913)、その名前がによって返されると[ **GetExpressionSyntaxNames**](https://msdn.microsoft.com/library/windows/hardware/ff546708)します。

によって返される値の型**Evaluate**シンボルと評価された文字列で使用される定数によって決定されます。 値が含まれている、 [**デバッグ\_値**](https://msdn.microsoft.com/library/windows/hardware/ff541719)構造体し、を使用して別の型にキャストできる[ **CoerceValue** ](https://msdn.microsoft.com/library/windows/hardware/ff539158)[ **CoerceValues**](https://msdn.microsoft.com/library/windows/hardware/ff539162)します。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>エイリアス

*エイリアス*は他のデバッガー コマンドと式で使用する場合は、文字の文字列に自動的に置き換え、文字の文字列。 エイリアスの概要については、次を参照してください。 [Using エイリアス](using-aliases.md)します。 デバッガー エンジンでは、エイリアスのいくつかのクラスがあります。

*固定名のエイリアス*番号でインデックスが作成され、名前を持つ**ドル u0**、 **$u1**,...,**ドル u9**します。 使用して、これらの別名の値を設定することができます、 [ **SetTextMacro** ](https://msdn.microsoft.com/library/windows/hardware/ff556809)メソッドを使用して取得できると[ **GetTextMacro** ](https://msdn.microsoft.com/library/windows/hardware/ff549270)メソッド。

*自動エイリアス*と*という名前のユーザーのエイリアス*任意の名前を持つことができます。 自動のエイリアスはデバッガー エンジンによって定義され、ユーザーのデバッガー コマンドまたはデバッガー エンジン API を実行してという名前のユーザーのエイリアスが定義されています。 を定義またはという名前のユーザーのエイリアスを削除するには使用、 [ **SetTextReplacement** ](https://msdn.microsoft.com/library/windows/hardware/ff556818)メソッド。 [ **GetTextReplacement** ](https://msdn.microsoft.com/library/windows/hardware/ff549280)メソッド名と自動のエイリアスまたはという名前のユーザーの別名の値を返します。 使用してという名前のユーザーのすべてのエイリアスを削除することができます、 [ **RemoveTextReplacements** ](https://msdn.microsoft.com/library/windows/hardware/ff554548)メソッド。 [ **GetNumberTextReplacements** ](https://msdn.microsoft.com/library/windows/hardware/ff547988)メソッドでは、ユーザー名と自動の別名の数を返しますこれは、で使用できる**GetTextReplacement**をすべて反復処理する。これらの別名。 [ **OutputTextReplacements** ](https://msdn.microsoft.com/library/windows/hardware/ff553268)メソッドがすべてという名前のユーザーのエイリアスなどの名前と値の一覧に表示されます。

**注**  という名前のユーザーのエイリアスが自動のエイリアスを非表示という名前のユーザーのエイリアスが自動的にエイリアスと同じ名前を指定した場合という名前のユーザーのエイリアスが使用される名前でエイリアスの値を取得するときにできるようにします。

 

### <a name="span-idengineoptionsspanspan-idengineoptionsspanengine-options"></a><span id="engine_options"></span><span id="ENGINE_OPTIONS"></span>エンジンのオプション

エンジンでは、さまざまな動作を制御するオプションがあります。 これらのオプションは、「 [**デバッグ\_ENGOPT\_XXX**](https://msdn.microsoft.com/library/windows/hardware/ff541475)します。 によって返される[ **GetEngineOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff546598)を使用して設定できる[ **SetEngineOptions**](https://msdn.microsoft.com/library/windows/hardware/ff556670)します。 使用して個々 のオプションを設定できる[ **AddEngineOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff537884)設定解除を使用して、 [ **RemoveEngineOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554491)します。

### <a name="span-idinterruptsspanspan-idinterruptsspaninterrupts"></a><span id="interrupts"></span><span id="INTERRUPTS"></span>割り込み

割り込みは、デバッガーにブレークを実行したり、WinDbg で ctrl キーを押しながら Break キーを押して現在コマンドの処理を停止するエンジンに通知する手段です。

デバッガーにブレークを要求する、またはデバッガーの現在のタスクを中断するを使用して、 [ **SetInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff556722)します。 確認するには、割り込みがあったがかどうかを使用して、 [ **GetInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff546944)します。

**注**  デバッガー拡張機能からの時間のかかるタスクを実行する場合は、拡張機能を確認することをお勧め**GetInterrupt**定期的に割り込みが要求されている場合の処理を停止するとします。

 

デバッガーに中断を要求すると、エンジンは、侵入を実行する対象の時間がかかる場合に、タイムアウトが可能性があります。 これは、ターゲットが応答しない状態の場合、または侵入要求がブロックされているか、リソースの競合で遅延が発生した場合に発生することができます。 エンジンが待機する時間の長さがによって返される[ **GetInterruptTimeout** ](https://msdn.microsoft.com/library/windows/hardware/ff546955)を使用して設定できる[ **SetInterruptTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff556725)します。

 

 





