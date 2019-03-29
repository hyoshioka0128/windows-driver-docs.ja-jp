---
title: 例 6 のトレースの特殊なセッション
description: 例 6 のトレースの特殊なセッション
ms.assetid: 5e528086-812c-478b-a2d1-69d54781cbb2
keywords:
- Tracefmt WDK、特殊なセッション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f43daa3857a69dca363726e2e5e6c7f060115f17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572408"
---
# <a name="example-6-tracing-special-sessions"></a>例 6:特殊なセッションのトレース


Tracefmt を使用するには、NT Kernel Logger、WMI イベント ロガーからのトレース メッセージを書式設定して、グローバル ロガーには、トレース セッションが予約されています。

次のコマンドは、書式設定し、NT Kernel Logger のリアルタイムのトレース セッションからのトレース メッセージを表示します。 (NT Kernel Logger のトレース セッションを開始する方法の詳細については、次を参照してください[traceview で](traceview.md)または[Tracelog](tracelog.md)。)。

```
tracefmt -rt -tmf system.tmf -display
```

使用している場合でも、このコマンドで、トレース セッションの名前が含まれません、 **-rt**パラメーター。 必要でないこの例では、"NT Kernel Logger"が既定値であるためです。

ただし、 **- tmf** Tracefmt を system.tmf ファイルに送信するためにパラメーターが必要です。 既定では、Tracefmt は NT Kernel Logger トレース メッセージの書式が含まれていない、default.tmf を使用します。 **-P** TMF ファイル名が 37753236-c81f-505e-d40a-128d3bb2b5ff.tmf など、メッセージの guid である場合にのみ、パラメーターが TMF ファイルを検索します。

このコマンドを使用しても、 **-表示**パラメーターで、ログ ファイルへの書き込みだけでなく、コマンド プロンプト ウィンドウで、トレース メッセージが表示されます。 この場合は、ため、 **-o**メッセージはパラメーターを省略すると、既定のログ ファイル、FmtFile.txt、ローカル ディレクトリに書き込まれます。

 

 





