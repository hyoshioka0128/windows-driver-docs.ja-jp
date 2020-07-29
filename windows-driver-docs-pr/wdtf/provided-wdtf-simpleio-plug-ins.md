---
title: 提供されている WDTF シンプル I/O プラグイン
description: 単純な i/o プラグインは、デバイス固有の汎用 i/o 機能を実装する Windows Driver Test Framework (WDTF) の拡張機能です。
ms.assetid: 948E8CF5-24A1-4A7C-BD18-374F989AD053
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ace73923487e0e97601732548056aa2cbdabf0b
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264459"
---
# <a name="provided-wdtf-simple-io-plug-ins"></a>提供されている WDTF シンプル I/O プラグイン

単純な i/o プラグインは、デバイス固有の汎用 i/o 機能を実装する Windows Driver Test Framework (WDTF) の拡張機能です。 テスト対象のデバイスの種類に対してプラグインが存在する場合、[デバイスの基本テスト](https://docs.microsoft.com/windows-hardware/drivers)では、Wdtf Simple i/o インターフェイスを使用して i/o をテストします。

次の表は、単純な i/o プラグインを持つデバイスの種類を示しています。この表は、デバイスのテストに関する特定の要件があるかどうかも示しています。 これらは、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)を使用する場合に従う必要がある要件と同じです。

デバイスの種類が表示されない場合は、作成できます。「 [WDTF Simple I/o Action プラグインを使用してデバイスの i/o をカスタマイズする方法](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)」を参照してください。

## <a name="provided-simple-io-plugins-and-device-requirements-for-testing-and-tips-for-troubleshooting"></a>単純な i/o プラグインと、テスト用のデバイス要件とトラブルシューティングのヒントを提供しました

次のセクションでは、単純な i/o プラグインが含まれているデバイスの種類の一覧を示します。また、デバイスのテストに関する特定の要件があるかどうかも示します。 これらは、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)を使用する場合に従う必要がある要件と同じです。 このセクションでは、テストの失敗のトラブルシューティングとトリアージに使用できるヒントについても説明します。

