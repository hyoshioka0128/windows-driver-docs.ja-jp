---
title: ディスプレイ ドライバーのタイムアウト回復の無効化
description: ディスプレイ ドライバーのタイムアウト回復の無効化
ms.assetid: 71fa0273-be21-4603-8491-09078a38cdf2
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、タイムアウトの回復
- タイムアウト recovery WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d81deeb25086e6847ef7cecfefe3423be7b9db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362822"
---
# <a name="disabling-timeout-recovery-for-display-drivers"></a>ディスプレイ ドライバーのタイムアウト回復の無効化


Microsoft Windows XP SP1 と以降のオペレーティング システムで GDI は、ウォッチドッグ タイマーを使用して、スレッドが、ディスプレイ ドライバーでの実行に費やす時間を監視します。 ウォッチドッグは、時間のしきい値を定義します。 スレッドは、ディスプレイ ドライバーで、しきい値の指定よりも多くの時間を費やして、ウォッチドッグはグラフィックスの VGA モードに切り替えることで回復しようとします。 ウォッチドッグがバグ チェック 0 xea、スレッドを生成、試行が失敗した場合、\_STUCK\_IN\_デバイス\_ドライバー。

タイムアウト回復用コードは複雑なためディスプレイ ドライバーと非互換性をしまう可能性があります。 互換性の問題を解決するには、タイムアウトの回復を無効にできます。

タイムアウトの回復を無効にするには、次のレジストリを作成\_DWORD エントリのレジストリで、その値を 0 に設定します。

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\EaRecovery
```

 

 





