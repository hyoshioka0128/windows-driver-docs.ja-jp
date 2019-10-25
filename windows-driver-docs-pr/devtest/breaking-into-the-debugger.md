---
title: デバッガーへの割り込み
description: デバッガーへの割り込み
ms.assetid: c52c99a2-5db0-49e8-88a7-db075a32c26b
keywords:
- ドライバーのデバッグ WDK、デバッガーの中断
- デバッガーの WDK への侵入
- ユーザーモード中断ルーチン WDK
- カーネルモード中断ルーチン WDK
- 中断ルーチン WDK
- 条件付きブレークマクロ WDK
- 中断マクロ WDK
- ルーチン WDK デバッグ、中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce967354be111c6aa76844c4027375eae676b891
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839579"
---
# <a name="breaking-into-the-debugger"></a>デバッガーへの割り込み


## <span id="ddk_breaking_into_the_debugger_tools"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_TOOLS"></span>


ユーザーモードとカーネルモードのドライバーは、デバッガーを中断するためにさまざまなルーチンを使用します。

### <a name="span-iduser_mode_break_routinesspanspan-iduser_mode_break_routinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>ユーザーモードの中断ルーチン

中断ルーチンは、現在のプロセスで例外を発生させます。これにより、呼び出し元のスレッドが呼び出し元のプロセスに関連付けられたデバッガーに通知できるようになります。

ユーザーモードプログラムからデバッガーを中断するには、 **DebugBreak**ルーチンを使用します。 プロトタイプは次のとおりです。

```
VOID DebugBreak(VOID);
```

このルーチンは、windows .h ヘッダーを含むユーザーモードドライバーによって呼び出すことができます。 このルーチンと、デバッグに役立つその他のユーザーモードルーチンの完全なドキュメントについては、Microsoft Windows SDK を参照してください。

ユーザーモードプログラムが**DebugBreak**を呼び出すと、次の操作が実行されます。

1.  ユーザーモードのデバッガーがアタッチされている場合、プログラムはデバッガーを中断します。 これは、プログラムが一時停止し、デバッガーがアクティブになることを意味します。

2.  ユーザーモードのデバッガーがアタッチされていないが、起動時にカーネルモードのデバッグが有効になっている場合、コンピューター全体がカーネルデバッガーに侵入します。 カーネルデバッガーがアタッチされていない場合、コンピューターはカーネルデバッガーをフリーズし、待機します。

3.  ユーザーモードのデバッガーがアタッチされておらず、カーネルモードのデバッグが有効になっていない場合、プログラムはハンドルされない例外で終了し、事後分析 (ジャストインタイム) デバッガーがアクティブ化されます。 既定では、事後分析デバッガーはワトソン博士です。これにより、クラッシュダンプファイルが作成され、このクラッシュダンプファイルを Microsoft に送信するかどうかを確認するメッセージが表示されます。

### <a name="span-idkernel_mode_break_routinesspanspan-idkernel_mode_break_routinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>カーネルモードの中断ルーチン

カーネルモードプログラムがデバッガーに侵入すると、カーネルデバッガーが実行を再開できるまで、オペレーティングシステム全体がフリーズします。 カーネルデバッガーが存在しない場合、これはバグチェックとして扱われます。

[**Dbgbreakpoint ポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)ルーチンは、カーネルモードコードで動作しますが、それ以外の場合は**DebugBreak**ユーザーモードルーチンに似ています。

また、 [**Dbgbreakpointwithstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)ルーチンでも break が発生しますが、さらに、32ビットのステータスコードがデバッガーに送信されます。

[**KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))ルーチンと[**KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)ルーチンは、チェックされたビルド環境でコンパイルされると、それぞれ**Dbgbreakpoint ポイント**と**dbgbreakpointwithstatus**と同じです。 無料のビルド環境でコンパイルした場合、影響はありません。

### <a name="span-idkernel_mode_conditional_break_macrosspanspan-idkernel_mode_conditional_break_macrosspankernel-mode-conditional-break-macros"></a><span id="kernel_mode_conditional_break_macros"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_MACROS"></span>カーネルモードの条件付き中断マクロ

カーネルモードドライバーでは、次の2つの条件付きブレークマクロを使用できます。

-   [**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))マクロは、論理式をテストします。 式が false の場合、実行が停止し、デバッガーがアクティブになります。 失敗した式とプログラム内のその位置がデバッガーに表示されます。

-   [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)マクロは、追加のメッセージをデバッガーに送信することを許可する点を除いて、 **ASSERT**と同じです。

**ASSERT**と**ASSERTMSG**は、チェックされたビルド環境でコンパイルした場合にのみアクティブになります。 無料のビルド環境でコンパイルした場合、影響はありません。

 

 





