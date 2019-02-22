---
title: WinDbg にブレークポイントを設定
description: 設定、表示、および WinDbg を使用してブレークポイントを操作できるいくつかの方法はあります。
ms.assetid: 4A7BE6D2-05AF-4EFB-8F24-C19B1A98217C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cfdeb439a342d0dc328842621dc34f89cd567da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556500"
---
# <a name="setting-breakpoints-in-windbg"></a>WinDbg にブレークポイントを設定


設定、表示、および WinDbg を使用してブレークポイントを操作できるいくつかの方法はあります。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウ


設定、表示、およびデバッガー コマンド ウィンドウでコマンドを入力して、ブレークポイントを操作することができます。 コマンドの一覧は、次を参照してください。[ブレークポイントの制御メソッド](methods-of-controlling-breakpoints.md)します。

## <a name="span-idwindbgmenuspanspan-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg のメニュー


開くことができます、**ブレークポイント** ダイアログ ボックスを選択して**ブレークポイント**から、**編集**メニューまたは ALT + F9 キーを押しています。 このダイアログ ボックスは、すべてのブレークポイントを示し、無効化、有効にする、または既存のブレークポイントをクリアするか、新しいブレークポイントを設定するに使用することができます。

## <a name="span-idcodewindowsspanspan-idcodewindowsspanspan-idcodewindowsspancode-windows"></a><span id="Code_Windows"></span><span id="code_windows"></span><span id="CODE_WINDOWS"></span>コードの Windows


逆アセンブル ウィンドウとソース ウィンドウには、設定されたブレークポイントの行が強調表示します。 ブレークポイントが有効では、赤、および無効になっているブレークポイントが黄色です。

逆アセンブル ウィンドウで、またはソース ウィンドウ内の特定の行にカーソルを設定した場合は、その行にブレークポイントを設定して f9 キーを押すことができます。

 

 





