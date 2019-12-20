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
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0aa10a13187565ff7cedf9e407a58b3e7a0aa80
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209790"
---
# <a name="sending-output-to-the-debugger"></a>デバッガーへの出力の送信


## <span id="ddk_sending_output_to_the_debugger_dbg"></span><span id="DDK_SENDING_OUTPUT_TO_THE_DEBUGGER_DBG"></span>


ユーザーモードとカーネルモードのコードでは、さまざまなルーチンを使用して、出力をデバッガーに送信します。

### <a name="span-iduser_mode_output_routinesspanspan-iduser_mode_output_routinesspanuser-mode-output-routines"></a><span id="user_mode_output_routines"></span><span id="USER_MODE_OUTPUT_ROUTINES"></span>ユーザーモード出力ルーチン

**OutputDebugString**は、null で終わる文字列を呼び出しプロセスのデバッガーに送信します。 ユーザーモードドライバーでは、 **OutputDebugString**によってコマンドウィンドウデバッガーに文字列が表示されます。 デバッガーが実行されていない場合、このルーチンによる影響はありません。 **OutputDebugString**は、 **printf**書式設定された文字列の可変引数をサポートしていません。

このルーチンの完全なドキュメントについては、Microsoft Windows SDK を参照してください。

### <a name="span-idkernel_mode_output_routinesspanspan-idkernel_mode_output_routinesspankernel-mode-output-routines"></a><span id="kernel_mode_output_routines"></span><span id="KERNEL_MODE_OUTPUT_ROUTINES"></span>カーネルモード出力ルーチン

[ **Dbgprint** ] デバッガーウィンドウに出力を表示します。 このルーチンは、基本的な**printf**形式のパラメーターをサポートしています。 **Dbgprint**を呼び出すことができるのは、カーネルモードのコードだけです。

**Dbgprintex**は、 **dbgprint**に似ていますが、メッセージに "タグを付ける" ことができます。 デバッガーを実行するときに、特定のタグを持つメッセージだけを送信することを許可できます。 これにより、関心のあるメッセージだけを表示できます。 詳細については、「[デバッグメッセージの読み取りとフィルター処理](reading-and-filtering-debugging-messages.md)」を参照してください。

**注**   windows Vista 以降のバージョンの windows では、 **dbgprint**でもタグ付きメッセージが生成されます。 これは、以前のバージョンの Windows から変更されています。
**KdPrint**と**KdPrintEx**は、チェックされたビルド環境でコンパイルされると、それぞれ**Dbgprint**と**dbgprintex**と同じです。 無料のビルド環境でコンパイルした場合、影響はありません。

これらのルーチンおよびビルド環境の完全なドキュメントについては、「Windows Driver Kit」を参照してください。
