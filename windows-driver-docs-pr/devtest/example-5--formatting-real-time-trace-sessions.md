---
title: 例 5 の書式設定のリアルタイムのトレース セッション
description: 例 5 の書式設定のリアルタイムのトレース セッション
ms.assetid: 340453ab-4736-4191-b9d4-08ee7d9190fe
keywords:
- Tracefmt WDK、リアルタイムのトレース セッション
- WDK のリアルタイムのトレース セッション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27ca23fe8c86b7f62b523a0fb8d919b256d9ec8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527548"
---
# <a name="example-5-formatting-real-time-trace-sessions"></a>例 5:リアルタイムのトレース セッションの書式設定


トレース ログ ファイルに加えてリアルタイム トレース セッションから、トレース メッセージの形式に Tracefmt を使用できます。

次の一連のコマンドは[Tracelog](tracelog.md) Tracefmt とします。 最初のコマンドでは、トレース ログを使用して、Tracedrv サンプル トレース プロバイダーとリアルタイムのトレース セッションを開始します。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)、ソフトウェア トレースのように設計されたドライバーのサンプルが記載されて、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507 )GitHub リポジトリにあります。

```
tracelog -start MyTrace -guid tracedrv.ctl -flag 1 -rt
```

このコマンドは、MyTrace と呼ばれるトレース セッションを開始します。 使用して、-**guid**その制御 GUID ファイルを使用して、Tracedrv.sys のトレース プロバイダーを識別するためにパラメーター tracedrv.ctl します。 使用して、 **-フラグ**を設定するパラメーター、[トレース フラグ](trace-flags.md)値を**1**します。 使用して、 **-rt**パラメーター Tracefmt などのトレース コンシューマーに直接メッセージを配信するトレース セッションを開始します。 なし、 **-rt**パラメーター、トレース プロバイダーは送信メッセージのログ ファイルにのみです。

次のコマンドは、MyTrace トレース セッション中に Tracedrv によって生成されたメッセージの書式設定 Tracefmt を使用します。

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

この Tracefmt コマンドを使用して、 **-rt** MyTrace、リアルタイムのトレース セッションを識別するためにパラメーターおよび **-p** Tracedrv.sys の TMF ファイルが配置されているディレクトリを指定するパラメーター。 **-O**パラメーターは、ローカル ディレクトリに mytrace.txt ファイルに出力を転送します。

このコマンドに応答して、Tracefmt はリアルタイムでのトレース メッセージを書式設定を準備します。 次のステータス メッセージが表示されますが、コマンド プロンプトに戻るはありません。

```
c:\tracetools>tracefmt -rt mytrace -display -o mytrace.txt
Setting RealTime mode for  mytrace
Getting guids from c:\tracetools\default.tmf
```

トレース ログの次のコマンドは、MyTrace トレース セッションを停止します。 別のコマンド プロンプト ウィンドウでコマンドを入力する必要があります。

```
tracelog -stop mytrace
```

トレース セッションが停止したら、Tracefmt は出力ファイルにしてから、コマンド プロンプトに返しますにトレース メッセージを記述したことを報告します。

```
Event traces dumped to mytrace.txt
Event Summary dumped to mytrace.txt.sum
```

 

 





