---
title: デバッガーエンジン API の概要
description: デバッガーエンジン API の概要
ms.assetid: ea8beca6-93b7-4537-af89-78d599b8b982
keywords:
- デバッガーエンジン API, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25a3754cffd481507e310815fb5eea6f97510fea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837775"
---
# <a name="debugger-engine-api-overview"></a>デバッガーエンジン API の概要


## <span id="ddk_debugger_engine_overview_dbx"></span><span id="DDK_DEBUGGER_ENGINE_OVERVIEW_DBX"></span>


このセクションの内容は次のとおりです。

[エンジンとの対話](interacting-with-the-engine.md)

[入力と出力の使用](using-input-and-output.md)

[イベントの監視](monitoring-events.md)

[ブレークポイントの使用](using-breakpoints2.md)

[メモリアクセス](memory-access.md)

[スタックトレースを調べています](examining-the-stack-trace.md)

[制御 (スレッドとプロセスを)](controlling-threads-and-processes.md)

[シンボルの使用](using-symbols.md)

[ソースファイルの使用](using-source-files.md)

[ターゲットへの接続](connecting-to-targets.md)

[ターゲット情報](target-information.md)

[ターゲットの状態](target-state.md)

[拡張機能と拡張関数の呼び出し](calling-extensions-and-extension-functions.md)

[命令のアセンブルと逆アセンブル](assembling-and-disassembling-instructions.md)

**重要**  idebug\* インターフェイスなど[**のインターフェイス (** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) com など) は適切な com api ではありません。 マネージコードからこれらのインターフェイスを呼び出すことは、サポートされていないシナリオです。 ガベージコレクションやスレッド所有権などの問題により、マネージコードを使用してインターフェイスを呼び出すと、システムが不安定になる可能性があります。

 

 

 





