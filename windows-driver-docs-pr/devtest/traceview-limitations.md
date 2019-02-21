---
title: Traceview での制限事項
description: Traceview での制限事項
ms.assetid: 946d7c69-7c6a-4bab-8fa5-fc21dcf85ddb
keywords:
- Traceview で WDK、制限事項
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 852cc78489f444d45429c8176bccfabc45e07368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550396"
---
# <a name="traceview-limitations"></a>Traceview での制限事項


このトピックでは、traceview での制限事項について説明します。

## <a name="traceview-window-limitations"></a>Traceview でウィンドウの制限事項

Traceview でウィンドウを表示でき、ウィンドウを使用して開始されるトレース セッションのみを制御します。 一覧、およびコントロールを使用して、システム上のセッションのすべてのトレースを[traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md)します。

Traceview で終了すると、すべての実行が停止 (または*リアルタイム*) traceview でを使用して開始したセッションをトレースします。 Traceview でウィンドウとは無関係に実行トレース セッションを開始するには、traceview でのコマンド ライン インターフェイスを使用します。

使用することができます、 [traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md)とその他のソフトウェアなど、ツールをトレース[Tracelog](tracelog.md)、traceview で開始したトレース セッションを制御します。 ただし、これらのツールを使用して、実行中のトレース セッションのプロパティを変更する場合は、トレース セッションの実行中に変更できるプロパティを変更した場合でも traceview で、トレース セッションは停止します。 Traceview で再起動に使用する場合 (または*結合*)、トレース セッション プロパティを更新します。

## <a name="traceview-command-line-limitations"></a>Traceview でコマンドラインの制限事項

コマンド プロンプト ウィンドウで traceview でコマンドを送信するときに、traceview では、その出力を表示する新しいコマンド プロンプト ウィンドウを開きます。 これらの追加のウィンドウを抑制することはできません。

## <a name="etw-limitations"></a>ETW の制限事項

Traceview でとを Event Tracing for Windows (ETW) に基づくその他のトレース ツールは、1 つだけのトレース セッションを作成または WPP または従来のトレース プロバイダーごとに 1 つのトレース ログを表示します。 トレース セッションを作成または別のトレース セッションで既に有効になっている WPP プロバイダーでトレース ログを表示する場合は、その他のセッションで無効化されます。

## <a name="global-logger-trace-sessions"></a>グローバルのロガーのトレース セッション

Traceview でウィンドウには、開始するためのオプションはありません、[グローバル ロガー トレース セッション](global-logger-trace-session.md)します。 ただし、グローバルのロガーを入力してグローバル ロガー トレース セッションを開始するウィンドウを使用することができます[コントロール GUID](control-guid.md)、e8908abc aa84-11 d 2-9a93-00805f85d7c6、またはコントロールの GUID を保存することによってで、[制御 GUID ファイル](control-guid-file.md). これらの手順の詳細については、次を参照してください。[トレース セッションを作成するコントロールの GUID を持つ](creating-a-trace-session-with-a-control-guid.md)と[CTL ファイルを使用してトレース セッションを作成する](creating-a-trace-session-with-a-ctl-file.md)します。

使用することも、 [traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md)グローバル ロガーのトレース セッションを開始します。 グローバル ロガー トレース セッションを開始するのにには、次のコマンドを使用します。 このコマンドでは、"GlobalLogger"という単語が大文字小文字を区別します。

```dos
traceview -start GlobalLogger [parameters]
```

Traceview でコマンドの詳細については、次を参照してください。 [traceview で管理コマンド](traceview-control-commands.md)します。

## <a name="enabling-trace-providers"></a>トレース プロバイダーを有効にします。

Traceview では、トレース セッションに追加したトレース プロバイダーを自動的に有効にします。 ただし、トレース セッションを作成した後、トレース セッションを別のトレース プロバイダーを有効にするか、トレース セッションに追加したトレース プロバイダーを無効にする traceview でウィンドウを使用することはできません。

有効またはプロバイダーを無効にする、使用、 **traceview で-有効にする**コマンド。 このコマンドの詳細については、次を参照してください。 [ **traceview で管理コマンド**](traceview-control-commands.md)します。
