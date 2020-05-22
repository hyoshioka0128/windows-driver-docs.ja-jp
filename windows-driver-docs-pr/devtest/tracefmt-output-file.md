---
title: Tracefmt の出力ファイル
description: Tracefmt の出力ファイル
ms.assetid: 55c8964c-992f-468c-83ea-0316fcb12110
keywords:
- Tracefmt WDK、出力ファイル
- 出力ファイル WDK Tracefmt
- ファイル WDK Tracefmt
- out ファイル
- out ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5dee9ffeb1a8b5b7c70c37526fcb4af762ee533
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769580"
---
# <a name="tracefmt-output-file"></a>Tracefmt の出力ファイル


Tracefmt 出力 (out) ファイルは、ユーザーが判読できる形式でトレースログまたはリアルタイムトレースセッションからのトレースメッセージを表示するテキストファイルです。 各トレースメッセージの前には、カスタマイズ可能な[トレースメッセージのプレフィックス](trace-message-prefix.md)が付いています。

Tracefmt 出力ファイルは省略可能です。 トレースメッセージを表示するように Tracefmt に指示できますが、出力ファイルを作成することはできません。また、トレースメッセージを表示して出力ファイルに記録することもできます。

Tracefmt 出力ファイルは、トレースメッセージを分析およびフィルター処理する他のプログラムへの入力としてよく使用されます。

次に示すのは、ソフトウェアトレース用にインストルメント化されたサンプルドライバーである Tracefmt で、トレースセッションの Tracefmt 出力ファイルの内容を抜粋したものです。 ソフトウェアトレース用に設計された[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)は、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

```
EventTrace
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]IOCTL = 1
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 1 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 2 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 3 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 4 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 5 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 6 Hi
```

 

 





