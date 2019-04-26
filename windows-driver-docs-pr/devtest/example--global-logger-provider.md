---
title: グローバルのログ プロバイダーの例
description: グローバルのログ プロバイダーの例
ms.assetid: 06de4d6f-747c-4cf9-a325-2b697b72a1e9
keywords:
- グローバルなロガー トレース セッション WDK、ログ記録
- 起動時のグローバル ログ トレース セッション WDK、ログ記録
- 起動中に WDK トレース ログに記録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0da3421309af849261e51f07ac3f77c518ad13bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344798"
---
# <a name="example-global-logger-provider"></a>以下に例を示します。グローバル ロガー プロバイダー


次のスクリーン ショットは、 **GlobalLogger**サブキーで、構成エントリが含まれる、[グローバル ロガー トレース セッション](global-logger-trace-session.md)します。 下、 **GlobalLogger**サブキーが、 **ControlGUID**サブキーをグローバル ロガーのトレース セッションを記録するトレース プロバイダーを表します。 **ControlGUID**サブキーが選択されているし、右側のウィンドウで、サブキー、エントリが表示されます。

![windows xp でグローバル ロガー トレース セッションを記録するトレース プロバイダーのサブキーのスクリーン ショット](images/globallogger.png)

この例で、 **ControlGUID**サブキーが TraceDrv サンプル ドライバーを表します。 サブキーの名前は、Tracedrv の[コントロール GUID](control-guid.md)、d58c126f b309-11 d 0000f875a5bc 969e 1。 トレース セッションが Windows XP で実行しているため、GUID は中かっこで囲まれていません。

[TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)サンプル ドライバーが表示されます、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリの GitHub で入手できます。

これは、 **ControlGUID**サブキーが含まれています、**フラグ**エントリと**レベル**エントリ。 これらのエントリはオプションであり、値は、プロバイダーによって定義されます。

 

 





