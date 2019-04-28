---
title: デバッガーへの出力の送信
description: デバッガーへの出力の送信
ms.assetid: e0640e70-9846-4239-a3ff-b78788751384
keywords:
- 出力をデバッガーに送信します。
- OutputDebugString 関数
- による DbgPrint 関数
- DbgPrintEx 関数
- KdPrint 関数
- KdPrintEx 関数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f36b17bc543213ccb01cb8f985d4be42e8086b5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381978"
---
# <a name="sending-output-to-the-debugger"></a>デバッガーへの出力の送信


## <span id="ddk_sending_output_to_the_debugger_dbg"></span><span id="DDK_SENDING_OUTPUT_TO_THE_DEBUGGER_DBG"></span>


ユーザー モードとカーネル モード コードでは、異なるルーチンを使用して、出力をデバッガーに送信します。

### <a name="span-idusermodeoutputroutinesspanspan-idusermodeoutputroutinesspanuser-mode-output-routines"></a><span id="user_mode_output_routines"></span><span id="USER_MODE_OUTPUT_ROUTINES"></span>ユーザー モード出力ルーチン

**OutputDebugString** null で終わる文字列を呼び出し元プロセスのデバッガーに送信します。 ユーザー モードのドライバー、 **OutputDebugString**デバッガー コマンド ウィンドウで、文字列が表示されます。 デバッガーが実行されていない場合は、このルーチンに影響はありません。 **OutputDebugString**の可変個の引数をサポートしていません、 **printf**文字列の書式を設定します。

このルーチンの完全なドキュメントについては、Microsoft Windows SDK を参照してください。

### <a name="span-idkernelmodeoutputroutinesspanspan-idkernelmodeoutputroutinesspankernel-mode-output-routines"></a><span id="kernel_mode_output_routines"></span><span id="KERNEL_MODE_OUTPUT_ROUTINES"></span>カーネル モード出力ルーチン

**による DbgPrint**デバッガー ウィンドウに出力が表示されます。 このルーチンには、basic がサポートしている**printf**パラメーターの書式を設定します。 カーネル モード コードのみを呼び出すことができます**による DbgPrint**します。

**DbgPrintEx**のような**による DbgPrint**に、メッセージの「タグ」ことができます。 デバッガーを実行するときに送信する特定のタグを持つメッセージのみを許可することができます。 これにより、興味のあるメッセージだけを表示することができます。 詳細については、次を参照してください。[読み取りとデバッグ メッセージをフィルター処理](reading-and-filtering-debugging-messages.md)します。

**注**  で Windows Vista と以降のバージョンの Windows、**による DbgPrint**が生成されますがメッセージにもタグ付けします。 これは、Windows の以前のバージョンからの変更点です。

 

**KdPrint**と**KdPrintEx**と同じ**による DbgPrint**と**DbgPrintEx**をそれぞれチェック ビルド環境でコンパイルされた場合。 無料のビルド環境でコンパイルすると、影響ありません。

ビルド環境と同様に、これらのルーチンの完全なドキュメントについては、Windows Driver Kit を参照してください。

 

 





