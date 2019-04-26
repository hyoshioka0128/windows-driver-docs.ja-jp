---
title: トレース フラグ
description: トレース フラグ
ms.assetid: a94159ab-ce21-4604-beb8-ee01e333505e
keywords:
- WDK のトレース フラグ
- WDK ソフトウェア トレースのフラグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fad3585b2e31b2d95eb0b9a0e52ece0de633d5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339723"
---
# <a name="trace-flags"></a>トレース フラグ


トレース フラグは、のプロパティを[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーまたはユーザー モード アプリケーションなどです。 これらのフラグは、トレース プロバイダーが生成されるイベントを決定します。 プロバイダーは、メッセージを生成するための条件としてフラグを解釈します。

通常、フラグがしだいに詳細レポートのレベルを表す、プロバイダーは、トレース メッセージを生成するための任意の条件を表すフラグを使用することができます。

トレース プロバイダーでは、各フラグを定義、WPP で\_定義\_ビット要素の[WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)構造体。 Windows ソフトウェア トレース プリプロセッサ (WPP) は、1 から始まる、構造体に出現する順序で要素をビット値を割り当てます。

実行するときに、[トレース セッション](trace-session.md)、トレース フラグを使用して、確認するメッセージがセッション中に生成されます。 [コンシューマーのトレース](trace-consumer.md)など[Tracelog](tracelog.md)と[traceview で](traceview.md)、ユーザーは、パラメーターとトレース フラグを選択するオプションを設定と[トレース レベル](trace-level.md)ごとトレース セッションのプロバイダー。

トレース プロバイダーを再有効化してトレース セッションの実行中には、トレース フラグを変更できます。

 

 





