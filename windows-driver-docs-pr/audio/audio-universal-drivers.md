---
title: オーディオ用のユニバーサル Windows ドライバー
description: Windows 10 では、さまざまな種類のハードウェアで動作するユニバーサルオーディオドライバーを作成できます。
ms.assetid: F4B56B3F-792F-4887-AF0F-FFC1F000CB8F
ms.date: 10/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: f067360b3938102f5bbd7e2f59256a8315277221
ms.sourcegitcommit: 36b7db40d5a91d8726feb2e2d9d4ece1fb484051
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72591010"
---
# <a name="universal-windows-drivers-for-audio"></a>オーディオ用のユニバーサル Windows ドライバー

Windows 10 では、さまざまな種類のハードウェアで動作するユニバーサルオーディオドライバーを作成できます。 このトピックでは、この方法の利点、および異なるプラットフォーム間の違いについて説明します。 Windows では、オーディオ用のユニバーサル Windows ドライバーに加えて、従来のオーディオドライバーテクノロジ (WDM など) を引き続きサポートしています。

## <a name="getting-started-with-universal-windows-drivers-for-audio"></a>オーディオ用ユニバーサル Windows ドライバーを使用したはじめに

Ihv は、すべてのデバイス (デスクトップ、ノート pc、タブレット、携帯電話) で動作するユニバーサル Windows ドライバーを開発できます。 これにより、初期開発および後のコードメンテナンスの開発にかかる時間とコストを削減できます。

ユニバーサル Windows ドライバーのサポートを開発するために、次のツールを使用できます。

