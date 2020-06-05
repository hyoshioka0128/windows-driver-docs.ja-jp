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
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 583e7206e3e5a7c1ef25942ac26947c69031e162
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428335"
---
# <a name="breaking-into-the-debugger"></a>デバッガーへの割り込み

ユーザーモードとカーネルモードのドライバーは、デバッガーを中断するためにさまざまなルーチンを使用します。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

## <a name="user-mode-break-routines"></a>ユーザーモードの中断ルーチン

中断ルーチンは、現在のプロセスで例外を発生させます。これにより、呼び出し元のスレッドが呼び出し元のプロセスに関連付けられたデバッガーに通知できるようになります。

ユーザーモードプログラムからデバッガーを中断するには、 **DebugBreak**ルーチンを使用します。 プロトタイプは次のとおりです。

```cpp
VOID DebugBreak(VOID);
```

このルーチンは、windows .h ヘッダーを含むユーザーモードドライバーによって呼び出すことができます。 このルーチンと、デバッグに役立つその他のユーザーモードルーチンの完全なドキュメントについては、Microsoft Windows SDK を参照してください。

ユーザーモードプログラムが**DebugBreak**を呼び出すと、次の操作が実行されます。

1. ユーザーモードのデバッガーがアタッチされている場合、プログラムはデバッガーを中断します。 これは、プログラムが一時停止し、デバッガーがアクティブになることを意味します。

1. ユーザーモードのデバッガーがアタッチされていないが、起動時にカーネルモードのデバッグが有効になっている場合、コンピューター全体がカーネルデバッガーに侵入します。 カーネルデバッガーがアタッチされていない場合、コンピューターはカーネルデバッガーをフリーズし、待機します。

1. ユーザーモードのデバッガーがアタッチされておらず、カーネルモードのデバッグが有効になっていない場合、プログラムはハンドルされない例外で終了し、事後分析 (ジャストインタイム) デバッガーがアクティブ化されます。 既定では、事後分析デバッガーはワトソン博士です。これにより、クラッシュダンプファイルが作成され、このクラッシュダンプファイルを Microsoft に送信するかどうかを確認するメッセージが表示されます。

## <a name="kernel-mode-break-routines"></a>カーネルモードの中断ルーチン

カーネルモードプログラムがデバッガーに侵入すると、カーネルデバッガーが実行を再開できるまで、オペレーティングシステム全体がフリーズします。 カーネルデバッガーが存在しない場合、これはバグチェックとして扱われます。

[**Dbgbreakpoint ポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)ルーチンは、カーネルモードコードで動作しますが、それ以外の場合は**DebugBreak**ユーザーモードルーチンに似ています。

また、 [**Dbgbreakpointwithstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)ルーチンでも break が発生しますが、さらに、32ビットのステータスコードがデバッガーに送信されます。

[**KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))ルーチンと[**KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)ルーチンは、チェックされたビルド環境でコンパイルされると、それぞれ**Dbgbreakpoint ポイント**と**dbgbreakpointwithstatus**と同じです。 無料のビルド環境でコンパイルした場合、影響はありません。

## <a name="kernel-mode-conditional-break-macros"></a>カーネルモードの条件付き中断マクロ

カーネルモードドライバーでは、次の2つの条件付きブレークマクロを使用できます。

- [**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))マクロは、論理式をテストします。 式が false の場合、実行が停止し、デバッガーがアクティブになります。 失敗した式とプログラム内のその位置がデバッガーに表示されます。

- [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)マクロは、追加のメッセージをデバッガーに送信することを許可する点を除いて、 **ASSERT**と同じです。

**ASSERT**と**ASSERTMSG**は、チェックされたビルド環境でコンパイルした場合にのみアクティブになります。 無料のビルド環境でコンパイルした場合、影響はありません。
