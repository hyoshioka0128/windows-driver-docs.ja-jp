---
title: デバッガー エンジン API の概要
description: デバッガー エンジン API の概要
ms.assetid: ea8beca6-93b7-4537-af89-78d599b8b982
keywords:
- デバッガー エンジン API, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19356776e5b311e00b5c21c167866b16ee685602
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366946"
---
# <a name="debugger-engine-api-overview"></a>デバッガー エンジン API の概要


## <span id="ddk_debugger_engine_overview_dbx"></span><span id="DDK_DEBUGGER_ENGINE_OVERVIEW_DBX"></span>


このセクションの内容:

[エンジンと対話します。](interacting-with-the-engine.md)

[入力と出力を使用します。](using-input-and-output.md)

[イベントの監視](monitoring-events.md)

[ブレークポイントの使用](using-breakpoints2.md)

[メモリへのアクセス](memory-access.md)

[スタック トレースを調べる](examining-the-stack-trace.md)

[スレッドとプロセスを制御します。](controlling-threads-and-processes.md)

[シンボルを使用します。](using-symbols.md)

[ソース ファイルを使用します。](using-source-files.md)

[ターゲットへの接続](connecting-to-targets.md)

[ターゲットの情報](target-information.md)

[対象の状態](target-state.md)

[拡張機能と拡張機能の関数の呼び出し](calling-extensions-and-extension-functions.md)

[アセンブルおよび逆アセンブル](assembling-and-disassembling-instructions.md)

**重要な**  、IDebug\*ようなインターフェイス[ **IDebugEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイス、like、COM は適切な COM Api ではありません。 これらのインターフェイスをマネージ コードから呼び出すことは、サポートされていないシナリオです。 ガベージ コレクション スレッドの所有権などの問題は、インターフェイスがマネージ コードで呼び出されたときに、システムが不安定につながります。

 

 

 





