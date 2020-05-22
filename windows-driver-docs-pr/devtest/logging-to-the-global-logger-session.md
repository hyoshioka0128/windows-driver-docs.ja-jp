---
title: グローバル ロガー セッションへのログ記録
description: グローバル ロガー セッションへのログ記録
ms.assetid: 48dfe101-b083-4d70-b85f-2e115f7e1dfa
keywords:
- ブート WDK でのトレース、グローバルロガートレースセッション
- ブート時トレース WDK、グローバルロガートレースセッション
- グローバルロガートレースセッション WDK、ログ記録
- ブート時グローバルロガートレースセッション WDK、ログ記録
- ブート中に WDK トレースをログに記録します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfc2d5eb9506e2c3ce21775f917837a295f9b939
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769636"
---
# <a name="logging-to-the-global-logger-session"></a>グローバル ロガー セッションへのログ記録


システムの起動時に、ドライバーまたはその他のトレースプロバイダーの操作をトレースするには、システムの起動時に実行されるトレースセッションである[グローバルロガートレースセッション](global-logger-trace-session.md)にログを記録するようにドライバーを構成します。 ドライバーは、ソフトウェアのトレース用にインストルメント化する必要があります。

グローバルロガートレースセッションは、プロバイダーに対して有効にする通知を送信しませんが、このセクションで説明されているメソッドは、ドライバーがグローバル Logger セッションへのトレースを有効にするタイミングを決定できるようにするコードをドライバーに追加します。

このメソッドは、windows 2000 以降のバージョンの Windows でサポートされています。 ただし、Windows Vista 以降のバージョンの Windows では、ブートトレースの推奨される方法は、ブートトレース用に特別に設計された新しい機能である自動ロガーを使用することです。 自動ロガーを使用したドライバーのアクティビティのトレースについては、「自動[ロガーセッションの構成と開始](https://docs.microsoft.com/windows/win32/etw/configuring-and-starting-an-autologger-session)」を参照してください。

ここでは、以下の内容について説明します。

[グローバル ロガー セッションにログ記録する方法](how-to-log-to-the-global-logger-session.md)

[例: グローバルロガープロバイダー](example--global-logger-provider.md)

 

 





