---
title: 起動中のトレース
description: 起動中のトレース
ms.assetid: 79594c33-5755-4484-aaf5-ac409b05ddcc
keywords:
- ソフトウェアトレース WDK、ブート中
- ブート中の WDK のトレース
- ブート時のトレース (WDK)
- カーネルモードソフトウェアトレース WDK
- ブート時トレース WDK, ブート時トレースについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1467b6ff7bafef952a15ecac7473e5b95222349e
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769720"
---
# <a name="tracing-during-boot"></a>起動中のトレース


Windows のブートプロセス中に、Microsoft Windows のソフトウェアトレースコンポーネントの機能を使用して、Windows カーネルの動作、およびドライバーやその他のトレースプロバイダーのアクティビティをトレースできます。

このセクションでは、新しいツールについては説明しません。 代わりに、既存のソフトウェアトレースツールと Windows イベントトレーシング (ETW) 機能を使用してこの重要なタスクを実行する方法について説明します。

このセクションでは、起動時のトレースの次の方法について説明します。

-   [起動時のグローバル ロガー セッション](boot-time-global-logger-session.md)

    [グローバルロガートレースセッション](global-logger-trace-session.md)を[NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)に変換することによって、ブートプロセス中の Windows カーネルアクティビティをトレースします。

-   [グローバル ロガー セッションへのログ記録](logging-to-the-global-logger-session.md)

    ブート中にドライバーまたはその他のトレースプロバイダーのアクティビティをトレースします。 プロバイダーはトレース用にインストルメント化する必要があります。 一度に実行できるグローバル Logger セッションは1つだけです。 この機能は、Windows 2000 以降のバージョンの Windows で使用できます。

-   **ロガー**

    これは、ブート中にドライバーまたはその他のトレースプロバイダーのアクティビティをトレースするために推奨される方法です。 プロバイダーはトレース用にインストルメント化する必要があります。 自動ロガーは、ドライバーへのコールバック通知を提供します。 複数の AutoLoggers を同時に実行できます。 この機能は、Windows Vista 以降のバージョンの Windows で使用できます。 自動ロガーを使用したドライバーのアクティビティのトレースについては、「自動[ロガーセッションの構成と開始](https://docs.microsoft.com/windows/win32/etw/configuring-and-starting-an-autologger-session)」を参照してください。

グローバルロガートレースセッションを使用する場合は、制限事項を把握していることを確認してください。 詳細については、「グローバルロガートレースセッションの制限事項」を参照してください。

 

 





