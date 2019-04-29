---
title: トレース レベル
description: トレース レベル
ms.assetid: 7ad3f6ee-61a4-4a0e-ab76-d839ae97a2b3
keywords:
- WDK のトレース レベル
- WDK ソフトウェア トレースのレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ba052f6d7f2762c2a17e11e1c840608e1fbd2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391288"
---
# <a name="trace-level"></a>トレース レベル


トレース レベルのプロパティとしては、[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーまたはユーザー モード アプリケーションなどです。 トレース レベルは、トレース プロバイダーが生成されるイベントを決定します。 通常、トレース レベル (情報、警告、またはエラー)、イベントの重大度を表しますが、トレース プロバイダーには、トレース メッセージを生成するための任意の条件を表すために定義できます。

異なり[トレース フラグ](trace-flags.md)でのトレース プロバイダーによって定義されている、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)構造体、トレース レベルが Evntrace.h、パブリック ヘッダー ファイルで定義されています。 ただし、トレース プロバイダーは、レベルを解釈し、その効果を決定します。

[コンシューマーのトレース](trace-consumer.md)など[Tracelog](tracelog.md)と[traceview で](traceview.md)、トレース レベルにプロバイダーに渡す、 *EnableLevel*のパラメーター、 **EnableTrace**関数。 について**EnableTrace**、Microsoft Windows SDK のドキュメントを参照してください。

トレース プロバイダーの開発者は、カスタマイズされたトレース関数を作成もできます (代替[ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)) のトレース メッセージを生成するための条件として、トレース レベルが含まれる。 手順については、次を参照してください[DoTraceMessage をカスタマイズできますか?。](can-i-customize-dotracemessage-.md)

トレース セッションを実行するときに、ユーザーは、セッション中にメッセージが生成されますを決定するのにトレース レベルを使用できます。 [コンシューマーのトレース](trace-consumer.md)など[Tracelog](tracelog.md)と[traceview で](traceview.md)ユーザーは、パラメーターとトレース セッションで、プロバイダーごとに、トレース フラグとトレース レベルを選択するオプションを設定します。

トレース フラグのようなユーザーはトレース プロバイダーを再有効化してトレース セッションの実行中にトレース レベルを変更できます。

 

 





