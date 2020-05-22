---
title: グローバルロガープロバイダーの例
description: グローバルロガープロバイダーの例
ms.assetid: 06de4d6f-747c-4cf9-a325-2b697b72a1e9
keywords:
- グローバルロガートレースセッション WDK、ログ記録
- ブート時グローバルロガートレースセッション WDK、ログ記録
- ブート中に WDK トレースをログに記録します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323751855948b5ebea5b7dd318267b38e5c58bf9
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769558"
---
# <a name="example-global-logger-provider"></a>例: グローバルロガープロバイダー


次のスクリーンショットは、[グローバルロガートレースセッション](global-logger-trace-session.md)を構成するエントリが含まれている**globallogger**サブキーを示しています。 **Globallogger**サブキーの下には、グローバルロガートレースセッションにログを記録するトレースプロバイダーを表す**controlguid**サブキーがあります。 **Controlguid**サブキーが選択され、サブキーのエントリが右ペインに表示されます。

![windows xp 上のグローバルロガートレースセッションにログを記録するトレースプロバイダーのサブキーのスクリーンショット](images/globallogger.png)

この例では、 **Controlguid**サブキーは TraceDrv サンプルドライバーを表します。 サブキーには、Tracedrv[コントロール GUID](control-guid.md)の d58c126f-b309-11d1-969e-0000f875a5bc という名前が付けられます。 トレースセッションは Windows XP で実行されているため、GUID は中かっこで囲まれていません。

[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)サンプルドライバーは、GitHub で入手できる[Windows driver samples](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

この**Controlguid**サブキーには、**フラグ**エントリと**レベル**エントリが含まれています。 これらのエントリは省略可能であり、その値はプロバイダーによって定義されます。

 

 





