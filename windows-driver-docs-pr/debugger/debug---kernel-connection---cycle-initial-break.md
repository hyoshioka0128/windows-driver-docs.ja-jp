---
title: デバッグのカーネル接続サイクルの初期の中断
description: デバッグのカーネル接続サイクルの初期の中断
ms.assetid: e4dbb810-d9b3-4721-89ec-af4b5e244cc0
keywords:
- デバッグのカーネル接続サイクルの初期の中断
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4f520cd1c3d1fb6ae882ddacbd0de8d41380050
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374354"
---
# <a name="debug--kernel-connection--cycle-initial-break"></a>Debug | Kernel Connection | Cycle Initial Break (デバッグ | カーネル接続 | 初期の中断を切り替える)


## <span id="ddk_debug_kernel_connection_cycle_initial_break_dbg"></span><span id="DDK_DEBUG_KERNEL_CONNECTION_CYCLE_INITIAL_BREAK_DBG"></span>


をポイント**カーネル接続**順にクリックします**サイクルの初期中断**上、**デバッグ**をデバッガーに自動的に分割、ターゲットの条件を変更するにはメニューコンピューター。

このコマンドは、CTRL + ALT + K キーを押すと同じです。 (することができますも押して CTRL + K KD で)。

このコマンドは、次の 3 つの状態を順番にカーネル デバッガーを実行します。

<span id="No_break"></span><span id="no_break"></span><span id="NO_BREAK"></span>**区切りはありません。**  
ターゲット コンピューターには、キーを押す場合を除き、デバッガーは中断されません[CTRL + BREAK](debug---break.md)またはデバッグ |中断します。

<span id="Break_on_reboot"></span><span id="break_on_reboot"></span><span id="BREAK_ON_REBOOT"></span>**再起動時に中断します。**  
デバッガーは、カーネルが初期化された後、再起動の対象のコンピューターに分割します。 このコマンドは、-b WinDbg から始まる[**コマンド ライン オプション**](windbg-command-line-options.md)します。

<span id="Break_on_first_module_load"></span><span id="break_on_first_module_load"></span><span id="BREAK_ON_FIRST_MODULE_LOAD"></span>**最初のモジュールの読み込み時に中断します。**  
デバッガーは、最初のカーネル モジュールが読み込まれた後、再起動の対象のコンピューターに分割します。 (この操作によってよりも前に発生するブレーク、**の再起動時に中断**状態です)。このコマンドは WinDbg を以降の-d で[**コマンド ライン オプション**](windbg-command-line-options.md)します。

使用すると、**サイクルの初期 Break**コマンドを新しいブレーク状態が表示されます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、関連するコマンドおよび再起動プロセスがデバッガーに与える影響の詳細については、次を参照してください。[クラッシュし、ターゲット コンピューターを再起動](crashing-and-rebooting-the-target-computer.md)します。

 

 





