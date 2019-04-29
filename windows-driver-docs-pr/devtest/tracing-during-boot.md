---
title: 起動中のトレース
description: 起動中のトレース
ms.assetid: 79594c33-5755-4484-aaf5-ac409b05ddcc
keywords:
- ソフトウェアの起動中に、WDK のトレース
- 起動中に、WDK のトレース
- 起動時にトレース WDK
- WDK をトレースするカーネル モード ソフトウェア
- 起動時にトレース WDK、ブート時のトレースについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9997e3cf374f3f79b81525e550c7243f5bea42d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392687"
---
# <a name="tracing-during-boot"></a>起動中のトレース


Windows のブート プロセス中に、Windows カーネルのアクティビティおよびドライバーと他のトレース プロバイダーのアクティビティを追跡するのに、Microsoft Windows でのトレースのソフトウェア コンポーネントの機能を使用できます。

このセクションでは、新しいツールについて説明します。 代わりに、既存のソフトウェア トレース ツールと Event Tracing for Windows (ETW) の機能を使用して、この重要なタスクを実行する方法について説明します。

このセクションでは、ブート中にトレースの次の方法について説明します。

-   [起動時のグローバル ロガー セッション](boot-time-global-logger-session.md)

    Windows カーネルのアクティビティを変換することで、ブート プロセス中にトレースを[グローバル ロガー トレース セッション](global-logger-trace-session.md)を[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

-   [ロガーがグローバル セッションへのログ記録](logging-to-the-global-logger-session.md)

    起動中に、ドライバーやその他のトレース プロバイダーのアクティビティをトレースします。 プロバイダーは、トレースのインストルメント化する必要があります。 一度に 1 つだけのグローバル ログ セッションを実行できます。 この機能は、Windows 2000 以降のバージョンの Windows で使用できます。

-   **AutoLogger**

    これは、起動中にドライバーやその他のトレース プロバイダーのアクティビティをトレースするための推奨される方法です。 プロバイダーは、トレースのインストルメント化する必要があります。 自動ロガーは、ドライバーにコールバック通知を提供します。 複数 AutoLoggers を同時に実行できます。 この機能は、Windows Vista および Windows の以降のバージョンで使用できます。 使用してドライバーを自動ロガーのアクティビティ トレースについては、次を参照してください。[構成し、自動ロガー セッションを開始する](https://go.microsoft.com/fwlink/p/?linkid=89723)します。

グローバル ロガーのトレース セッションを使用する場合は、制限事項を認識していることを確認します。 については、グローバルのロガーのトレース セッションの制限事項を参照してください。

 

 





