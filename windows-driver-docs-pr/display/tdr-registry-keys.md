---
title: タイムアウト検出と復旧 (TDR) レジストリ キー
description: 次の TDR (タイムアウト検出と回復)-関連のレジストリ キーは、ディスプレイ ドライバーの開発テストやデバッグのためだけにします。
ms.assetid: 77b8b2aa-0821-4297-a1e4-57894bd4181f
keywords:
- TDR (タイムアウト検出と回復)
- WDK の表示の開発
ms.date: 10/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1130c27a3109ed22211b9fb62e6f6e86d5fcfc01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362714"
---
# <a name="timeout-detection-and-recovery-tdr-registry-keys"></a>タイムアウト検出と復旧 (TDR) レジストリ キー

次の TDR (タイムアウト検出と回復) を使用する-関連するレジストリ キーは、テストまたはデバッグ目的でのみです。 つまりする必要がありますいないェケェ ・ ケェルェニェホォウーォノェマ対象となるテストやデバッグを外部にあるアプリケーション。

-   **TdrLevel**

    最初のレベルの回復を指定します。 既定値は、タイムアウト時に回復する (**TdrLevelRecover**)。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrLevel
    ValueType : REG_DWORD
    ValueData : TdrLevelOff (0) - Detection disabled 
     TdrLevelBugcheck (1) - Bug check on detected timeout, for example, no recovery.
     TdrLevelRecoverVGA (2) - Recover to VGA (not implemented).
     TdrLevelRecover (3) - Recover on timeout. This is the default value.
    ```

-   **TdrDelay**

    GPU が GPU スケジューラからの切断要求を遅らせることができる秒数を指定します。 これは、実質的に、タイムアウトしきい値です。 既定値は、2 秒です。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrDelay
    ValueType : REG_DWORD
    ValueData : Number of seconds to delay. 2 seconds is the default value.
    ```

-   **TdrDdiDelay**

    オペレーティング システムでドライバーのままにするスレッドは、秒数を指定します。 指定した後は、オペレーティング システムのバグ チェック ビデオ、コードを使用してコンピューター\_TDR\_障害 (0x116)。 既定値は、5 秒です。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrDdiDelay
    ValueType : REG_DWORD
    ValueData : Number of seconds to leave the driver. 5 seconds is the default value.
    ```

-   **TdrTestMode**

    予約済み。 使わないでください。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrTestMode
    ValueType : REG_DWORD
    ValueData : Do not use.
    ```

-   **TdrDebugMode**

    TDR プロセスのデバッグに関連する動作を指定します。 既定値は TDR\_デバッグ\_モード\_回復\_いいえ\_プロンプトを示す、デバッガーを中断しないようにします。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrDebugMode
    ValueType : REG_DWORD
    ValueData : TDR_DEBUG_MODE_OFF (0) - Break to kernel debugger before the recovery to allow investigation of the timeout. 
     TDR_DEBUG_MODE_IGNORE_TIMEOUT (1) - Ignore any timeout.
     TDR_DEBUG_MODE_RECOVER_NO_PROMPT (2) - Recover without breaking into the debugger. This is the default value.
     TDR_DEBUG_MODE_RECOVER_UNCONDITIONAL (3) - Recover even if some recovery conditions are not met (for example, recover on consecutive timeouts).
    ```

-   **TdrLimitTime**

    Windows Server 2008 以降のバージョンと Windows Vista Service Pack 1 (SP1)、以降のバージョンでサポートされています。

    既定の時間を指定します TDRs の特定の数 (で指定された、 **TdrLimitCount**キー)、コンピューターがクラッシュせず許可されます。 既定値は、60 秒です。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrLimitTime
    ValueType : REG_DWORD
    ValueData : Number of seconds before crashing. 60 seconds is the default value.
    ```

-   **TdrLimitCount**

    Windows Server 2008 以降のバージョンと Windows Vista Service Pack 1 (SP1)、以降のバージョンでサポートされています。

    指定した時間中に許可されている TDRs (0x117) の既定の数を指定します、 **TdrLimitTime**コンピューターがクラッシュせずキー。 既定値は 5 です。

    ```registry
    KeyPath   : HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers
    KeyValue  : TdrLimitCount
    ValueType : REG_DWORD
    ValueData : Number of TDRs before crashing. The default value is 5.
    ```

