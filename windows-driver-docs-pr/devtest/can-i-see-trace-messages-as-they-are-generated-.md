---
title: 表示できますトレース メッセージは、生成時
description: 表示できますトレース メッセージは、生成時
ms.assetid: 21d8606b-5693-4f50-81f9-c5c3a65c0550
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60b1b65a224878517ef50ff70c9dddb7b316f4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553557"
---
# <a name="can-i-see-trace-messages-as-they-are-generated"></a>生成されると、トレース メッセージを表示できますか。


[はい]。 トレースを表示するメッセージが生成されるオプションを使用して、リアルタイムのトレース セッション[traceview で](traceview.md)、 [Tracelog](tracelog.md)、または[Tracefmt](tracefmt.md)します。 これらのツールは、ツールに含まれる\\トレース\\&lt;*プラットフォーム*&gt;サブディレクトリ Microsoft Windows Driver Kit (WDK) の場所&lt; *プラットフォーム*&gt; i386、amd64、または ia64 のいずれかです。

[トレース プロバイダー](trace-provider.md)リアルタイムのトレースをサポートするために特別なコードを含める必要はありません。

### <a name="span-idtraceviewspanspan-idtraceviewspantraceview"></a><span id="traceview"></span><span id="TRACEVIEW"></span>Traceview で

[Traceview で](traceview.md)生成されると、トレース メッセージを表示するリアルタイムのトレース セッションを開始できます。 Traceview でのリアルタイム監視を使用するには

1.  Traceview でを起動します。

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  クリックして**プロバイダーを追加する**します。

4.  選択、 **CTL (コントロールの GUID) ファイル**オプション。 クリックして省略記号ボタン (**.**) を検索する、[制御 GUID ファイル](control-guid-file.md)プロバイダー。

5.  クリックして**TMF ファイル選択**します。

6.  をクリックして**追加**、検索、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)プロバイダーには、次のようにクリックします。**オープン**、順にクリックします**完了**。

7.  **[次へ]** をクリックします。

8.  **ログ セッション オプション** ページで、いることを確認、**リアルタイム表示** チェック ボックスが選択されている (オン)。

    指定するには、その他のオプションを選択することができます[トレース フラグ](trace-flags.md)と[トレース レベル](trace-level.md)、またはトレース セッションをカスタマイズします。

9.  **[Finish]**(完了) をクリックします。

Traceview の詳細については、上、**ヘルプ** メニューのをクリックして**ヘルプ トピック**します。

### <a name="span-idtracelogspanspan-idtracelogspantracelog"></a><span id="tracelog"></span><span id="TRACELOG"></span>トレース ログ

トレース ログは、開始、停止、およびリアルタイムのトレース セッションを更新できます。

トレース ログを使用してリアルタイムのトレース セッションを開始するには、使用、 **-rt**トレース セッションを開始するコマンド (リアルタイム) のパラメーター。

次のコマンドは、プロバイダーと「マイ トレース」と呼ばれるトレース セッションを開始、MyProvider.ctl で Guid が表示されているコントロール[制御 GUID ファイル](control-guid-file.md)します。 **-Rt**パラメーターは、リアルタイムのトレース セッションを指定します。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt
```

詳細の例では、次を参照してください。[例 10。リアルタイムのトレース セッションを開始する](example-10--starting-a-real-time-trace-session.md)します。

リアルタイムのトレース セッションからのトレース メッセージを表示する使用[Tracefmt](tracefmt.md)します。

### <a name="span-idtracefmtspanspan-idtracefmtspantracefmt"></a><span id="tracefmt"></span><span id="TRACEFMT"></span>Tracefmt

[Tracefmt](tracefmt.md)リアルタイム トレース セッションからのトレース メッセージを表示することができます。 リアルタイム モードでは、Tracefmt は書式設定し、ファイルに書き込まれたメッセージが表示されます。

次のコマンドでは、"MyTrace"リアルタイム トレース セッションからのトレース メッセージが表示されます。 **-Rt**パラメーターは、リアルタイムのセッションを指定します。 **-P**パラメーターのパスを示します、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース メッセージ。 **-表示**パラメーターが Tracefmt バッファーから到着すると、トレース メッセージを表示するように指示します。 **-O**パラメーター、出力ファイルの場所を指定します。

```
tracefmt -rt MyTrace -p c:\tracing -display -o mytrace.txt
```

詳細の例では、次を参照してください。[例 5。リアルタイムのトレース セッションの書式設定](example-5--formatting-real-time-trace-sessions.md)します。

 

 





