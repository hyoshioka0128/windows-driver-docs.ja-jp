---
title: 起動時のグローバル ロガー セッション
description: 起動時のグローバル ロガー セッション
ms.assetid: f1f5bbee-48bd-4e4d-8849-9d21a4f85d44
keywords:
- WDK の起動時にトレース、トレース セッションのグローバル ロガー
- グローバルなロガー トレース セッション WDK
- 起動時のグローバル ログ トレース セッション WDK
- グローバル ロガー トレース セッション WDK、ロガーがグローバル セッションについて
- グローバル ログ セッションに関するグローバル ロガー トレース セッション WDK、ブート時間
- 起動中に、WDK のトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7e2b1dab487326169a72455e4739dfdd0a31ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360404"
---
# <a name="boot-time-global-logger-session"></a>起動時のグローバル ロガー セッション


システムの起動中に Windows のカーネル イベントをトレースするグローバル ロガー トレース セッションを作成することができます。 このメソッドは、の機能を組み合わせて、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)と、カーネルをトレースする、[グローバル ロガー トレース セッション](global-logger-trace-session.md)システムの起動中に発生するイベントをトレースします。

このセクションで説明する手順グローバル ロガー トレース セッションを作成し、特別なレジストリ エントリを追加し、 **EnableKernelFlags**します。 有無、 **EnableKernelFlags**エントリは、有効な値では、グローバルのロガーのトレース セッションを NT Kernel Logger のトレース セッションに変換します。 有効な値**EnableKernelFlags**の値から取得されますが、 **EnableFlags**のメンバー、 [**イベント\_トレース\_プロパティ** ](https://docs.microsoft.com/windows/desktop/ETW/event-trace-properties)構造体。 手順については、「[起動時のグローバルなロガー セッションを作成する方法](how-to-create-a-boot-time-global-logger-session.md)します。

ドライバーなどのトレース プロバイダーは、この種類のセッションにトレース メッセージを記録できます。 この手順はそのために記載されている[ロガーのグローバルなセッションへのログ記録](logging-to-the-global-logger-session.md)します。

このセクションの内容:

[グローバル ロガーの起動時にセッションを作成する方法](how-to-create-a-boot-time-global-logger-session.md)

 

 





