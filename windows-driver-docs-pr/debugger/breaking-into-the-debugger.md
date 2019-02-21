---
title: デバッガーの中断
description: デバッガーの中断
ms.assetid: 4fec7170-7480-4a8a-b060-1c8a8c3fb9dc
keywords:
- デバッガーの中断
- DebugBreak 関数
- DbgBreakPoint 関数
- KdBreakPoint 関数
- DbgBreakPointWithStatus 関数
- KdBreakPointWithStatus 関数
- ASSERT マクロ
- ASSERTMSG マクロ
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f10e442ea7c18f65d4ddd8330555777618dcbe0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531303"
---
# <a name="breaking-into-the-debugger"></a>デバッガーの中断


## <span id="ddk_breaking_into_the_debugger_dbg"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_DBG"></span>

ユーザー モードとカーネル モード コードでは、異なるルーチンを使用して、デバッガーを中断します。

### <a name="span-idusermodebreakroutinesspanspan-idusermodebreakroutinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>ユーザー モード Break ルーチン

Break ルーチンでは、呼び出し元のスレッドが呼び出し元のプロセスに関連付けられているデバッガーを通知するために、現在のプロセスで発生する例外が発生します。

ユーザー モードのプログラムからデバッガーへの割り込みを使用して、 [DebugBreak 関数](https://msdn.microsoft.com/library/windows/desktop/ms679297(v=vs.85).aspx)します。 

ユーザー モードのプログラムを呼び出すと**DebugBreak**、次の動作が発生します。

1.  ユーザー モード デバッガーがアタッチされている場合、プログラムがデバッガーに中断されます。 これは、プログラムは一時停止し、デバッガーがアクティブになることを意味します。

2.  ユーザー モード デバッガーがアタッチされていない、起動時にカーネル モードのデバッグが有効になっている場合は、コンピューター全体がカーネル デバッガーに中断されます。 カーネル デバッガーがアタッチされていない場合、コンピューターが固定し、カーネル デバッガーを待機します。

3.  ユーザー モードのデバッガーがアタッチされていない、カーネル モードのデバッグが有効になっていない場合は、未処理の例外で、プログラムが終了し、事後 (だけの時間) のデバッガーをアクティブになります。 詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

### <a name="span-idkernelmodebreakroutinesspanspan-idkernelmodebreakroutinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>カーネル モード Break ルーチン

カーネル モードのプログラムは、デバッガーを中断、カーネル デバッガーにより、実行を再開するまでに全体のオペレーティング システムがフリーズします。 カーネル デバッガーが存在しない場合、これはバグ チェックとして扱われます。

**DbgBreakPoint**ルーチンが、カーネル モード コードで動作しますが、それ以外の場合に似ています、 **DebugBreak**ユーザー モードのルーチンです。

**DbgBreakPointWithStatus**も原因休憩がさらに送信、32 ビットの状態コード、デバッガーにします。

**KdBreakPoint**と**KdBreakPointWithStatus**と同じ**DbgBreakPoint**と**DbgBreakPointWithStatus**をそれぞれでコンパイルされた場合、チェック ビルド環境。 無料のビルド環境でコンパイルすると、影響ありません。

ビルド環境と同様に、これらのルーチンの完全なドキュメントについては、Windows Driver Kit を参照してください。

### <a name="span-idkernelmodeconditionalbreakroutinesspanspan-idkernelmodeconditionalbreakroutinesspankernel-mode-conditional-break-routines"></a><span id="kernel_mode_conditional_break_routines"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_ROUTINES"></span>カーネル モードの条件付き改ルーチン

2 つの条件付き改ルーチンでは、カーネル モード コードで使用できます。 これらのルーチンでは、論理式をテストします。 式が false の場合は、実行が停止され、デバッガーがアクティブになります。

**ASSERT**マクロにより、デバッガーをプログラムで失敗した式とその場所を表示します。 **ASSERTMSG**マクロが似ていますが、デバッガーに送信される追加のメッセージを許可します。

**ASSERT**と**ASSERTMSG**はアクティブのチェック ビルド環境でのコンパイル時になります。 無料のビルド環境でコンパイルすると、影響ありません。

ビルド環境と同様に、これらのルーチンの完全なドキュメントについては、Windows Driver Kit を参照してください。

 

 





