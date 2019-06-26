---
title: デバッガーへの出力の送信
description: デバッガーへの出力の送信
ms.assetid: ee167261-78cd-4178-ba98-3250cc735657
keywords:
- WDK、出力を送信するコードのデバッグ
- 出力をデバッガーに送信します。
- 出力ルーチン WDK
- ユーザー モード出力ルーチン WDK
- カーネル モード出力ルーチン WDK
- ルーチンのデバッグは、WDK の出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca4cd449ab950ca82c8a4c9719c076525cc020a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374426"
---
# <a name="sending-output-to-the-debugger"></a>デバッガーへの出力の送信


## <span id="ddk_sending_output_to_the_debugger_tools"></span><span id="DDK_SENDING_OUTPUT_TO_THE_DEBUGGER_TOOLS"></span>


ユーザー モードとカーネル モード ドライバーでは、異なるルーチンを使用して、出力をデバッガーに送信します。

### <a name="span-idusermodeoutputroutinesspanspan-idusermodeoutputroutinesspanuser-mode-output-routines"></a><span id="user_mode_output_routines"></span><span id="USER_MODE_OUTPUT_ROUTINES"></span>ユーザー モード出力ルーチン

**OutputDebugString**ルーチンが null で終わる文字列を呼び出し元プロセスのデバッガーに送信します。 ユーザー モードのドライバー、 **OutputDebugString**デバッガー コマンド ウィンドウで、文字列が表示されます。 デバッガーが実行されていない場合は、このルーチンに影響はありません。 **OutputDebugString**の可変個の引数をサポートしていません、 **printf**文字列の書式を設定します。

このルーチンのプロトタイプは次のとおりです。

```
VOID OutputDebugString(
   LPCTSTR lpOutputString
   );
```

このルーチンは、windows.h のヘッダーを含む任意のユーザー モード ドライバーによって呼び出すことができます。 このルーチンとその他のユーザー モード ルーチンのデバッグに役立つ詳細なドキュメントについては、Microsoft Windows SDK を参照してください。

### <a name="span-idkernelmodeoutputroutinesspanspan-idkernelmodeoutputroutinesspankernel-mode-output-routines"></a><span id="kernel_mode_output_routines"></span><span id="KERNEL_MODE_OUTPUT_ROUTINES"></span>カーネル モード出力ルーチン

[**による DbgPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprint)ルーチンでは、デバッガー ウィンドウに出力が表示されます。 このルーチンには、basic がサポートしている**printf**パラメーターの書式を設定します。 カーネル モード ドライバーのみが呼び出せる**による DbgPrint**します。

[ **DbgPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprintex)ルーチンはのような**による DbgPrint**に、メッセージの「タグ」ことができます。 デバッガーを実行するときに送信する特定のタグを持つメッセージのみを許可することができます。 これにより、興味のあるメッセージだけを表示することができます。 詳細については、次を参照してください。[読み取りとデバッグ メッセージをフィルター処理](reading-and-filtering-debugging-messages.md)します。

**注**  で Windows Vista と以降のバージョンの Windows、**による DbgPrint**が生成されますがメッセージにもタグ付けします。 以前のバージョンの Windows、**による DbgPrint**タグなしのメッセージを生成します。

 

[ **KdPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprint)と[ **KdPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprintex)マクロと同じ**による DbgPrint**と**DbgPrintEx**それぞれチェック ビルド環境でコンパイルされた場合。 無料のビルド環境でコンパイルすると、影響ありません。

 

 





