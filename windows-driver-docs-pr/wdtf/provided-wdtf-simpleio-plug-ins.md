---
title: 提供されている WDTF シンプル I/O プラグイン
description: 単純な I/O プラグインは、デバイス固有の汎用の I/O 機能を実装する Windows ドライバー テスト フレームワーク (WDTF) に拡張機能です。
ms.assetid: 948E8CF5-24A1-4A7C-BD18-374F989AD053
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a21b6854177caada0cd72e669aa2eff6ad6c3267
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570490"
---
# <a name="provided-wdtf-simple-io-plug-ins"></a>提供されている WDTF シンプル I/O プラグイン


単純な I/O プラグインは、デバイス固有の汎用の I/O 機能を実装する Windows ドライバー テスト フレームワーク (WDTF) に拡張機能です。 テスト対象のデバイスの種類のプラグインが存在する場合、[デバイス基本テスト](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)I/O のテストに WDTF 単純な I/O インターフェイスを使用します。

次の表では、単純な I/O プラグインがあるデバイスの種類を示します。また、デバイスをテストするための特定の要件があるかどうかも示します。 これらは、同じ要件を使用するときに実行する必要があります、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)します。

デバイスの種類が表示されない場合は、1 つを作成を参照してください[WDTF 単純な I/O 操作のプラグインを使用してデバイスの I/O をカスタマイズする方法](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)

## <a name="provided-simple-io-plugins-and-device-requirements-for-testing-and-tips-for-troubleshooting"></a>指定された単純な I/O プラグインとデバイスの要件のテストとトラブルシューティングのヒント


次のセクションでは、単純な I/O プラグインがあるデバイスの種類を示します。セクションでは、デバイスをテストするための特定の要件があるかどうかについても示します。 これらは、同じ要件を使用するときに実行する必要があります、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)します。 セクションでは、テスト エラーのトラブルシューティングを行うし、優先順位を決定する際のヒントも示します。

