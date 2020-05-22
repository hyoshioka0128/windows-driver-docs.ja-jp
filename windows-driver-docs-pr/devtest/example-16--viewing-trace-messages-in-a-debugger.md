---
title: 例16デバッガーでトレースメッセージを表示する
description: 例16デバッガーでトレースメッセージを表示する
ms.assetid: c548643c-ae0c-47e7-af0a-0d89ed78f281
keywords:
- WDK を表示するトレースメッセージ
- トレースメッセージの表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2c86e9a266e069c79a62b1c74e7f05c44caf1d0
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769678"
---
# <a name="example-16-viewing-trace-messages-in-a-debugger"></a>例 16: デバッガーでのトレースメッセージの表示


## <span id="ddk_viewing_trace_messages_in_a_debugger_tools"></span><span id="DDK_VIEWING_TRACE_MESSAGES_IN_A_DEBUGGER_TOOLS"></span>


この例では、トレースメッセージを KD または WinDbg にリダイレクトする方法を示します。

トレースセッションを開始する前に、ホストコンピューター上のデバッガーの検索パスに Wmitrace と Traceprt があることを確認します。 これらの Dll は、windows[のデバッグツール](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)の \\ \\ windows Winxp ディレクトリのプログラムファイルデバッグツールに含まれてい \\ ます。 (ディレクトリ名にかかわらず、ファイルは windows 2000 以降のバージョンの Windows で動作します)。

また、トレースプロバイダーの[トレースメッセージフォーマットファイル](trace-message-format-file.md)(tmf) がデバッガーの検索パスにあることを確認します。

デバッガーの検索パスを設定するには、wmitrace の searchpath 特殊化されたデバッガー拡張機能を使用するか、% TRACE \_ FORMAT \_ search \_ path% 環境変数の値を設定します。 次に例を示します。

```
set TRACE_FORMAT_SEARCH_PATH=c:\tracing
```

次に、デバッガーを起動します。 **-Kd**パラメーターを指定して tracelog コマンドを送信するときに、デバッガーが実行されていない場合、tracelog は応答を停止します ("ハング")。

次のコマンドは、トレースセッションを開始し、のトレースメッセージを KD または Windbg に送信します (どちらか一方がアタッチされている場合)。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**トレースログ-start**コマンドには、トレースセッションを開始するためのセッション名が含まれています。 この例では、 **-guid**パラメーターを使用してプロバイダーファイルを識別します。 また、 **-rt**パラメーターを使用してリアルタイムのトレースセッションを開始し、トレースメッセージがログファイルではなくデバッガーに送信されるようにします。

応答として、Tracelog はセッションを開始したことを報告します。 トレースプロバイダーがメッセージを生成すると、メッセージがデバッガーに表示されます。

デバッガーでメッセージを表示するには、WMI トレース拡張機能を使用します。 詳細については、「 [Windows 用デバッグツール](https://docs.microsoft.com/windows-hardware/drivers/debugger/)」を参照してください。

 

 





