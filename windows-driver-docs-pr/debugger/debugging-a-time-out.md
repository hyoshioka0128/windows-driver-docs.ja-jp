---
title: タイムアウトのデバッグ
description: タイムアウトのデバッグ
ms.assetid: 795774da-10fb-4431-908d-94c3baa01132
keywords:
- タイムアウト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52aa4d073c745b40201cbc064fc3c71b0d00f142
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324596"
---
# <a name="debugging-a-time-out"></a>タイムアウトのデバッグ


## <span id="ddk_debugging_time_outs_dbg"></span><span id="DDK_DEBUGGING_TIME_OUTS_DBG"></span>


Windows システムで発生する 2 つの主なタイム アウトがあります。

[リソースのタイムアウト](resource-time-outs.md)(カーネル モード)

[重要なセクション タイムアウト](critical-section-time-outs.md)(ユーザー モード)

多くの場合、これらの問題は、リソースを解放またはコードのセクションの終了に長時間かかってスレッドの問題にすぎません。

小売りシステムのタイムアウト値が十分高く設定こと (true、デッドロックがハングアップだけです)、中断は表示されません。 タイムアウト値は下のレジストリで設定**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control\\SessionManager**します。 整数値では、各タイムアウトの秒数を指定します。

 

 





