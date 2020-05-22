---
title: トレースメッセージをカーネルデバッガーに送信操作方法には
description: トレースメッセージをカーネルデバッガーに送信操作方法には
ms.assetid: 867791a7-30a5-4539-be85-61f1716c279a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 956f11355ab3a1cfee8484a0f06680ee5b91d91d
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769620"
---
# <a name="how-do-i-send-trace-messages-to-a-kernel-debugger"></a>カーネル デバッガーにトレース メッセージを送信する方法


複数のメソッドを使用して、カーネルモードのデバッガーにトレースメッセージをリダイレクトできます。 ここでは、いくつかについて説明します。

トレースメッセージは、接続されているいずれかの場合に、KD または Windbg にリダイレクトできます。 デバッガーは、デバッグ (null モデム) ケーブルを使用する COM ポート、または IEEE 1394 ケーブルを使用した 1394 ("firewire") ポートを介してアタッチする必要があります。 トレースメッセージを他のカーネルデバッガー (NTSD など) にリダイレクトすることはできません。

デバッガーでトレースメッセージを表示するには、wmitrace と traceprt がホストコンピューター上のデバッガーの検索パスに存在している必要があります。 これらの Dll は、[デバッグツール (Windows の](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)場合) にも含まれています。デバッガーがトレースメッセージの[トレースメッセージ形式 (tmf) ファイル](trace-message-format-file.md)を検索できるようにするには、ホストコンピューター上のデバッガーの検索パスに tmf ファイルが含まれている必要があります。 デバッガーの検索パスを設定するには、wmitrace の searchpath 特殊化されたデバッガー拡張機能を使用するか、% TRACE \_ FORMAT \_ search \_ path% 環境変数の値を設定します。

詳細については、「 *Windows 用デバッグツール*」で **! wmitrace**を検索してください。

### <a name="span-idlogmanspanspan-idlogmanspanlogman"></a><span id="logman"></span><span id="LOGMAN"></span>Logman

カーネルモードのデバッガーにトレースメッセージをリダイレクトするには、次の Logman コマンドを使用します。

```
logman start TraceSession -ets -mode KernelFilter -bs 3
```

**-** 引数を指定すると、パフォーマンスログと警告サービスによって制御されないイベントトレースセッションが開始されます。 **-Mode**パラメーターを指定すると、詳細オプション (**カーネルフィルター**オプションを含む) がアクティブになります。

**-Bs**パラメーターを指定すると、トレースセッションのバッファーサイズがデバッガーの最大バッファーサイズである 3 KB に設定されます。 このパラメーターを省略した場合、デバッガーセッションは正常に動作しません。

Logman は、windows XP 以降のバージョンの Windows に含まれています。

### <a name="span-idtracelogspanspan-idtracelogspantracelog"></a><span id="tracelog"></span><span id="TRACELOG"></span>トレースログ

次の[Tracelog](tracelog.md)コマンドを使用して、カーネルモードのデバッガーにトレースメッセージをリダイレクトします。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**-Guid**パラメーターは、[トレースプロバイダー](trace-provider.md)を指定します。 **-Rt**パラメーターは、リアルタイムのトレースセッションを指定します。 **-Kd**パラメーターを指定すると、トレースメッセージがカーネルデバッガーにリダイレクトされ、最大バッファーサイズがデバッガーの最大値である 3 KB に設定されます。

例については、「[例 16: デバッガーでのトレースメッセージの表示](example-16--viewing-trace-messages-in-a-debugger.md)」を参照してください。

Tracelog は、 \\ WDK の tools tracing \\ * &lt; Platform &gt; *サブディレクトリにあります。 * &lt; プラットフォーム &gt; *は、i386、amd64、ia64 のいずれかです。

### <a name="span-idtraceviewspanspan-idtraceviewspantraceview"></a><span id="traceview"></span><span id="TRACEVIEW"></span>TraceView

[Traceview](traceview.md)にはグラフィカルユーザーインターフェイスがあります。

トレースセッションを作成するときに、トレースメッセージをカーネルデバッガーにリダイレクトすることができます。 [**ログセッションオプション**] ページで、[ログセッションの**詳細オプション**] をクリックし、[**ログセッションパラメーターのオプション**] タブをクリックして、[ **Windbg** ] オプションの値を**TRUE**に変更します。 トレースセッションの実行中にこのオプションを変更することはできません。

Traceview は、 \\ WDK の tools tracing \\ * &lt; Platform &gt; *サブディレクトリにあります。ここで、 * &lt; Platform &gt; *は i386、amd64、ia64 のいずれかです。

 

 





