---
title: Te.Service
description: クロス マシンのテストの実行や、RunAs など、一部の TAEF 機能は、Te.Service がインストールされているし、開始する必要があります。
ms.assetid: 2F137748-865C-45de-8F60-B607EEB791C0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a5b22621058cc0ed4132759ab12606a01fc11d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537586"
---
# <a name="teservice"></a>Te.Service


などのいくつか TAEF 機能[クロス マシンのテストの実行](cross-machine-execution.md)と[RunAs](runas.md)Te.Service がインストールされているし、開始する必要があります。

## <a name="span-idinstallingandstartingteservicespanspan-idinstallingandstartingteservicespaninstalling-and-starting-teservice"></a><span id="installing_and_starting_te.service"></span><span id="INSTALLING_AND_STARTING_TE.SERVICE"></span>インストールと起動 Te.Service


-   Wex.Services.exe、Wex.Common.dll、および Wex.Communication.dll が同じディレクトリに存在することを確認します。 既定の場所は、\\テスト\\ランタイム\\WDK の TAEF サブディレクトリ
-   管理者特権でコマンド プロンプトで、次のように入力します。

    ``` syntax
    cd [your Wex.Services.exe directory]
    Wex.Services.exe /install:Te.Service
    sc start Te.Service
    ```

    **注**で CoreSystem Te.Service は、サービスではなくコンソール アプリケーションとして実行できます。




``` syntax
cd [your Wex.Services.exe directory]
Wex.Services.exe /run:Te.Service
```


## <a name="span-idstoppingandremovingteservicespanspan-idstoppingandremovingteservicespanstopping-and-removing-teservice"></a><span id="stopping_and_removing_te.service"></span><span id="STOPPING_AND_REMOVING_TE.SERVICE"></span>停止して Te.Service を削除します。


-   管理者特権でコマンド プロンプトで、次のように入力します。

    ``` syntax
    cd [your Wex.Services.exe directory]
    sc stop Te.Service
    Wex.Services.exe /remove:Te.Service
    ```

    CoreSystem、Te.Service を実行するコンソール アプリケーションを閉じます。

## <a name="span-idprocessorarchitecturessupportedspanspan-idprocessorarchitecturessupportedspanspan-idprocessorarchitecturessupportedspanprocessor-architectures-supported"></a><span id="Processor_Architectures_Supported"></span><span id="processor_architectures_supported"></span><span id="PROCESSOR_ARCHITECTURES_SUPPORTED"></span>サポートされるプロセッサのアーキテクチャ


Te.Service の x86 と x64 の両方のバージョンでは、x86 および x64 の実行中のテストをサポートします。

## <a name="span-idsafemodeinstallationinstructionsspanspan-idsafemodeinstallationinstructionsspanspan-idsafemodeinstallationinstructionsspansafe-mode-installation-instructions"></a><span id="Safe_Mode_Installation_Instructions"></span><span id="safe_mode_installation_instructions"></span><span id="SAFE_MODE_INSTALLATION_INSTRUCTIONS"></span>セーフ モードのインストール手順


既定では、セーフ モードでサービスを開始することはできません。 Sc start Te.Service を実行するときは、次のエラーが表示されます。エラー 1084:セーフ モードでこのサービスを開始することはできず、このエラーは (Windows) の仕様です。

TAEF サービスのセーフ モード機能を有効にする必要があります。

-   Windows のスプラッシュ画面の前に f8 キーを押し、セーフ モードでコンピューターを再起動します。
-   [スタート] ボタンをクリックし、[ファイル名を指定して実行] をクリックして、regedit と入力し、[OK] をクリックします。
-   次のレジストリ サブキーを探してクリックします。
    -   HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\SafeBoot\\(純粋なセーフ モード) の最小限
    -   HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\SafeBoot\\(セーフ モードとネットワーク) のネットワーク
-   [編集] メニューは、[新規] をポイントし、キーをクリックして Te.Service を入力します。
-   既定をダブルクリックし、[サービスを値データ] ボックスに入力し、[ok] をクリックします。
-   レジストリ エディターを終了し、コンピューターを再起動します。
-   昇格特権でコマンド ウィンドウを開きます。
-   Sc start Te.Service を使用するサービスを開始するは正常にようになりました

## <a name="span-idsubscribingtonotificationsspanspan-idsubscribingtonotificationsspanspan-idsubscribingtonotificationsspansubscribing-to-notifications"></a><span id="Subscribing_to_Notifications"></span><span id="subscribing_to_notifications"></span><span id="SUBSCRIBING_TO_NOTIFICATIONS"></span>通知のサブスクライブ


を実行しているサーバー テストを開発する場合は、HandlerEx のコールバック関数と同様の方法では、いくつかサーバー通知のサブスクライブできます。 現時点では、サービスのみ\_コントロール\_SESSIONCHANGE 制御コードがサポートされています。

購読するのには

-   HandlerEx コールバック関数のシグネチャのコールバック関数を定義します。
-   TAEF 通知 API を使用してこの関数を登録します。
-   通知を受信する必要がなくなったときにこの関数の登録を解除します。
-   Te.Common.lib にコードをリンクします。

以下に例を示します。

```cpp
    // define a call back function
    DWORD WINAPI HandlerEx(DWORD dwControl, DWORD dwEventType, LPVOID, LPVOID)
    {
        // Do some work here
        return 0;
    }

    // register the callback function to receive notifications
    TestNotification::RegisterHandler(HandlerEx));
```









