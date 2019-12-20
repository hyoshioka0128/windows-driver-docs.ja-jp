---
title: デバッガーへの割り込み
description: デバッガーへの割り込み
ms.assetid: 4fec7170-7480-4a8a-b060-1c8a8c3fb9dc
keywords:
- デバッガーの中断
- DebugBreak 関数
- DbgBreakPoint ポイント関数
- KdBreakPoint 関数
- DbgBreakPointWithStatus 関数
- KdBreakPointWithStatus 関数
- ASSERT マクロ
- ASSERTMSG マクロ
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbeeec83d71201a4c58be5d507477d2c72b32b45
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209094"
---
# <a name="breaking-into-the-debugger"></a>デバッガーへの割り込み


## <span id="ddk_breaking_into_the_debugger_dbg"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_DBG"></span>

ユーザーモードとカーネルモードのコードでは、さまざまなルーチンを使用してデバッガーを中断します。

### <a name="span-iduser_mode_break_routinesspanspan-iduser_mode_break_routinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>ユーザーモードの中断ルーチン

中断ルーチンは、現在のプロセスで例外を発生させます。これにより、呼び出し元のスレッドが呼び出し元のプロセスに関連付けられたデバッガーに通知できるようになります。

ユーザーモードプログラムからデバッガーを中断するには、 [DebugBreak 関数](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-debugbreak)を使用します。 

ユーザーモードプログラムが**DebugBreak**を呼び出すと、次の操作が実行されます。

1.  ユーザーモードのデバッガーがアタッチされている場合、プログラムはデバッガーを中断します。 これは、プログラムが一時停止し、デバッガーがアクティブになることを意味します。

2.  ユーザーモードのデバッガーがアタッチされていない場合でも、起動時にカーネルモードのデバッグが有効になっていると、コンピューター全体がカーネルデバッガーに侵入します。 カーネルデバッガーがアタッチされていない場合、コンピューターはカーネルデバッガーをフリーズし、待機します。

3.  ユーザーモードのデバッガーがアタッチされておらず、カーネルモードのデバッグが有効になっていない場合、プログラムはハンドルされない例外で終了し、事後分析 (ジャストインタイム) デバッガーがアクティブ化されます。 詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。

### <a name="span-idkernel_mode_break_routinesspanspan-idkernel_mode_break_routinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>カーネルモードの中断ルーチン

カーネルモードプログラムがデバッガーに侵入すると、カーネルデバッガーが実行を再開できるまで、オペレーティングシステム全体がフリーズします。 カーネルデバッガーが存在しない場合、これはバグチェックとして扱われます。

**Dbgbreakpoint ポイント**ルーチンは、カーネルモードコードで動作しますが、それ以外の場合は**DebugBreak**ユーザーモードルーチンに似ています。

**Dbgbreakpointwithstatus**も break を発生させますが、さらに、32ビット状態コードをデバッガーに送信します。

**KdBreakPoint**と**KdBreakPointWithStatus**は、チェックされたビルド環境でコンパイルされると、それぞれ**Dbgbreakpoint ポイント**と**dbgbreakpointwithstatus**と同じです。 無料のビルド環境でコンパイルした場合、影響はありません。

### <a name="span-idkernel_mode_conditional_break_routinesspanspan-idkernel_mode_conditional_break_routinesspankernel-mode-conditional-break-routines"></a><span id="kernel_mode_conditional_break_routines"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_ROUTINES"></span>カーネルモードの条件付き中断ルーチン

カーネルモードのコードでは、2つの条件付きブレークルーチンを使用できます。 これらのルーチンは、論理式をテストします。 式が false の場合、実行が停止し、デバッガーがアクティブになります。

**ASSERT**マクロを指定すると、デバッガーによって、失敗した式とプログラム内のその位置が表示されます。 **ASSERTMSG**マクロは似ていますが、追加のメッセージをデバッガーに送信することができます。

**ASSERT**と**ASSERTMSG**は、チェックされたビルド環境でコンパイルした場合にのみアクティブになります。 無料のビルド環境でコンパイルした場合、影響はありません。

これらのルーチンおよびビルド環境の完全なドキュメントについては、「Windows Driver Kit」を参照してください。

 

 





