---
title: TraceView のコマンド ライン インターフェイス
description: TraceView のコマンド ライン インターフェイス
ms.assetid: da38268f-ebdf-468c-95fe-500ba747047a
keywords:
- Traceview で WDK、コマンド ライン インターフェイス
- WDK traceview でのコマンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2e74c971fc34d4d7da368ccf676d9d847b54c4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369620"
---
# <a name="traceview-command-line-interface"></a>TraceView のコマンド ライン インターフェイス

> [!IMPORTANT]
> Traceview でのコマンド ライン インターフェイスをすべてのスタンドアロン ツールで使用できる最新の更新プログラムにするにはありません。 使用することをお勧め[Tracelog](tracelog.md)、 [Tracefmt](tracefmt.md)、および[Tracepdb](tracepdb.md)代わりにします。

Traceview でのコマンド ライン インターフェイスでは、コマンド プロンプト ウィンドウから traceview で機能を制御することができます。

コマンド ライン インターフェイスでは、3 つの部分があります。

<span id="TraceView_Control_Commands"></span><span id="traceview_control_commands"></span><span id="TRACEVIEW_CONTROL_COMMANDS"></span>[**Traceview で管理コマンド**](traceview-control-commands.md)  
管理、[トレース コント ローラー](trace-controller.md) traceview での機能です。 似ています[Tracelog](tracelog.md)します。

<span id="TraceView_-process"></span><span id="traceview_-process"></span><span id="TRACEVIEW_-PROCESS"></span>[**Traceview で-プロセス**](traceview--process.md)  
管理、[トレース コンシューマー](trace-consumer.md) traceview での機能です。 似ています[Tracefmt](tracefmt.md)します。

<span id="TraceView_-parsepdb"></span><span id="traceview_-parsepdb"></span><span id="TRACEVIEW_-PARSEPDB"></span>[**Traceview で parsepdb**](traceview--parsepdb.md)  
作成、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース メッセージを抽出することからの指示を書式設定、 [PDB シンボル ファイル](pdb-symbol-files.md)します。 似ています[Tracepdb](tracepdb.md)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview でウィンドウと traceview でコマンド ライン インターフェイスは、独立して動作し、同じ意味で使用することはできません。 Traceview でのコマンド ライン インターフェイスを使用して、traceview でウィンドウを使用して開始したトレース セッションを制御することができますが、traceview でコマンド ライン インターフェイスを使用して開始したコントロールのトレース セッションを traceview でウィンドウを使用することはできません。

コマンド プロンプト ウィンドウで traceview でコマンドを送信するときに、traceview では、その出力の新しいコマンド プロンプト ウィンドウを開きます。 その他の windows を抑制することはできません。
