---
title: デバッガーへの割り込み
description: デバッガーへの割り込み
ms.assetid: c52c99a2-5db0-49e8-88a7-db075a32c26b
keywords:
- ドライバー WDK、デバッガーの中断のデバッグ
- WDK のデバッガーの中断
- ユーザー モード break ルーチン WDK
- カーネル モード break ルーチン WDK
- WDK のルーチンを中断します。
- WDK の条件付き改マクロ
- WDK のマクロを中断します。
- ルーチン WDK のデバッグ、break
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fefba27951f5283ece14799bba7d4bfb816b9d84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371652"
---
# <a name="breaking-into-the-debugger"></a>デバッガーへの割り込み


## <span id="ddk_breaking_into_the_debugger_tools"></span><span id="DDK_BREAKING_INTO_THE_DEBUGGER_TOOLS"></span>


ユーザー モードとカーネル モード ドライバーでは、異なるルーチンを使用して、デバッガーを中断します。

### <a name="span-idusermodebreakroutinesspanspan-idusermodebreakroutinesspanuser-mode-break-routines"></a><span id="user_mode_break_routines"></span><span id="USER_MODE_BREAK_ROUTINES"></span>ユーザー モード Break ルーチン

Break ルーチンでは、呼び出し元のスレッドが呼び出し元のプロセスに関連付けられているデバッガーを通知するために、現在のプロセスで発生する例外が発生します。

ユーザー モードのプログラムからデバッガーへの割り込みを使用して、 **DebugBreak**ルーチン。 そのプロトタイプは次のとおりです。

```
VOID DebugBreak(VOID);
```

このルーチンは、windows.h のヘッダーを含む任意のユーザー モード ドライバーによって呼び出すことができます。 このルーチンとその他のユーザー モード ルーチンのデバッグに役立つ詳細なドキュメントについては、Microsoft Windows SDK を参照してください。

ユーザー モードのプログラムを呼び出すと**DebugBreak**、次の動作が発生します。

1.  ユーザー モード デバッガーがアタッチされている場合、プログラムがデバッガーに中断されます。 これは、プログラムは一時停止し、デバッガーがアクティブになることを意味します。

2.  ユーザー モード デバッガーがアタッチされていない、起動時にカーネル モードのデバッグが有効になっている場合は、コンピューター全体がカーネル デバッガーに中断されます。 カーネル デバッガーがアタッチされていない場合、コンピューターが固定し、カーネル デバッガーを待機します。

3.  ユーザー モード デバッガーがアタッチされていません、カーネル モードのデバッグが有効になっていない場合は、未処理の例外で、プログラムが終了し、事後 (だけの時間) のデバッガーをアクティブになります。 既定では、事後分析のデバッガーは、Dr が。ワトソン クラッシュ ダンプ ファイルが作成され、要求するクラッシュ ダンプ ファイルを Microsoft に送信するかどうか。

### <a name="span-idkernelmodebreakroutinesspanspan-idkernelmodebreakroutinesspankernel-mode-break-routines"></a><span id="kernel_mode_break_routines"></span><span id="KERNEL_MODE_BREAK_ROUTINES"></span>カーネル モード Break ルーチン

カーネル モードのプログラムは、デバッガーを中断、カーネル デバッガーにより、実行を再開するまでに全体のオペレーティング システムがフリーズします。 カーネル デバッガーが存在しない場合、これはバグ チェックとして扱われます。

[ **DbgBreakPoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgbreakpoint)ルーチンが、カーネル モード コードで動作しますが、それ以外の場合に似ています、 **DebugBreak**ユーザー モードのルーチンです。

[ **DbgBreakPointWithStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgbreakpointwithstatus)ルーチンには、中断ともが、さらに、32 ビットの状態コード、デバッガーに送信します。

[ **KdBreakPoint** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))と[ **KdBreakPointWithStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdbreakpointwithstatus)ルーチンと同じ**DbgBreakPoint**と**DbgBreakPointWithStatus**それぞれチェック ビルド環境でコンパイルされた場合。 無料のビルド環境でコンパイルすると、影響ありません。

### <a name="span-idkernelmodeconditionalbreakmacrosspanspan-idkernelmodeconditionalbreakmacrosspankernel-mode-conditional-break-macros"></a><span id="kernel_mode_conditional_break_macros"></span><span id="KERNEL_MODE_CONDITIONAL_BREAK_MACROS"></span>カーネル モードの条件付き改マクロ

2 つの条件付き改マクロはカーネル モード ドライバー用に使用できます。

-   [ **ASSERT** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))マクロは、論理式をテストします。 式が false の場合は、実行が停止され、デバッガーがアクティブになります。 デバッガーでは、失敗した式と、プログラムでは、その場所が表示されます。

-   [ **ASSERTMSG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-assertmsg)マクロと同じ**ASSERT**デバッガーに送信される追加のメッセージを許可する点が異なります。

**ASSERT**と**ASSERTMSG**はアクティブのチェック ビルド環境でのコンパイル時になります。 無料のビルド環境でコンパイルすると、影響ありません。

 

 





