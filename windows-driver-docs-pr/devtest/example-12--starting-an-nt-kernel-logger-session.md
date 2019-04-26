---
title: NT カーネル ロガー セッションを開始する 12 の例
description: NT カーネル ロガー セッションを開始する 12 の例
ms.assetid: ce795cd3-4d95-49a1-a8b7-a32c69c776dd
keywords:
- WDK、NT Kernel Logger のセッションをトレースします。
- トレース セッションの NT Kernel Logger WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f0c75886d6b984d0d794f3ed4087d09302e3c3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344721"
---
# <a name="example-12-starting-an-nt-kernel-logger-session"></a>例 12:NT カーネル ロガー セッションの開始


## <span id="ddk_starting_an_nt_kernel_logger_session_tools"></span><span id="DDK_STARTING_AN_NT_KERNEL_LOGGER_SESSION_TOOLS"></span>


次のコマンドは、NT Kernel Logger トレース セッションを開始します。 NT Kernel Logger トレース セッションが既定値であるため、その他のパラメーターは必要ありません。

```
tracelog -start
```

既定、プロセス、スレッド、ディスク、および TCP/IP では、イベントがトレースされます。 既定の設定を無効にするには、NT Kernel Logger セッション用に設計されたパラメーターを使用することができます。

次のコマンドを使用して、 **- nothread**スレッドのイベントのトレースを無効にするパラメーター、 **- hf**ハード ページ フォールトをトレースするパラメーター、および **、cm**トレース パラメーターレジストリのイベント。 この例でも、省略可能な使用 **-ft**パラメーターで、バッファーがいっぱいのときに発生する自動フラッシュをさらに、一定の時間間隔でバッファーをフラッシュする任意のトレース セッションで使用できます。

```
tracelog -start -nothread -hf -cm -ft 2
```

NT Kernel Logger でリアルタイムのトレース セッションを開始することもできます。 次のコマンドは、NT Kernel Logger でリアルタイムのトレース セッションを開始します。 ここでも、前の例のように、"NT Kernel Logger"は、既定のため、セッション名を省略できます。

```
tracelog -start -rt
```

バッファーとタイマー精度をカスタマイズするパラメーターに加え、リアルタイムのトレース セッションのカスタマイズされた NT Kernel Logger のパラメーターを使用することもできます。

フォーマットして、このセッションからのトレース メッセージを表示するには、Tracefmt を使用します。 次のコマンドでは、コマンド プロンプト ウィンドウで、NT Kernel Logger セッションからのトレース メッセージが表示されます。 詳細については、次を参照してください。 [Tracefmt](tracefmt.md)します。

```
tracefmt -rt -display
```

 

 





