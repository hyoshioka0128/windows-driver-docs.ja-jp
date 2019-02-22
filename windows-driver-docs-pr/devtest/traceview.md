---
title: Traceview で
description: Traceview で
ms.assetid: f64ddf90-56b8-4341-8d59-f4d7e3eeddaf
keywords:
- ソフトウェアの WDK、traceview でのトレース
- WDK、traceview でのトレース
- Traceview で WDK
- トレース メッセージを表示します。
- WDK を表示するトレース メッセージ
- WDK、traceview でのセッションをトレースします。
- WDK、セッションのトレースを制御します。
- トレース コンシューマ WDK
- トレース コント ローラー WDK
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: b36bd02fc3054ee81e8f51ceb790ef88bc026b40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553194"
---
# <a name="traceview"></a>Traceview で

## <span id="ddk_traceview_tools"></span><span id="DDK_TRACEVIEW_TOOLS"></span>

Traceview で (TraceView.exe) を構成および制御[トレース セッション](trace-session.md)書式のリアルタイムのトレース セッションからのトレース メッセージを表示し、[トレース ログ](trace-log.md)。

> [!IMPORTANT]
> Traceview でのコマンド ライン インターフェイスは非推奨し、期限切れです。 SDK および WDK に含まれている専用のコマンド ライン ツールを使用する必要があります。[Tracepdb](tracepdb.md)、 [Tracelog](tracelog.md)、および[Tracefmt](tracefmt.md)します。

Traceview では、[トレース コント ローラー](trace-controller.md)と[トレース コンシューマー](trace-consumer.md)します。 Traceview でを使用するには有効にする、構成、開始、更新、およびトレース セッションを停止するにはリアルタイムまたはログに記録されたトレース メッセージを表示するには1 つのディスプレイで別のプロバイダーからのトレース メッセージを結合するにはトレース メッセージを表示し、フィルター処理するにはトレース メッセージをテキスト形式に変換します。

Traceview では、ツールである\\&lt;*プラットフォーム*&gt;サブディレクトリ Windows Driver Kit (WDK) の場所&lt;*プラットフォーム*&gt;、x86、x64、または arm64 などのトレース セッションを実行しているプラットフォームを表します。

このセクションでは、Windows 10 Fall Creators Update (1709) WDK 以降に付属している traceview でのバージョンについて説明します。 Traceview での以前のバージョンは、ここで説明されている機能の多くがない可能性があります。

> [!NOTE]
> Traceview では、Microsoft Windows 7 以降のバージョンの Windows で動作します。

* [Traceview での概要](traceview-overview.md)

[Traceview での使用](using-traceview.md)
