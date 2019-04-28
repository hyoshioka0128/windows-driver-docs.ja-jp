---
title: トレース メッセージ一覧
description: トレース メッセージ一覧
ms.assetid: 32dcd09d-1046-4785-91bc-ccdd79452c7d
keywords:
- Traceview で WDK、ウィンドウ
- トレース メッセージの一覧 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a75ff6e1d6490d3cf1d8b2ab41f533e05ff642a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369743"
---
# <a name="trace-message-lists"></a>トレース メッセージ一覧


Traceview では、いずれかが表示されます*トレース メッセージ一覧*各トレース セッションまたはトレース ログ、[トレース セッション リスト](trace-session-list.md)します。 トレース メッセージの一覧など、トレース セッションの最初に開始日、空で、または多数のトレース メッセージを含めることができます。

次のスクリーン ショットには、2 つの既存のログを表示するトレース セッションの一覧が表示されます: WDK に含まれているサンプル トレースでインストルメント化されたドライバーである、Tracedrv 用とに 1 つずつ、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。 トレース セッションごとに 1 つのトレース メッセージの一覧があります。

![tracedrv と nt カーネル ロガーのトレース セッション ログを表示するトレース セッションの一覧のスクリーン ショット](images/traceview-multilog.png)

各トレース メッセージの一覧の左の境界線にセッション Id を使用して、トレース メッセージの一覧に、トレース セッションを関連付けるのに役立ちます。 この例では、「ID 0」の名前が、上位トレース メッセージ一覧はセッション 0 の場合に対応*LogSession0*; セッション トレース セッションの一覧で、Tracedrv.etl ログを表示します。

セッション 1, LogSession1; に対応する下部にある「ID 1」の名前が、トレース メッセージの一覧このセッション トレース セッションの一覧で NTKernelLogger.etl ログを表示します。

次のトピックでは、内容とトレース メッセージの一覧の機能について説明します。

[トレース メッセージの一覧の列](trace-message-list-columns.md)

[トレース メッセージの一覧の機能](trace-message-list-features.md)

 

 





