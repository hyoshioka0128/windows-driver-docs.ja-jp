---
title: デバッガーへの出力の送信
description: デバッガーへの出力の送信
ms.assetid: e0640e70-9846-4239-a3ff-b78788751384
keywords:
- デバッガーへの出力の送信
- OutputDebugString 関数
- DbgPrint 関数
- DbgPrintEx 関数
- KdPrint 関数
- KdPrintEx 関数
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8251d4dc8ff55d70c7c39533e8cc6ede44900a25
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873854"
---
# <a name="sending-output-to-the-debugger"></a>デバッガーへの出力の送信

ユーザーモードとカーネルモードのコードでは、さまざまなルーチンを使用して、出力をデバッガーに送信します。

## <a name="user-mode-output-routines"></a>ユーザーモード出力ルーチン

**OutputDebugString**ルーチンは、null で終わる文字列を呼び出しプロセスのデバッガーに送信します。 ユーザーモードドライバーでは、 **OutputDebugString**によってコマンドウィンドウデバッガーに文字列が表示されます。 デバッガーが実行されていない場合、このルーチンによる影響はありません。 **OutputDebugString**は、 **printf**書式設定された文字列の可変引数をサポートしていません。

このルーチンのプロトタイプは次のとおりです。

```cpp
VOID OutputDebugString(
   LPCTSTR lpOutputString
   );
```

このルーチンの完全なドキュメントについては、「[デバッガーとの通信](https://docs.microsoft.com/windows/win32/debug/communicating-with-the-debugger)」を参照してください。

### <a name="kernel-mode-output-routines"></a>カーネルモード出力ルーチン

[**Dbgprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)ルーチンは、デバッガーウィンドウに出力を表示します。 このルーチンは、基本的な**printf**形式のパラメーターをサポートしています。 **Dbgprint**を呼び出すことができるのは、カーネルモードのドライバーだけです。

[**Dbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)ルーチンは、 **dbgprint**に似ていますが、メッセージに "タグを付ける" ことができます。 デバッガーを実行するときに、特定のタグを持つメッセージだけを送信することを許可できます。 これにより、関心のあるメッセージだけを表示できます。 詳細については、「[デバッグメッセージの読み取りとフィルター処理](reading-and-filtering-debugging-messages.md)」を参照してください。


[**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)マクロと[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)マクロは、チェックされたビルド環境でコンパイルされると、それぞれ**Dbgprint**および**dbgprintex**と同じです。 無料のビルド環境でコンパイルした場合、影響はありません。
