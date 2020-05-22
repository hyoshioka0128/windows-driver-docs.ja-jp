---
title: 例5リアルタイムトレースセッションの書式設定
description: 例5リアルタイムトレースセッションの書式設定
ms.assetid: 340453ab-4736-4191-b9d4-08ee7d9190fe
keywords:
- Tracefmt WDK、リアルタイムトレースセッション
- リアルタイムトレースセッション WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e13b16211e937a9dd5b9681c3070d9850413b302
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769696"
---
# <a name="example-5-formatting-real-time-trace-sessions"></a>例 5: リアルタイムのトレースセッションの書式設定


トレースログファイルに加えて、トレースメッセージをリアルタイムのトレースセッションから書式設定するには、Tracefmt を使用します。

次の一連のコマンドでは、 [Tracelog](tracelog.md)と Tracefmt を使用します。 最初のコマンドは、Tracelog を使用して、Tracedrv サンプルトレースプロバイダーとのリアルタイムトレースセッションを開始します。 ソフトウェアトレース用に設計された[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)は、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

```
tracelog -start MyTrace -guid tracedrv.ctl -flag 1 -rt
```

このコマンドは、MyTrace という名前のトレースセッションを開始します。 この例では、-**guid**パラメーターを使用して、トレースプロバイダーである tracedrv を識別します。そのためには、コントロール guid ファイルである tracedrv を使用します。 [トレースフラグ](trace-flags.md)の値を**1**に設定するには、 **-flag**パラメーターを使用します。 この例では、 **-rt**パラメーターを使用して、Tracefmt などのトレースコンシューマーにメッセージを直接配信するトレースセッションを開始します。 **-Rt**パラメーターを指定しない場合、トレースプロバイダーはログファイルにのみメッセージを送信します。

次のコマンドは、Tracefmt を使用して、MyTrace トレースセッション中に Tracefmt によって生成されるメッセージを書式設定します。

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

この Tracefmt コマンドは、 **-rt**パラメーターを使用して、リアルタイムのトレースセッション、mytrace、および **-p**パラメーターを識別し、TRACEFMT の tmf ファイルが配置されているディレクトリを指定します。 **-O**パラメーターを指定すると、出力がローカルディレクトリの mytrace .txt ファイルに送られます。

このコマンドに応答して、Tracefmt はトレースメッセージをリアルタイムで書式設定することを準備します。 次のステータスメッセージが表示されますが、コマンドプロンプトに戻りません。

```
c:\tracetools>tracefmt -rt mytrace -display -o mytrace.txt
Setting RealTime mode for  mytrace
Getting guids from c:\tracetools\default.tmf
```

次の Tracelog コマンドは、MyTrace トレースセッションを停止します。 別のコマンドプロンプトウィンドウでコマンドを入力する必要があります。

```
tracelog -stop mytrace
```

トレースセッションが停止すると、Tracefmt は、出力ファイルにトレースメッセージを書き込んだことを報告してから、コマンドプロンプトに戻ります。

```
Event traces dumped to mytrace.txt
Event Summary dumped to mytrace.txt.sum
```

 

 