* [オーディオデバイス](#audio)
* [Bluetooth デバイス](#bluetooth)
* [CDROM デバイス](#cdrom)
* [ディスクデバイス](#disk)
* [デバイスの表示](#display)
* [GPS デバイス](#gps-devices-and-gps-devices-in-systems)
* [LAN デバイス](#lan)
* [モバイルブロードバンドデバイス](#mobile-broadband)
* [ポータブルデバイス](#portable-devices)
* [スマートカードリーダー](#smart-card-readers)
* [センサ デバイス](#sensors)
* [数量](#volume)
* [Web カメラ](#webcam)
* [WLAN](#wlan)
* [USB コントローラーと Mutt を使用したハブ](#usb-controller-and-hub-with-mutt)

特定の要件を持つデバイスの基本テストの一覧については、「[特定のデバイス構成要件を持つデバイスの基本テスト](#device-fundamental-tests-that-have-specific-device-configuration-requirements)」を参照してください。

### <a name="audio"></a>オーディオ

#### <a name="requirements"></a>必要条件

* デバイスには、少なくとも1つのレンダリングの種類のエンドポイント (スピーカー、ヘッドホンなど) が接続されている必要があります。

* 対象のオーディオデバイスに HDMI ビデオとオーディオ出力機能がある場合、オーディオテストを実行するには、デバイスが hdmi モニターや A/V 受信者などの HDMI オーディオ対応デバイスに接続されている必要があります。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* レンダー型エンドポイントでサイン調整を再生します。 キャプチャの種類のエンドポイントでオーディオをキャプチャします。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* 最初のトリアージを実行するための HRESULT の失敗を確認します。
* テストが応答していない場合は、ターゲットコンピューターでカーネルデバッガーを使用して、根本原因を絞り込むことができます。
* トレースの実行:
  * カーネルトレースを開始します。

```syntax
xperf.exe -on LOADER+PROC_THREAD+CSWITCH+DISK_IO+HARD_FAULTS+PROFILE+INTERRUPT+NETWORKTRACE+DPC+Latency+POWER -stackwalk ProcessCreate+ProcessDelete+ImageLoad+ImageUnload+ThreadCreate+ThreadDelete+CSwitch+ReadyThread+Profile+DiskFlushInit+FileFlush+RegFlush+HardFault+VirtualAlloc+VirtualFree -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo_Kernel.etl
```

  * オーディオトレースの開始:

```syntax
xperf.exe -start AudioSimpleIo -on Microsoft-Windows-Audio+a6a00efd-21f2-4a99-807e-9b3bf1d90285:0xffff:0x3 -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo.etl
```

  * テストを実行します。
  * トレースの停止:

```syntax
xperf.exe -stop "NT Kernel Logger" Audio_SimpleIo
```

  * マージトレース:

```syntax
xperf.exe -merge Audio_SimpleIo_Kernel.etl Audio_SimpleIo.etl Audio_SimpleIo _Merged.etl
```

  * マージされたトレースファイルを Xperf (**xperfview**) で表示します。

### <a name="bluetooth"></a>Bluetooth

#### <a name="requirements"></a>必要条件

* 特別な要件はありません。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* [**BluetoothFindFirstDevice 関数**](https://docs.microsoft.com/windows/desktop/api/bluetoothapis/nf-bluetoothapis-bluetoothfindfirstdevice)を使用して Bluetooth デバイスを検索します。

### <a name="cdrom"></a>CDROM

#### <a name="requirements"></a>必要条件

* ドライブ文字が割り当てられています。
* メディアはデバイスに存在します。
* ファイルは、挿入されたメディア上に存在します。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* は、Win32 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile) API を使用して、cd-rom 上のファイルを検索し、読み取り操作を実行します。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* テストコンピューターで、問題の CD/DVD ドライブに移動し、ドライブの内容にアクセスできることを確認します。
* CD-ROM の単純な i/o プラグインは、から読み取りを実行するために使用する CD/DVD 上のファイルを検索します。 CD/DVD のファイルがディスク上にエンコードされていることを確認します。
* この単純な i/o プラグでは、Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 [**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)、 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)関数を使用します。 返されるエラーは、多くの場合、これらの Api からの Win32 エラーコードです。

### <a name="disk"></a>ディスク

#### <a name="requirements"></a>必要条件

* ディスクに、関連付けられているボリュームドライブ文字が少なくとも1つ割り当てられています。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* [ボリューム](#volume)の単純な i/o プラグインを使用します。

### <a name="display"></a>ディスプレイ

#### <a name="requirements"></a>必要条件

* テストの特別な要件はありません。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* では、D3DX Api を使用してグラフィックスアダプターを実行します。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* 使用されている Api からの失敗を報告するテストログを確認します。

### <a name="gps-devices-and-gps-devices-in-systems"></a>GPS デバイス (およびシステム内の GPS デバイス)

#### <a name="requirements"></a>必要条件

* デバイスは、適切な GPS 信号を持つ場所でテストする必要があります。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* [センサー](#sensors)に i/o プラグインを使用します。

### <a name="lan"></a>LAN

#### <a name="requirements"></a>必要条件

* デバイスに IPv6 アドレスがあります。

* デバイスは IPv6 ゲートウェイアドレスを持っています (それ以外の場合、テスト NIC が ping できる IPv6 アドレスを使用して、WDTFREMOTESYSTEM パラメーターをテストに渡す必要があります)。

* デバイスのネットワーク操作状態は、Ifoperation Statusup です。

* ネットワークデバイスは、WWAN でも WLAN デバイスでもありません。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* IPv6 ネットワークゲートウェイアドレスに ping を行います。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* 既存の IP アドレスがあることを確認します。
* ゲートウェイ IPv6 IP アドレスがあることを確認します。
* IP ゲートウェイアドレスを手動で確認します (ping.exe を使用します)。

### <a name="mobile-broadband"></a>モバイル ブロードバンド

#### <a name="requirements"></a>必要条件

* テストの特別な要件はありません。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* は[**Imbninterface インターフェイス**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)を使用し、GetHomeProvider、 [**Imbninterface:: GetInterfaceCapability メソッド**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterface-getinterfacecapability)、 [**Imbninterface:: GetReadyState method**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterface-getreadystate) api を呼び出してデバイスを実行します。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* MobileBroadbandPlugin は、限られた領域を持つことができません。

  * "MobileBroadbandPlugin: すべてのモバイルブロードバンドインターフェイスの取得でエラーが返されました。"
  * "MobileBroadbandPlugin: インターフェイスを取得しているときにエラーが返されました。"
  * "MobileBroadbandPlugin: 返された DeviceId を取得しています"
  * "MobileBroadbandPlugin: インターフェイス機能を取得するときにエラーが返されました"
  * "MobileBroadbandPlugin: ReadyState を取得できませんでした。"

* エラーを調査する最適な場所は、デバイスから開始し、準備情報またはデバイスの機能を示すことができなかったかどうかを判断することです。 さらに OS トレースファイルをデバッグするには、収集する必要があります。

  * **Netsh trace start wwan \_ dbg**コマンドを実行します。
  * 問題を再現します。
  * **Netsh trace stop**コマンドを実行します。

### <a name="portable-devices"></a>ポータブルデバイス

#### <a name="requirements"></a>必要条件

* デバイスには、フォルダーとファイルを作成できるストレージコンポーネントがあります。

**実行される i/o プラグインの種類:**

* WPD Api を使用して、WPD デバイス上のストレージコンポーネントに対してファイルの読み取りと書き込みを行います。

### <a name="smart-card-readers"></a>スマート カード リーダー

#### <a name="requirements"></a>必要条件

* デバイスにアテナ T0 のテストカードが挿入されています。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* カードリーダーに挿入されたアテナ T0 カードに対してデータの読み取りと書き込みを行います。

### <a name="sensors"></a>Sensors

#### <a name="requirements"></a>必要条件

* GPS デバイスは、適切な GPS 信号を持つ場所でテストする必要があります。

### <a name="volume"></a>ボリューム

#### <a name="requirements"></a>必要条件

* ボリュームにドライブ文字が割り当てられています。
* ボリュームに 5 MB の空き領域があります。
* ボリュームが書き込み禁止になっていません。
* メディアはデバイスに存在します。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* WDTF Volume IO という名前のディレクトリを作成 \_ \_ し、SimpleIO という名前のファイルを作成します。 I/o は、このファイルに対して[**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile) Api と[**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile) api を呼び出すことによって実行されます。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* テストコンピューターで、問題のドライブに移動し、ドライブの内容にアクセスできることを確認します。
* ドライブにファイルを保存しようとしました。 保存して簡単にアクセスできることを確認します。
* この単純な i/o プラグでは、Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 [**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)、 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)関数を使用します。 返されるエラーは、多くの場合、これらの Api からの Win32 エラーコードです。

### <a name="webcam"></a>ウェブ カメラ

#### <a name="requirements"></a>必要条件

* テストの特別な要件はありません。

    > [!NOTE]
    > Web カメラデバイス用の単純な i/o プラグインには MFPlat.dll ファイルに対する依存関係があります。これは、Windows 7 N や Windows 7 KN など、Media Player および関連するテクノロジを含まないバージョンの Windows では使用できません。 これらのバージョンの Windows では、Media Feature Pack がインストールされている必要があります。 メディア機能パックはダウンロードできます。 詳細については、[サポート技術情報の記事 968211](https://go.microsoft.com/fwlink/p/?linkid=266437)を参照してください。

**実行される i/o プラグインの種類:**

* メディアファンデーションインターフェイスを使用してビデオをキャプチャします。

### <a name="wlan"></a>WLAN

#### <a name="requirements"></a>必要条件

* HCK のドキュメントの「[デバイスの基本テストによって記録された WLAN SimpleIO プラグインのエラーのトラブルシューティング](https://go.microsoft.com/fwlink/p/?linkid=309556)」を参照してください。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* HCK のドキュメントの「[デバイスの基本テストによって記録された WLAN SimpleIO プラグインのエラーのトラブルシューティング](https://go.microsoft.com/fwlink/p/?linkid=309556)」を参照してください。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* HCK のドキュメントの「[デバイスの基本テストによって記録された WLAN SimpleIO プラグインのエラーのトラブルシューティング](https://go.microsoft.com/fwlink/p/?linkid=309556)」を参照してください。

### <a name="usb-controller-and-hub-with-mutt"></a>USB コントローラーと Mutt を使用したハブ

#### <a name="requirements"></a>必要条件

* テストの特別な要件はありません。

    デバイスにシンボリックリンクがあります。

#### <a name="type-of-io-plug-in-performs"></a>実行される i/o プラグインの種類

* Microsoft USB テストツール (MUTT) デバイスを使用した USB 転送テスト。 対象となる転送の種類は、制御、一括、アイソクロナス、割り込み、およびストリームです (スーパー Mutt が USB 3.0 コントローラーに接続されている場合のみ)。

#### <a name="how-to-triage-test-failures"></a>テストの失敗をトリアージする方法

* まず、テストログファイル内のメッセージを調べます。
* USB 2.0 および USB 3.0 スタックで Windows イベントトレーシング (ETW) を有効にすることで、さらに調査します。
  * USB 2.0 については、「Microsoft Windows USB Core チームのブログ- [windows 7 の usb コアスタックの ETW](https://go.microsoft.com/fwlink/p/?linkid=266442) 」を参照してください。
  * USB 3.0 については、「 [windows 8 で USB ETW トレースをキャプチャして読み取る方法]( https://go.microsoft.com/fwlink/p/?linkid=266443)」を参照してください。

## <a name="device-fundamental-tests-that-have-specific-device-configuration-requirements"></a>特定のデバイス構成要件を持つデバイスの基本テスト

次の[デバイスの基本テスト](https://docs.microsoft.com/windows-hardware/drivers)を実行する前に、特定のデバイスの種類について説明されている要件に従って、テストコンピューター上のデバイスを構成する必要があります。 提供されて[いる単純な i/o プラグインとデバイス要件](#provided-simple-io-plugins-and-device-requirements-for-testing-and-tips-for-troubleshooting)の一覧を参照してください。

* PCI ルートポートの突然の削除テスト (PCI デバイスのみ)
* デバイスパス Exerciser テスト (認定)
* スリープと PNP (無効化および有効化) と IO の前後 (認定)
* プラグアンドプレイドライバーテスト (認定)
* ハードウェアとオペレーティングシステムの同時実行 (混乱) テスト (認定)
* IO の前後に (証明書を使用して) 再インストールする
* ファイルシステムの整合性に関するデバイスのインストールチェック (証明書)
* デバイスのインストールチェックによるその他のデバイスの安定性の確認 (証明書)

## <a name="related-topics"></a>関連トピック

[Device Fundamental のテスト](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-fundamentals-tests)  
[Visual Studio を使って実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)  
[コマンドプロンプトから実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)  
[Device Fundamental テストを選んで構成する方法](https://docs.microsoft.com/windows-hardware/drivers)  
[デバイスの基本テストのトラブルシューティング](https://docs.microsoft.com/windows-hardware/drivers)  
