---
title: トレース ログ
description: トレース ログ
ms.assetid: c15fcfec-b584-4cb8-bc48-9ff122f5a8fc
keywords:
- イベント トレース ログは、WDK
- ログ ファイルの WDK トレース
- .etl ファイル
- etl ファイル
- WDK のトレース ログ
- トレース メッセージを格納します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a6aabdf804d313c7def6a33ae4c960a4e44802f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380247"
---
# <a name="trace-log"></a>トレース ログ


## <span id="ddk_trace_log_tools"></span><span id="DDK_TRACE_LOG_TOOLS"></span>


イベント トレース ログ (.etl) ファイルとも呼ばれる、*トレース ログ*、1 つまたは複数の中に生成されたトレース メッセージを格納[トレース セッション](trace-session.md)します。

システムが最初に、トレースを格納メッセージ[トレース プロバイダー](trace-provider.md)トレース セッションのバッファーで生成し、それらに直接配信、[トレース コンシューマー](trace-consumer.md)またはトレース ログに書き込みます。

メッセージが大量のディスク領域を占有できるため、トレース ログに保存するバイナリ形式に圧縮。 トレース コンシューマがトレース プロバイダーによって提供される情報を使用して、メッセージを読み取り、(、 *FormatString*パラメーター、 [ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロ) を解析し、書式設定メッセージが読みやすいようにします。 トレース コンシューマーでこの情報を見つけることができます、 [PDB シンボル ファイル](pdb-symbol-files.md)または[トレース メッセージのフォーマット ファイル](trace-message-format-file.md)プロバイダー。

 

 





