---
title: デバッガーへの出力の送信
description: デバッガーへの出力の送信
ms.assetid: ee167261-78cd-4178-ba98-3250cc735657
keywords:
- コード WDK のデバッグ、出力の送信
- 出力をデバッガーに送信しています
- 出力ルーチン WDK
- ユーザーモード出力ルーチン WDK
- カーネルモード出力ルーチン WDK
- ルーチン WDK デバッグ、出力
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7b0096388d1c43baaafde7532c18737413e523d5
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428347"
---
# <a name="sending-output-to-the-debugger"></a>デバッガーへの出力の送信

ユーザーモードとカーネルモードのドライバーは、さまざまなルーチンを使用して、出力をデバッガーに送信します。

## <a name="user-mode-output-routines"></a>ユーザーモード出力ルーチン

**OutputDebugString**ルーチンは、null で終わる文字列を呼び出しプロセスのデバッガーに送信します。 ユーザーモードドライバーでは、 **OutputDebugString**によってコマンドウィンドウデバッガーに文字列が表示されます。 デバッガーが実行されていない場合、このルーチンによる影響はありません。 **OutputDebugString**は、 **printf**書式設定された文字列の可変引数をサポートしていません。

このルーチンのプロトタイプは次のとおりです。

```cpp
VOID OutputDebugString(
   LPCTSTR lpOutputString
   );
```

このルーチンは、windows .h ヘッダーを含むユーザーモードドライバーによって呼び出すことができます。 このルーチンと、デバッグに役立つその他のユーザーモードルーチンの完全なドキュメントについては、Microsoft Windows SDK を参照してください。

## <a name="kernel-mode-output-routines"></a>カーネルモード出力ルーチン

[**Dbgprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)ルーチンは、デバッガーウィンドウに出力を表示します。 このルーチンは、基本的な**printf**形式のパラメーターをサポートしています。 **Dbgprint**を呼び出すことができるのは、カーネルモードのドライバーだけです。

[**Dbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)ルーチンは、 **dbgprint**に似ていますが、メッセージに "タグを付ける" ことができます。 デバッガーを実行するときに、特定のタグを持つメッセージだけを送信することを許可できます。 これにより、関心のあるメッセージだけを表示できます。 詳細については、「[デバッグメッセージの読み取りとフィルター処理](reading-and-filtering-debugging-messages.md)」を参照してください。

> [!NOTE]
> Windows Vista 以降のバージョンの Windows では、 **Dbgprint**でもタグ付きメッセージが生成されます。 以前のバージョンの Windows では、 **Dbgprint**はタグなしのメッセージを生成しました。

[**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)マクロと[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)マクロは、チェックされたビルド環境でコンパイルされると、それぞれ**Dbgprint**および**dbgprintex**と同じです。 無料のビルド環境でコンパイルした場合、影響はありません。
