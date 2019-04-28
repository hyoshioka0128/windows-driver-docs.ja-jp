---
title: EA 回復の無効化
description: EA 回復の無効化
ms.assetid: a414f1b0-acfc-4617-bf68-202bdef829ce
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デバッグ
- デバッグ ドライバー WDK Windows 2000 を表示します。
- EA recovery WDK Windows 2000 の表示
- 無効になっている EA recovery WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30b288731f61677866225bedd5466c4f2012885
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367382"
---
# <a name="disabling-ea-recovery"></a>EA 回復の無効化


## <span id="ddk_disabling_ea_recovery_gg"></span><span id="DDK_DISABLING_EA_RECOVERY_GG"></span>


Microsoft Windows XP SP1 と以降のオペレーティング システムで GDI は、ウォッチドッグ タイマーを使用して、スレッドが、ディスプレイ ドライバーでの実行に費やす時間を監視します。 ウォッチドッグは、時間のしきい値を定義します。 スレッドは、ディスプレイ ドライバーで、しきい値の指定よりも多くの時間を費やして、ウォッチドッグはグラフィックスの VGA モードに切り替えることで回復しようとします。 ウォッチドッグがバグ チェック 0 xea、スレッドを生成、試行が失敗した場合、\_STUCK\_IN\_デバイス\_ドライバー。

回復する前に、ウォッチドッグは、コンピューターに接続されているすべてのデバッガーが中断されます。 無効になっている最初の EA リカバリーがある限り、--コードをデバッグできます。

Windows XP SP1 では、グローバル変数を設定して EA の回復を無効に**WdDisableRecovery**、ある*watchdog.sys*1 にします。 これを行うには、次を入力することができます**WinDbg**コマンド。

```cmd
ed watchdog!WdDisableRecovery 1
```

Microsoft Windows Server 2003 では、グローバル変数を設定して EA の回復を無効に**VpDisableRecovery**、ある*videoprt.sys*1 にします。 これを行うには、次を入力することができます**WinDbg**コマンド。

```cmd
ed videoprt!VpDisableRecovery 1
```

EA の回復を無効にした後、コードがループ思わ、ディスプレイ ドライバーにブレークポイントを設定し、実行を再開します。

 

 