- Visual Studio 2015 のサポート: "Target Platform" を "Universal" に設定するドライバー設定があります。 ドライバー開発環境の設定の詳細については、「[ユニバーサル Windows ドライバーでのはじめに](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

- APIValidator ツール: ApiValidator ツールを使用して、ドライバーが呼び出す Api がユニバーサル Windows ドライバーに対して有効であることを確認できます。 このツールは windows 10 用の Windows Driver Kit (WDK) の一部であり、Visual Studio 2015 を使用している場合は自動的に実行されます。 詳細については、「[ユニバーサル Windows ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

- 更新された DDI リファレンスドキュメント: DDI リファレンスドキュメントは、ユニバーサル Windows ドライバーでサポートされている DDIs を示すために更新されています。 詳細については、「[オーディオデバイスリファレンス](https://docs.microsoft.com/previous-versions/ff536192(v=vs.85))」を参照してください。

## <a name="create-a-universal-audio-driver"></a>ユニバーサルオーディオドライバーを作成する

詳細な手順のガイダンスについては、「[ユニバーサル Windows ドライバーでのはじめに](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 手順の概要を次に示します。

1. ユニバーサルオーディオドライバーの開始点として使用するために、universal audio sysvad サンプルを読み込みます。 または、空の WDM ドライバーテンプレートを使用して開始し、オーディオドライバーの必要に応じて、universal sysvad サンプルのコードを追加します。

2. プロジェクトのプロパティで、[ターゲットプラットフォーム] を "Universal" に設定します。

3. インストールパッケージを作成する: ターゲットがデスクトップエディション (Home、Pro、Enterprise、および教育) の Windows 10 を実行しているデバイスである場合は、構成可能な INF ファイルを使用します。 ターゲットが Windows 10 Mobile を実行しているデバイスの場合は、PkgGen を使用して、spkg ファイルを生成します。

4. Windows 10 for desktop edition または Windows 10 Mobile 用のドライバーをビルド、インストール、展開、およびデバッグします。

## <a name="sample-code"></a>サンプルコード

Sysvad と SwapAPO は、ユニバーサル Windows ドライバーのサンプルに変換されました。 詳細については、「[サンプルオーディオドライバー](sample-audio-drivers.md)」を参照してください。

## <a name="available-programming-interfaces-for-universal-windows-drivers-for-audio"></a>オーディオ用ユニバーサル Windows ドライバーの使用可能なプログラミングインターフェイス

Windows 10 以降では、ドライバーのプログラミングインターフェイスは、OneCoreUAP ベースの Windows のエディションに含まれています。 この共通セットを使用して、ユニバーサル Windows ドライバーを作成できます。 これらのドライバーは、デスクトップエディションと Windows 10 Mobile 用の Windows 10 とその他の Windows 10 バージョンの両方で動作します。

次の DDIs は、ユニバーサルオーディオドライバーを使用する場合に使用できます。

- [オーディオドライバーのイベントセット](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-event-sets)

- [オーディオドライバーのインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-interfaces)

- [オーディオドライバーのプロパティセット](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)

- [オーディオドライバーの構造](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-structures)

- [オーディオトポロジノード](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-topology-nodes)

- [High Definition Audio DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/audio/high-definition-audio-ddi-reference)

- [Port クラス Audio Driver リファレンス](https://docs.microsoft.com/windows-hardware/drivers/audio/port-class-audio-driver-reference)

## <a name="convert-an-existing-audio-driver-to-a-universal-windows-driver"></a>既存のオーディオドライバーをユニバーサル Windows ドライバーに変換する

このプロセスに従って、既存のオーディオドライバーをユニバーサル Windows ドライバーに変換します。

1. 既存のドライバーの呼び出しが OneCoreUAP ウィンドウで実行されるかどうかを判断します。 リファレンスページの「必要条件」セクションを確認します。 詳細については、「[オーディオデバイスリファレンス](https://docs.microsoft.com/previous-versions/ff536192(v=vs.85))」を参照してください。

2. ユニバーサル Windows ドライバーとしてドライバーを再コンパイルします。 プロジェクトのプロパティで、[ターゲットプラットフォーム] を "Universal" に設定します。

3. ApiValidator ツールを使用して、ドライバーが呼び出した DDIs がユニバーサル Windows ドライバーで有効であることを確認します。 このツールは windows 10 用の Windows Driver Kit (WDK) の一部であり、Visual Studio 2015 を使用している場合は自動的に実行されます。 詳細については、「[ユニバーサル Windows ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

4. ドライバーが OneCoreUAP の一部ではないインターフェイスを呼び出すと、コンパイラはエラーを表示します。

5. これらの呼び出しを代替呼び出しに置き換えるか、コードの回避策を作成するか、新しいドライバーを記述します。

## <a name="creating-a-componentized-audio-driver-installation"></a>コンポーネント化オーディオドライバーのインストールの作成

### <a name="overview"></a>概要

より円滑で信頼性の高いインストールエクスペリエンスを作成し、コンポーネントサービスをより適切にサポートするには、ドライバーのインストールプロセスを次のコンポーネントに分割します。

- DSP (存在する場合) とコーデック
- 郵便局
- OEM のカスタマイズ

必要に応じて、DSP とコーデックに個別の INF ファイルを使用できます。

この図は、コンポーネント化オーディオインストールの概要を示しています。

![DSP ドライバーコーデックと APOs を示す、コンポーネント化されたオーディオスタック](images/audio-componentized-stack-diagram.png)

個別の拡張 INF ファイルを使用して、特定のシステムの各基本ドライバーコンポーネントをカスタマイズします。 カスタマイズには、チューニングパラメーターやその他のシステム固有の設定が含まれます。 詳細については、「[拡張機能の INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)」を参照してください。

拡張機能の INF ファイルは、ユニバーサル INF ファイルである必要があります。 詳細については、「 [UNIVERSAL INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)」を参照してください。

INF ファイルを使用したソフトウェアの追加の詳細については、「[コンポーネント Inf ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)」を参照してください。

### <a name="submitting-componentized-inf-files"></a>コンポーネント化 INF ファイルの送信

APO INF パッケージは、基本ドライバーパッケージとは別にパートナーセンターに送信する必要があります。 パッケージの作成の詳細については、「 [WINDOWS HLK はじめに](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)」を参照してください。

### <a name="sysvad--componentized-inf-files"></a>SYSVAD コンポーネント化 INF ファイル

コンポーネント化された INF ファイルの例については、Github の[sysvad/TabletAudioSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad/TabletAudioSample)を参照してください。

| ファイル名                              | 説明                                                                    |
|----------------------------------------|--------------------------------------------------------------------------------|
| ComponentizedAudioSample           | 基本コンポーネントのサンプルオーディオ INF ファイル。                                  |
| ComponentizedAudioSampleExtension  | 追加の OEM カスタマイズを含む sysvad base の拡張ドライバー。   |
| ComponentizedApoSample             | APO サンプル拡張機能の INF ファイル。                                              |

従来の INF ファイルは、SYSVAD サンプルで引き続き使用できます。

| ファイル名                      | 説明                                                                    |
|--------------------------------|--------------------------------------------------------------------------------|
| tabletaudiosample          | ドライバーのインストールに必要なすべての情報を含むデスクトップ monolitic INF ファイル。 |
| 電話のサンプル .inf           | ドライバーのインストールに必要なすべての情報を含む phone monolitic INF ファイル。   |

### <a name="apo-vendor-specific-tuning-parameters-and-feature-configuration"></a>APO ベンダー固有のチューニングパラメーターと機能の構成

すべての APO ベンダーシステム固有の設定、パラメーター、およびチューニング値は、拡張機能の INF パッケージを使用してインストールする必要があります。 多くの場合、これは[INF AddReg ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して単純な方法で実行できます。 より複雑なケースでは、チューニングファイルを使用できます。  

基本ドライバーパッケージは、機能するためにこれらのカスタマイズに依存しないようにする必要があります (もちろん、機能が低下する可能性があります)。  

### <a name="uwp-audio-settings-apps"></a>UWP オーディオ設定アプリ

エンドユーザーの UI を実装するには、Windows ユニバーサルオーディオドライバーにハードウェアサポートアプリ (HSA) を使用します。  詳細については、「[ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-driver-developers)」を参照してください。

### <a name="programmatically-launching-uwp-hardware-support-apps"></a>UWP ハードウェアサポートアプリのプログラムによる起動

ドライバーイベント (たとえば、新しいオーディオデバイスが接続されている場合) に基づいて UWP ハードウェアサポートアプリをプログラムで起動するには、Windows シェル Api を使用します。 Windows 10 Shell Api は、リソースのアクティブ化に基づいて UWP UI を起動する方法、または[IApplicationActivationManager](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nf-shobjidl_core-iapplicationactivationmanager-activateapplication)を介して直接起動する方法をサポートしています。 UWP アプリケーションの自動起動の詳細については、「 [Windows 10 uwp アプリの起動の自動化](https://docs.microsoft.com/windows/uwp/xbox-apps/automate-launching-uwp-apps#launch-activation)」を参照してください。  

### <a name="apo-and-device-driver-vendor-use-of-the-audiomodules-api"></a>APO およびデバイスドライバベンダーによる AudioModules API の使用

オーディオモジュール API/DDI は、UWP アプリケーションまたはユーザーモードサービスの間でカーネルドライバーモジュールまたは DSP 処理ブロックに渡されるコマンドの通信トランスポート (プロトコルではありません) を標準化するように設計されています。 オーディオモジュールには、モジュールの列挙と通信をサポートする正しい DDI を実装するドライバーが必要です。 これらのコマンドはバイナリとして渡され、解釈/定義は作成者に対して残されます。  

オーディオモジュールは、現在、UWP アプリとオーディオエンジンで実行されている SW APO との間の直接的な通信を容易にするようには設計されていません。

オーディオモジュールの詳細については、「[オーディオモジュール通信の実装](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)」および「[オーディオデバイスモジュールの構成とクエリ](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)」を参照してください。

### <a name="apo-hwid-strings-construction"></a>APO HWID strings コンストラクション  

APO ハードウェア Id には、標準情報とベンダー定義の文字列の両方が組み込まれています。

これらは次のように構成されます。

```syntax
SWC\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4) &REV_r(4)
SWC\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4)
SWC\VEN_v(4)&AID_a(4)
```

各値の意味は次のとおりです。

- v (4) は、APO デバイスベンダーの4文字の識別子です。 これは、Microsoft によって管理されます。  
- (4) は、APO ベンダーによって定義された、APO の4文字の識別子です。  
- n (4) は、親デバイスのサブシステムのベンダーに対して、4文字の PCI SIG で割り当てられた識別子です。 これは通常、OEM 識別子です。
- s (4) は、親デバイスの4文字のベンダー定義サブシステム識別子です。 これは通常、OEM 製品識別子です。

### <a name="plug-and-play-inf-version-and-date-evaluation-for-driver-update"></a>ドライバーの更新に関するプラグアンドプレイ INF バージョンと日付の評価

Windows プラグアンドプレイシステムは、日付とドライバーのバージョンを評価して、複数のドライバーが存在する場合にインストールするドライブを決定します。  詳細については、「 [Windows がドライバーをランク付けする方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)」を参照してください。

最新のドライバーを使用できるようにするには、新しいバージョンのドライバーごとに、日付とバージョンを必ず更新してください。

### <a name="apo-driver-registry-key"></a>APO ドライバーレジストリキー

サードパーティが定義したオーディオドライバー/APO レジストリキーについては、HKLM\System\CurrentControlSet. を除き、HKR を使用します。

### <a name="use-a-windows-service-to-facilitate-uwp---apo-communication"></a>Windows サービスを使用して UWP < > APO 通信を容易にする

Windows サービスは APOs のようなユーザーモードのコンポーネントの管理には厳密には必要ありませんが、設計に UWP < > APO 通信を容易にする RPC サーバーが含まれている場合は、Windows サービスにその機能を実装することをお勧めします。オーディオエンジンで実行されている APO を制御します。  

## <a name="building-the-sysvad-universal-audio-sample-for-windows10-desktop"></a>Windows 10 Desktop 用の Sysvad Universal Audio サンプルのビルド

Windows 10 desktop 用の sysvad サンプルをビルドするには、次の手順を実行します。

1. デスクトップの inf ファイル (tabletaudiosample) を見つけて、製造元の名前を "Contoso" などの値に設定します。

2. ソリューションエクスプローラーで、[ソリューション ' sysvad '] を右クリックし、[Configuration Manager] を選択します。 Windows の64ビットバージョンにデプロイする場合は、ターゲットプラットフォームを x64 に設定します。 すべてのプロジェクトで、構成とプラットフォームの設定が同じであることを確認します。

3. Sysvad ソリューションのすべてのプロジェクトをビルドします。

4. ビルドからビルドの出力ディレクトリを探します。 たとえば、次のようなディレクトリに配置できます。

   ```cmd
   C:\Program Files (x86)\Windows Kits\10\src\audio\sysvad\x64\Debug\package
   ```

5. WDK インストールの Tools フォルダーに移動し、PnpUtil ツールを見つけます。 たとえば、C: \\Program Files (x86) \\Windows Kit \\10 \\Tools \\x64 \\PnpUtil .exe フォルダーを探します。

6. Sysvad ドライバーをインストールするシステムに、次のファイルをコピーします。

|                            |                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------|
| TabletAudioSample      | ドライバーファイル。                                                                  |
| tabletaudiosample      | ドライバーのインストールに必要な情報が含まれている情報 (INF) ファイル。 |
| sysvad.cat                 | カタログファイル。                                                                 |
| SwapAPO .dll                | APOs を管理するための UI のサンプルドライバー拡張機能。                                |
| PropPageExt            | プロパティページのドライバーの拡張機能のサンプルです。                                    |
| KeywordDetectorAdapter | キーワード検出機能のサンプルです。                                                        |

## <a name="install-and-test-the-driver"></a>ドライバーをインストールしてテストする

ターゲットシステムの PnpUtil を使用してドライバーをインストールするには、次の手順に従います。

1. と管理者のコマンドプロンプトを開き、ドライバーファイルをコピーしたディレクトリに次のように入力します。

    **pnputil-i-tabletaudiosample**

2. Sysvad ドライバーのインストールが完了します。 エラーが発生した場合は、このファイルを調査して追加情報を確認できます。 `%windir%\inf\setupapi.dev.log`

3. デバイスマネージャーの [表示] メニューで、[種類別のデバイス] を選択します。 デバイスツリーで、[Microsoft 仮想オーディオデバイス (WDM)-Sysvad Sample] を見つけます。 通常は、[サウンド、ビデオ、およびゲームコントローラー] ノードの下にあります。

4. 対象のコンピューターで、コントロールパネル を開き、**ハードウェアとサウンド** に移動して、**オーディオデバイスの管理** を &gt; ます。 [サウンド] ダイアログボックスで、[Microsoft 仮想オーディオデバイス (WDM)-Sysvad Sample] というラベルのスピーカーアイコンを選択し、[既定値の設定] をクリックします。ただし、[OK] はクリックしないでください。 これにより、[サウンド] ダイアログボックスが開いたままになります。

5. 対象のコンピューターで MP3 またはその他のオーディオファイルを見つけ、ダブルクリックして再生します。 次に、[サウンド] ダイアログボックスで、Microsoft Virtual Audio Device (WDM)-Sysvad サンプルドライバーに関連付けられているボリュームレベルインジケーターにアクティビティがあることを確認します。

## <a name="building-the-sysvad-universal-audio-sample-for-windows10-mobile"></a>Windows 10 Mobile 用の Sysvad Universal Audio サンプルをビルドする

Windows 10 Mobile 用の sysvad サンプルをビルドするには、次の手順を実行します。

1. モバイル inf ファイル (「」を参照してください) を見つけ、製造元名を "Contoso" などの値に設定します。

2. Sysvad ソリューションで、次のプロジェクトをビルドします。

   - EndPointsCommon

   - 電話のオーディオサンプル

3. からビルドの出力ディレクトリを探します。 たとえば、の Visual Studio の既定の場所は、次のようなディレクトリに配置することができます。

   ```cmd
   C:\Program Files (x86)\Windows Kits\10\src\audio\sysvad\x64\Debug\package`
   ```

4. 「[パッケージの作成](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))」のガイダンスに従って、モバイルイメージのドライバーファイルを含むパッケージを作成します。

5. モバイルドライバーパッケージ (spkg ファイル) をインストールするには、パッケージをモバイル OS イメージにまとめる必要があります。 ImgGen を使用して、モバイルデバイスにフラッシュできる完全な flash 更新 (FFU) イメージに spkg ドライバーパッケージを追加します。 Sysvad 仮想オーディオドライバーのテストを可能にするために、モバイルイメージに存在する他のオーディオドライバーを削除することが必要になる場合があります。

6. OS イメージにドライバーパッケージが含まれていることを確認したら、サウンドクリップを再生し、sysvad phone audio サンプルが機能していることを確認します。 モバイルデバイスで sysvad 仮想ドライバーを監視するためのカーネルデバッガー接続を確立できます。
