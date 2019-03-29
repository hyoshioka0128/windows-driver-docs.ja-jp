---
title: デバッガー エンジン API の概要
description: デバッガー エンジン API の概要
ms.assetid: ea8beca6-93b7-4537-af89-78d599b8b982
keywords:
- デバッガー エンジン API, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d52f3aad2e0363ddba3ad23a1cad7cd46f7cb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577800"
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

**重要な**  、IDebug\*ようなインターフェイス[ **IDebugEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff550550)インターフェイス、like、COM は適切な COM Api ではありません。 これらのインターフェイスをマネージ コードから呼び出すことは、サポートされていないシナリオです。 ガベージ コレクション スレッドの所有権などの問題は、インターフェイスがマネージ コードで呼び出されたときに、システムが不安定につながります。

 

 

 