-   [オーディオ デバイス](#-audio)
-   [Bluetooth デバイス](#-bluetooth)
-   [CD-ROM デバイス](#-cdrom)
-   [ディスク デバイス](#-disk)
-   [デバイスを表示します。](#-display)
-   [GPS デバイス](#-gps)
-   [LAN デバイス](#-lan)
-   [モバイル ブロード バンド デバイス](#-mobile-broadband)
-   [ポータブル デバイス](#-portable-devices)
-   [スマート カード リーダー](#-smartcard)
-   [センサー デバイス](#-sensors)
-   [ボリューム](#-volume)
-   [Web カメラ](#-webcam)
-   [WLAN](#-wlan)
-   [USB コント ローラーと mutt ハブ](#-usb-mutt)

特定の要件であるデバイスの基本的なテストの一覧は、次を参照してください[特定のデバイスの構成要件があるデバイスの基本的なテスト。](#-devfund-test-req)

### <a href="" id="-audio"></a>

| オーディオ |
|-------|
|       |

**要件:**

-   デバイスに少なくとも 1 つレンダリング型のエンドポイント接続 (スピーカー、ヘッドホンなど) が必要です。

-   HDMI オーディオ対応デバイス、HDMI モニターや A などに、デバイスを接続する必要があります対象となるオーディオ デバイスは、HDMI ビデオとオーディオのテストを実行し、オーディオ出力の機能を持つ場合/V レシーバー。

**プラグインの I/O の種類を実行します。**

-   サインにあるチューニング アプローチでは、種類のエンドポイントをレンダリングします。 キャプチャの種類のエンドポイント上のオーディオをキャプチャします。

**テストの失敗をトリアージする方法。**

-   初期のトリアージを実行する HRESULT が失敗していることを確認します。
-   テストが応答していない場合は、根本原因を絞り込むためにターゲット コンピューターのカーネル デバッガーを使用します。
-   トレースを実行します。

    -   カーネル トレースを開始します。

        ``` syntax
        xperf.exe -on LOADER+PROC_THREAD+CSWITCH+DISK_IO+HARD_FAULTS+PROFILE+INTERRUPT+NETWORKTRACE+DPC+Latency+POWER -stackwalk ProcessCreate+ProcessDelete+ImageLoad+ImageUnload+ThreadCreate+ThreadDelete+CSwitch+ReadyThread+Profile+DiskFlushInit+FileFlush+RegFlush+HardFault+VirtualAlloc+VirtualFree -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo_Kernel.etl
        ```

    -   オーディオのトレースを開始します。

        ``` syntax
        xperf.exe -start AudioSimpleIo -on Microsoft-Windows-Audio+a6a00efd-21f2-4a99-807e-9b3bf1d90285:0xffff:0x3 -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo.etl
        ```

    -   テストを実行します。
    -   トレースを停止します。

        ``` syntax
        xperf.exe -stop "NT Kernel Logger" Audio_SimpleIo
        ```

    -   トレースをマージします。

        ``` syntax
        xperf.exe -merge Audio_SimpleIo_Kernel.etl Audio_SimpleIo.etl Audio_SimpleIo _Merged.etl
        ```

    -   Xperf でマージされたトレース ファイルの表示 (**xperfview**)。

### <a href="" id="-bluetooth"></a>

| Bluetooth |
|-----------|
|           |

**要件:**

-   特別な要件はありません。

**プラグインの I/O の種類を実行します。**

-   使用して[ **BluetoothFindFirstDevice 関数**](https://msdn.microsoft.com/library/windows/desktop/aa362784) Bluetooth デバイスが見つかりません。

### <a href="" id="-cdrom"></a>

| CD-ROM ドライブ |
|-------|
|       |

**要件:**

-   ドライブ文字が割り当てられます。
-   メディアでは、デバイスに存在します。
-   ファイルは、挿入、メディア上に存在します。

**プラグインの I/O の種類を実行します。**

-   CD-ROM 上のファイルを検索して、Win32 を使用して読み取り操作を実行します。 [ **ReadFile** ](https://msdn.microsoft.com/library/windows/desktop/aa365467) API。

**テストの失敗をトリアージする方法。**

-   テスト コンピューターに CD または DVD ドライブに移動し、ドライブの内容にアクセスできることを確認します。
-   使用してからの読み取りを実行するには、CD または DVD 上のファイルを CD-Rom の単純な I/O プラグイン検索します。 CD または DVD ディスク上でエンコードされたファイルが含まれることを確認します。
-   この単純な I/O プラグインは、Win32 を使用して[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 [ **WriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa365747)、 [ **ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467)関数。 返されたエラーは、これらの Api からの最も可能性の高い Win32 エラー コードです。

### <a href="" id="-disk"></a>

| Disk |
|------|
|      |

**要件:**

-   ディスクでは、少なくとも 1 つ関連付けられているボリューム文字が割り当てられているドライブがあります。

**プラグインの I/O の種類を実行します。**

-   単純な I/O のためのプラグインを使用して[ボリューム](#-volume)します。

### <a href="" id="-display"></a>

**要件:**


| デバイスを表示します。 |
|-----------------|
|                 |

-   テスト用の特別な要件はありません。

**プラグインの I/O の種類を実行します。**

-   D3DX Api を使用して、グラフィックス アダプターを実行します。

**テストの失敗をトリアージする方法。**

-   使用される Api からエラーを報告するテスト ログを参照します。

### <a href="" id="-gps"></a>

| GPS デバイス (とシステム内の GPS デバイス) |
|------------------------------------------|
|                                          |

**要件:**

-   デバイスは、GPS 信号が適切な場所でテストする必要があります。

**プラグインの I/O の種類を実行します。**

-   I/O のプラグインを使用して[センサー](#-sensors)します。

### <a href="" id="-lan"></a>

| LAN |
|-----|
|     |

**要件:**

-   デバイスでは、IPv6 アドレスがあります。

-   デバイスが IPv6 ゲートウェイ アドレス (それ以外の場合 WDTFREMOTESYSTEM パラメーターを IPv6 アドレスの ping を実行できる NIC のテストとテストに渡す必要があります)。

-   デバイスのネットワーク操作の状態は、ifoperstatusup であります。

-   ネットワーク デバイスは、WWAN または WLAN デバイスではありません。

**プラグインの I/O の種類を実行します。**

-   Ping の IPv6 ネットワーク ゲートウェイのアドレス。

**テストの失敗をトリアージする方法。**

-   既存の IP アドレスがあることを確認します。
-   ゲートウェイの IPv6 IP アドレスがあることを確認します。
-   ゲートウェイの IP アドレスを手動で確認します (ping.exe を使用します)。

### <a href="" id="-mobile-broadband"></a>

| モバイル ブロードバンド |
|------------------|
|                  |

**要件:**

-   テスト用の特別な要件はありません。

**プラグインの I/O の種類を実行します。**

-   使用して[ **IMbnInterface インターフェイス**](https://msdn.microsoft.com/library/windows/desktop/dd430406) GetHomeProvider を呼び出すと[ **IMbnInterface::GetInterfaceCapability メソッド**](https://msdn.microsoft.com/library/windows/desktop/dd323100)、および[**IMbnInterface::GetReadyState メソッド**](https://msdn.microsoft.com/library/windows/desktop/dd323102) Api デバイスの実行にします。

**テストの失敗をトリアージする方法。**

-   MobileBroadbandPlugin は領域を停止する可能性が制限されています。

    -   "MobileBroadbandPlugin:すべてのモバイル ブロード バンド インターフェイスの取得に失敗をしました。"
    -   "MobileBroadbandPlugin:エラーが返されるインターフェイスを取得します。"
    -   "MobileBroadbandPlugin:返される DeviceId を取得します。"
    -   "MobileBroadbandPlugin:インターフェイスの機能を取得するには、エラーが返される"
    -   "MobileBroadbandPlugin:エラーを返しました ReadyState を取得します。"

-   失敗を調査する最適な場所では、デバイスから開始し、準備完了の情報またはデバイスの機能を示すできなかったかどうかを決定します。 OS のトレース ファイルをさらにデバッグするには、収集する必要があります。

    -   コマンドを実行します**netsh トレース開始 wwan\_dbg。**
    -   問題を再現します。
    -   コマンドを実行します**netsh トレースの停止。**

### <a href="" id="-portable-devices"></a>

| ポータブル デバイス |
|------------------|
|                  |

**要件:**

-   デバイスは、フォルダーとファイルを作成できる場所を記憶域コンポーネントにあります。

**プラグインの I/O の種類を実行します。**

-   読み取り、WPD Api を使用して WPD デバイスで記憶域コンポーネントにファイルを書き込みます。

### <a href="" id="-smartcard"></a>

| スマート カード リーダー |
|--------------------|
|                    |

**要件:**

-   デバイスが、Athena T0 テスト カードが挿入されます。

**プラグインの I/O の種類を実行します。**

-   カード リーダーに挿入された Athena T0 カードにデータを読み書きします。

### <a href="" id="-sensors"></a>

| センサー |
|---------|
|         |

**要件:**

-   GPS デバイスは、GPS 信号が適切な場所でテストする必要があります。

### <a href="" id="-volume"></a>

| [ボリューム] |
|--------|
|        |

**要件:**

-   ボリュームには、割り当てられたドライブ文字があります。
-   ボリュームには、5 MB の空き領域があります。
-   ボリュームが書き込み-保護されていません。
-   メディアでは、デバイスに存在します。

**プラグインの I/O の種類を実行します。**

-   WDTF というディレクトリを作成します。\_ボリューム\_IO SimpleIO.tmp と呼ばれるファイルを作成します。 呼び出して、I/O が実行される[ **ReadFile** ](https://msdn.microsoft.com/library/windows/desktop/aa365467)と[ **WriteFile** ](https://msdn.microsoft.com/library/aa365747)このファイルへの Api。

**テストの失敗をトリアージする方法。**

-   テスト コンピューター上のドライブに移動し、ドライブの内容にアクセスできることを確認します。
-   ドライブにファイルを保存しようとしてください。 保存して簡単にアクセスできることを確認します。
-   この単純な I/O プラグインは、Win32 を使用して[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 [ **WriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa365747)、 [ **ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467)関数。 返されたエラーは、これらの Api からの最も可能性の高い Win32 エラー コードです。

### <a href="" id="-webcam"></a>

| Web カメラ |
|--------|
|        |

**要件:**

-   テスト用の特別な要件はありません。

    **注**web カメラ デバイス用のプラグイン単純な I/O では、依存関係を持つ MFPlat.dll ファイルでは、Media Player と関連テクノロジ、Windows 7 の N または Windows 7 KN などが含まれていない Windows のバージョンでは使用できません。 これらのバージョンの Windows で、Media Feature Pack をインストールする必要があります。 Media Feature Pack は、ダウンロードできます。 詳細については、次を参照してください。 [KB 記事 968211](https://go.microsoft.com/fwlink/p/?linkid=266437)します。



**プラグインの I/O の種類を実行します。**

-   ビデオをキャプチャするのにには、メディア ファンデーション インターフェイスを使用します。

### <a href="" id="-wlan"></a>

| WLAN |
|------|
|      |

**要件:**

-   参照してください[デバイス基本テストによってログに記録されるトラブルシューティング WLAN SimpleIO プラグイン エラー](https://go.microsoft.com/fwlink/p/?linkid=309556) HCK ドキュメント。

**プラグインの I/O の種類を実行します。**

-   参照してください[デバイス基本テストによってログに記録されるトラブルシューティング WLAN SimpleIO プラグイン エラー](https://go.microsoft.com/fwlink/p/?linkid=309556) HCK ドキュメント。

**テストの失敗をトリアージする方法。**

-   参照してください[デバイス基本テストによってログに記録されるトラブルシューティング WLAN SimpleIO プラグイン エラー](https://go.microsoft.com/fwlink/p/?linkid=309556) HCK ドキュメント。

### <a href="" id="-usb-mutt"></a>

| USB コント ローラーと mutt ハブ |
|----------------------------------|
|                                  |

**要件:**

-   テスト用の特別な要件はありません。

    デバイスでは、シンボリック リンクがあります。

**プラグインの I/O の種類を実行します。**

-   USB 転送は、Microsoft USB Test Tool (MUTT) デバイスを使用してテストします。 転送の種類の説明は、コントロール、一括でアイソクロナス、割り込み、ストリーム (SuperMUTT は、USB 3.0 コント ローラーに接続されている) 場合のみ

**テストの失敗をトリアージする方法。**

-   テストのログ ファイル内のメッセージを調べることで開始します。
-   さらに、USB 2.0 および 3.0 の USB スタックで Event Tracing for Windows (ETW) を有効にして調査します。
    -   USB 2.0 では、Microsoft Windows USB コア チーム ブログ - を参照してください[、Windows 7 の USB core スタックでの ETW。](https://go.microsoft.com/fwlink/p/?linkid=266442)
    -   USB 3.0 では、Microsoft Windows USB コア チーム ブログ - を参照してください[をキャプチャし、Windows 8 の USB の ETW トレースを読み取る方法。]( https://go.microsoft.com/fwlink/p/?linkid=266443)

## <a name="device-fundamental-tests-that-have-specific-device-configuration-requirements"></a>特定のデバイスの構成要件がある基本的なデバイス テスト


次を実行する前に[デバイス基本テスト](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)要件、特定のデバイスの種類の説明に従って、テスト コンピューター上のデバイスを構成する必要があります。 一覧を参照してください。 [、指定された単純な I/O プラグインとデバイスの要件。](#-provided-io-plugin-list)

-   PCI ルート ポート突然削除を行うテスト (PCI デバイスのみ)
-   Device Path Exerciser テスト (認定)
-   スリープと PNP (無効および有効にする) (認定) の前後に IO の前に
-   プラグ アンド プレイ ドライバーのテスト (認定)
-   同時実行ハードウェアおよびオペレーティング システム (CHAOS) のテスト (認定)
-   (認定) の前後に IO を再インストールします。
-   Device install Check ファイル システムの整合性 (認定) のインストールします。
-   Device install Check 他のデバイスの安定性 (認定) のインストールします。

## <a name="related-topics"></a>関連トピック
[Device Fundamental のテスト](https://msdn.microsoft.com/library/windows/hardware/jj673011)  
[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)  
[コマンド プロンプトから実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)  
[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)  
[デバイス基礎テストのトラブルシューティング](https://msdn.microsoft.com/windows-drivers/develop/troubleshooting_the_device_fundamental_tests)  



