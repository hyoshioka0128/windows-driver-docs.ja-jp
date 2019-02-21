---
title: ロガーがグローバル セッションへのログ記録
description: ロガーがグローバル セッションへのログ記録
ms.assetid: 48dfe101-b083-4d70-b85f-2e115f7e1dfa
keywords:
- WDK の起動中にトレース、グローバル ロガーをトレース セッション
- WDK の起動時にトレース、トレース セッションのグローバル ロガー
- グローバルなロガー トレース セッション WDK、ログ記録
- 起動時のグローバル ログ トレース セッション WDK、ログ記録
- 起動中に WDK トレース ログに記録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b9c5e05575b85cc4502697a4423e98cf51f092d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560784"
---
# <a name="logging-to-the-global-logger-session"></a>ロガーがグローバル セッションへのログ記録


システムの起動中にドライバーやその他のトレース プロバイダーの操作をトレースするには、ドライバーへのログインを構成することによって、[グローバル ロガー トレース セッション](global-logger-trace-session.md)システムのブート時に実行されるトレース セッション。 ドライバーは、ソフトウェア トレースのインストルメント化する必要があります。

トレース セッションを送信しませんグローバル ロガーには、プロバイダーに通知が有効にする、ですが、このセクションで説明されているメソッドは、グローバル ロガー セッションにトレースを有効になっている場合を判断するドライバーをドライバーにコードを追加します。

このメソッドは、Windows 2000 および Windows の以降のバージョンでサポートされます。 ただし、Windows Vista および Windows の以降のバージョンでは、ブート トレースの推奨される方法で、自動ロガー ブート トレース用にデザインされた新しい機能を使用します。 使用してドライバーを自動ロガーのアクティビティ トレースについては、次を参照してください。[構成し、自動ロガー セッションを開始する](https://go.microsoft.com/fwlink/p/?linkid=89723)します。

このセクションの内容:

[グローバルのロガーのセッションにログオンする方法](how-to-log-to-the-global-logger-session.md)

[例:グローバル ロガー プロバイダー](example--global-logger-provider.md)

 

 





