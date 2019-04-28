---
title: デバッガー エンジンの概要
description: デバッガー エンジンの概要
ms.assetid: e3cd8a1d-dd07-480b-bc3b-4f6acc647167
keywords:
- デバッガー エンジン
- デバッガー エンジン, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 092f1fad8cc839e4727b0c6f53c8c29b3b0039b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368124"
---
# <a name="debugger-engine-overview"></a>デバッガー エンジンの概要


*デバッガー エンジン*(DbgEng.dll) は通常と呼ばれる、*エンジン*、調べたりでデバッグ ターゲットを操作するためのインターフェイスを提供します*ユーザー モード*と*カーネル モード*Microsoft Windows にします。

デバッガー エンジンは、ターゲットを取得できる設定[ブレークポイント](multiprocessor-syntax.md#breakpoints)、モニター[イベント](events.md#events)、クエリ[シンボル](symbols.md#symbols)、読み取りおよび書き込みメモリ、およびコントロールに[スレッド](controlling-threads-and-processes.md#threads)と[プロセス](controlling-threads-and-processes.md#processes)をターゲットにします。

デバッガー エンジンを使用して、デバッガーの拡張機能ライブラリとスタンドアロン アプリケーションの両方を記述することができます。 このようなアプリケーションと呼びます*エンジン アプリケーションのデバッガー*します。 デバッガー エンジンのすべての機能を使用するデバッガー エンジン アプリケーションを呼び出す、*デバッガー*します。 たとえば、WinDbg、CDB、NTSD、および KD はデバッガーです。デバッガー エンジンは、その機能のコアを提供します。

**エンジンの概念:**

[デバッグ セッションと実行モデル](debugging-session-and-execution-model.md)

[クライアント オブジェクト](client-objects.md)

[入力と出力](input-and-output.md)

**調べると、ターゲットの操作:**

[ターゲット](targets.md)

[イベント](events.md)

[[ブレークポイント]](breakpoints3.md)

[シンボル](symbols.md)

[メモリ](memory.md)

[スレッドとプロセス](threads-and-processes.md)

### <a name="span-idincompletedocumentationspanspan-idincompletedocumentationspanincomplete-documentation"></a><span id="incomplete_documentation"></span><span id="INCOMPLETE_DOCUMENTATION"></span>不完全なドキュメント

これは、ドキュメントは暫定版と、完全ではありません。

ここでまだ記載されていないのデバッガーとデバッガー エンジンに関連する多く概念の参照、[のデバッグ技術](debugging-techniques.md)このドキュメントの「します。

デバッガー エンジン API の現在文書化されていない機能の一部を取得するには、使用、 [ **Execute** ](https://msdn.microsoft.com/library/windows/hardware/ff543208)個々 のデバッガー コマンドを実行するメソッド。

 

 





