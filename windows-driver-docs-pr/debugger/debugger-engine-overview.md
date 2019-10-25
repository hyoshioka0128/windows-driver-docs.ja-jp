---
title: デバッガーエンジンの概要
description: デバッガーエンジンの概要
ms.assetid: e3cd8a1d-dd07-480b-bc3b-4f6acc647167
keywords:
- デバッガーエンジン
- デバッガーエンジン、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ba51a8bd6dd298a5ea16d1974eb4197bc02412
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837771"
---
# <a name="debugger-engine-overview"></a>デバッガーエンジンの概要


*デバッガーエンジン*(dbgeng .dll) は、一般に*エンジン*と呼ばれます。これは、Microsoft Windows の*ユーザーモード*と*カーネルモード*でデバッグ対象を調べて操作するためのインターフェイスを提供します。

デバッガーエンジンでは、ターゲットの取得、[ブレークポイント](multiprocessor-syntax.md#breakpoints)の設定、[イベント](events.md#events)の監視、[シンボル](symbols.md#symbols)のクエリ、メモリの読み取りと書き込み、およびターゲットの[スレッド](controlling-threads-and-processes.md#threads)と[プロセス](controlling-threads-and-processes.md#processes)の制御を行うことができます。

デバッガーエンジンを使用して、デバッガー拡張ライブラリとスタンドアロンアプリケーションの両方を記述できます。 このようなアプリケーションは、*デバッガーエンジンアプリケーション*と呼ばれます。 デバッガーエンジンのすべての機能を使用するデバッガーエンジンアプリケーションは、*デバッガー*と呼ばれます。 たとえば、WinDbg、CDB、NTSD、および KD は、デバッガーです。デバッガーエンジンには、その機能の中核となる機能が用意されています。

**エンジンの概念:**

[デバッグセッションと実行モデル](debugging-session-and-execution-model.md)

[クライアントオブジェクト](client-objects.md)

[入力と出力](input-and-output.md)

**ターゲットの検証と操作:**

[ターゲット](targets.md)

[イベント](events.md)

[区切り](breakpoints3.md)

[文字](symbols.md)

[メモリ](memory.md)

[スレッドとプロセス](threads-and-processes.md)

### <a name="span-idincomplete_documentationspanspan-idincomplete_documentationspanincomplete-documentation"></a><span id="incomplete_documentation"></span><span id="INCOMPLETE_DOCUMENTATION"></span>不完全なドキュメント

このドキュメントは暫定版であり、現在は不完全です。

ここでまだ説明されていないデバッガーとデバッガーエンジンに関連する多くの概念については、このドキュメントの「[デバッグ技術](debugging-techniques.md)」セクションを参照してください。

デバッガーエンジン API の現在ドキュメントに記載されていない機能の一部を取得するには、 [**execute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-execute)メソッドを使用して個々のデバッガーコマンドを実行します。

 

 





