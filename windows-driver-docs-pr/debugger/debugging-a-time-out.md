---
title: タイムアウトのデバッグ
description: タイムアウトのデバッグ
ms.assetid: 795774da-10fb-4431-908d-94c3baa01132
keywords:
- タイムアウト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52aa4d073c745b40201cbc064fc3c71b0d00f142
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572070"
---
# <a name="debugging-a-time-out"></a>タイムアウトのデバッグ


## <span id="ddk_debugging_time_outs_dbg"></span><span id="DDK_DEBUGGING_TIME_OUTS_DBG"></span>


Windows システムで発生する 2 つの主なタイム アウトがあります。

[リソースのタイムアウト](resource-time-outs.md)(カーネル モード)

[重要なセクション タイムアウト](critical-section-time-outs.md)(ユーザー モード)

多くの場合、これらの問題は、リソースを解放またはコードのセクションの終了に長時間かかってスレッドの問題にすぎません。

小売りシステムのタイムアウト値が十分高く設定こと (true、デッドロックがハングアップだけです)、中断は表示されません。 タイムアウト値は下のレジストリで設定**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\sessionmanager で致命的**します。 整数値では、各タイムアウトの秒数を指定します。

 

 





