---
title: デバッグ用の GPU スケジューラの動作の変更
description: デバッグ用の GPU スケジューラの動作の変更
ms.assetid: 72eef7bf-b775-4e02-acc6-b745a41c616a
keywords:
- GPU スケジューラ変更 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27e02aeb61026ed4cf029dc42c6cac63abfe389
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363810"
---
# <a name="changing-the-behavior-of-the-gpu-scheduler-for-debugging"></a>デバッグ用の GPU スケジューラの動作の変更


ドライバーのデバッグのために、レジストリを構成することによってグラフィックス処理ユニット (GPU) のスケジューラの動作を変更できます。

有効にまたは GPU スケジューラからの割り込み要求を無効にすることができます (を参照してください[タイムアウト検出と回復](timeout-detection-and-recovery.md)) 次のレジストリ構成を使用しています。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler
KeyValue  : EnablePreemption
ValueType : REG_DWORD
ValueData : 0 to disable preemption, 1 to enable preemption (default).
```

 

 





