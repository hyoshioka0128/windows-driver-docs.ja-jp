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
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: b0a8617e4a7b876b3bad9670a674a3518cd8a9fe
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873847"
---
# <a name="breaking-into-the-debugger"></a>デバッガーへの割り込み

ユーザーモードとカーネルモードのコードでは、さまざまなルーチンを使用してデバッガーを中断します。

## <a name="user-mode-break-routines"></a>ユーザーモードの中断ルーチン

中断ルーチンは、現在のプロセスで例外を発生させます。これにより、呼び出し元のスレッドが呼び出し元のプロセスに関連付けられたデバッガーに通知できるようになります。

ユーザーモードプログラムからデバッガーを中断するには、 [DebugBreak 関数](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-debugbreak)を使用します。 プロトタイプは次のとおりです。

```cpp
VOID DebugBreak(VOID);
```

ユーザーモードプログラムが**DebugBreak**を呼び出すと、次の操作が実行されます。

1. ユーザーモードのデバッガーがアタッチされている場合、プログラムはデバッガーを中断します。 これは、プログラムが一時停止し、デバッガーがアクティブになることを意味します。

2. ユーザーモードのデバッガーがアタッチされていないが、起動時にカーネルモードのデバッグが有効になっている場合、コンピューター全体がカーネルデバッガーに侵入します。 カーネルデバッガーがアタッチされていない場合、コンピューターはカーネルデバッガーをフリーズし、待機します。

3. ユーザーモードのデバッガーがアタッチされておらず、カーネルモードのデバッグが有効になっていない場合、プログラムはハンドルされない例外で終了し、事後分析 (ジャストインタイム) デバッガーがアクティブ化されます。 詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。

## <a name="kernel-mode-break-routines"></a>カーネルモードの中断ルーチン

カーネルモードプログラムがデバッガーに侵入すると、カーネルデバッガーが実行を再開できるまで、オペレーティングシステム全体がフリーズします。 カーネルデバッガーが存在しない場合、これはバグチェックとして扱われます。

[**Dbgbreakpoint ポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)ルーチンは、カーネルモードコードで動作しますが、それ以外の場合は**DebugBreak**ユーザーモードルーチンに似ています。

また、 [**Dbgbreakpointwithstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)ルーチンでも break が発生しますが、さらに、32ビットのステータスコードがデバッガーに送信されます。

[**KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))ルーチンと[**KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)ルーチンは、チェックされたビルド環境でコンパイルされると、それぞれ**Dbgbreakpoint ポイント**と**dbgbreakpointwithstatus**と同じです。 無料のビルド環境でコンパイルした場合、影響はありません。

## <a name="kernel-mode-conditional-break-routines"></a>カーネルモードの条件付き中断ルーチン

カーネルモードのコードでは、2つの条件付きブレークルーチンを使用できます。 これらのルーチンは、論理式をテストします。 式が false の場合、実行が停止し、デバッガーがアクティブになります。

- [**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))マクロは、論理式をテストします。 式が false の場合、実行が停止し、デバッガーがアクティブになります。 失敗した式とプログラム内のその位置がデバッガーに表示されます。

- [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)マクロは、追加のメッセージをデバッガーに送信することを許可する点を除いて、 **ASSERT**と同じです。

**ASSERT**と**ASSERTMSG**は、チェックされたビルド環境でコンパイルした場合にのみアクティブになります。 無料のビルド環境でコンパイルした場合、影響はありません。
