---
title: WinDbg を使用してダンプ ファイルを開く
description: ダンプ ファイルを開く WinDbg を使用するいくつかの方法はあります。
ms.assetid: DE2EABE7-2B7A-4DF9-82FD-EF19D69E31A7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45306cc5c78042d70bcf803ebe61abccdea0c8d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570272"
---
# <a name="opening-a-dump-file-using-windbg"></a>WinDbg を使用してダンプ ファイルを開く


ダンプ ファイルを開く WinDbg を使用するいくつかの方法はあります。

### <a name="span-idwindbgmenuspanspan-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg のメニュー

選択して、ダンプを開くことができる場合、WinDbg が既に実行中、休止モード、**クラッシュ ダンプを開く**から、**ファイル**メニューまたは CTRL キーを押しながら D キーを押しています。 クラッシュ ダンプを開く ダイアログ ボックスが表示されたら、クラッシュ ダンプ ファイルの名前と完全なパスを入力してください。、**ファイル名**ボックス、またはダイアログ ボックスを使用して、適切なパスとファイル名を選択します。 適切なファイルを選択すると、クリックして**オープン**します。

### <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>コマンド プロンプト

コマンド プロンプト ウィンドウでは、WinDbg を起動するときにダンプ ファイルを開くことができます。 次のコマンドを使用します。

**windbg -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**オプション (詳細モード) も便利です。 コマンドライン構文の詳細については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。

### <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウ

WinDbg がカーネル モードのデバッグ セッションに既にある場合を使用して、ダンプ ファイルを開くことができます、 [ **.opendump (ダンプ ファイルを開く)** ](-opendump--open-dump-file-.md)コマンドの後に[ **g (移動)**](g--go-.md).

 

 





