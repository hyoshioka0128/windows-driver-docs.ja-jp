---
title: ディスプレイ ドライバーのテスト中におけるウォッチドッグ タイマーの無効化
description: ディスプレイ ドライバーのテスト中におけるウォッチドッグ タイマーの無効化
ms.assetid: dc0c9e64-044b-4b2c-8011-9bdbf121307c
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デバッグ
- デバッグ ドライバー WDK Windows 2000 を表示します。
- ウォッチドッグ タイマー WDK Windows 2000 を表示します。
- Windows 2000 の WDK のタイマーを表示します。
- VGA WDK Windows 2000 の表示
- VGA モード WDK Windows 2000 の表示に切り替える
- スレッドのウォッチドッグ タイマー WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 661d919bdfa4fa9d0579f6b4e1866e33b3466522
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578809"
---
# <a name="disabling-the-watchdog-timer-while-testing-display-drivers"></a>ディスプレイ ドライバーのテスト中におけるウォッチドッグ タイマーの無効化


## <span id="ddk_disabling_the_watchdog_timer_while_testing_display_drivers_gg"></span><span id="DDK_DISABLING_THE_WATCHDOG_TIMER_WHILE_TESTING_DISPLAY_DRIVERS_GG"></span>


Microsoft Windows XP SP1 と以降のオペレーティング システムで GDI は、ウォッチドッグ タイマーを使用して、スレッドが、ディスプレイ ドライバーでの実行に費やす時間を監視します。 ウォッチドッグは、時間のしきい値を定義します。 スレッドは、ディスプレイ ドライバーで、しきい値の指定よりも多くの時間を費やして、ウォッチドッグはグラフィックスの VGA モードに切り替えることで回復しようとします。 ウォッチドッグがバグ チェック 0 xea、スレッドを生成、試行が失敗した場合、\_STUCK\_IN\_デバイス\_ドライバー。

デバッグやテスト中には、ソフトウェア エミュレーションを使用するディスプレイ アダプターが最終的に実行するレンダリング場合は、ウォッチドッグ時間のしきい値を大きく必要があります。 それ以外は、エミュレーション描画するコードを大幅にハードウェアよりも遅くがしきい値を超えている可能性があります。

ディスプレイ ドライバーのウォッチドッグ時間のしきい値を指定するには、次のレジストリを作成\_DWORD レジストリ エントリ。

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\BreakPointDelay
```

値を設定**BreakPointDelay**を 10 秒単位で、ウォッチドッグ時間のしきい値。 たとえば、値 200 は、2,000 秒のしきい値を指定します。

アタッチされたデバッガーなしのディスプレイ ドライバーをテストする場合、ウォッチドッグのタイマーを防ぐためのバグ チェックが生成されないことができます。 これを行うには、次のレジストリを作成\_DWORD エントリのレジストリで、その値を 1 に設定。

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\DisableBugCheck
```

このトピックで説明する手法では、デバッグおよびテスト専用です。 作成または変更するドライバーをリリースしない**BreakPointDelay**または**DisableBugCheck**します。

 

 





