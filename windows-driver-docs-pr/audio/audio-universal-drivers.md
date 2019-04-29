---
title: オーディオ用のユニバーサル Windows ドライバー
description: Windows 10 では、さまざまな種類のハードウェアで動作するユニバーサル オーディオ ドライバーを記述できます。
ms.assetid: F4B56B3F-792F-4887-AF0F-FFC1F000CB8F
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795050c4d65f5be9d98dfc14572bd782bcb5d751
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333945"
---
# <a name="universal-windows-drivers-for-audio"></a>オーディオ用のユニバーサル Windows ドライバー

Windows 10 では、さまざまな種類のハードウェアで動作するユニバーサル オーディオ ドライバーを記述できます。 このトピックでは、さまざまなプラットフォーム間の相違点と同様にこのアプローチの利点について説明します。 オーディオのユニバーサル Windows ドライバーだけでなくは WDM など、オーディオ ドライバーの以前のテクノロジをサポートするために Windows が続行されます。

## <a name="getting-started-with-universal-windows-drivers-for-audio"></a>オーディオのユニバーサル Windows ドライバーの概要

Ihv は、すべてのデバイス (デスクトップ、ラップトップ、タブレット、携帯電話) で動作するユニバーサル Windows ドライバーを開発できます。 このことができますには、開発時とは初期開発と以降のコードの保守コストが削減されます。

これらのツールは、ユニバーサル Windows ドライバーのサポートを開発できます。

- Visual Studio 2015 のサポート:「ターゲット プラットフォーム」を"Universal"と等しく設定するドライバーの設定があります。 ドライバーの開発環境のセットアップの詳細については、次を参照してください。[ユニバーサル Windows ドライバーの概要](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)します。

- APIValidator ツール:ApiValidator.exe ツールを使うと、ドライバーから呼び出される API が、ユニバーサル Windows ドライバーにとって有効であるかどうかを確認できます。 このツールは、Windows 10、Windows Driver Kit (WDK) の一部であるし、Visual Studio 2015 を使用している場合は、自動的に実行されます。 詳細については、次を参照してください。[ユニバーサル Windows ドライバーの検証](https://msdn.microsoft.com/windows-drivers/develop/validating_universal_drivers)です。

- 更新された DDI リファレンス ドキュメント。ユニバーサル Windows ドライバーがサポートされるどの Ddi DDI のリファレンス ドキュメントを更新しています。 詳細については、次を参照してください。[オーディオ デバイス参照](https://msdn.microsoft.com/library/windows/hardware/ff536192)します。

## <a name="create-a-universal-audio-driver"></a>ユニバーサル オーディオ ドライバーを作成します。

ステップ バイ ステップ ガイダンスについては、次を参照してください。[ユニバーサル Windows ドライバーの概要](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)します。 手順の概要を次に示します。

1. ユニバーサル、オーディオ ドライバーの開始点として使用するオーディオ sysvad のユニバーサル サンプルを読み込みます。 または、空の WDM ドライバー テンプレートを使用して起動し、オーディオ ドライバーに必要なユニバーサル sysvad のサンプル コードに追加します。

2. プロジェクトのプロパティでは、"Universal"するターゲット プラットフォームを設定します。

3. インストール パッケージを作成します。ターゲットがデスクトップ エディション (Home、Pro、Enterprise、および教育機関向け) の使用、構成可能な INF ファイルの Windows 10 を実行しているデバイスの場合は。 ターゲットが Windows 10 Mobile を実行しているデバイスの場合は、.spkg ファイルを生成する PkgGen を使用します。

4. ビルド、インストール、展開、および Windows 10 のデスクトップ エディションまたは Windows 10 Mobile のドライバーをデバッグします。

## <a name="sample-code"></a>サンプル コード

ユニバーサル Windows ドライバーのサンプルを Sysvad と SwapAPO が変換されました。 詳細については、次を参照してください。[サンプル オーディオ ドライバー](sample-audio-drivers.md)します。

## <a name="available-programming-interfaces-for-universal-windows-drivers-for-audio"></a>オーディオのユニバーサル Windows ドライバーの使用可能なプログラミング インターフェイス

Windows 10 以降、ドライバーのプログラミング インターフェイスは、Windows OneCoreUAP ベース エディションの一部です。 その共通のセットを使用すると、ユニバーサル Windows ドライバーを作成することができます。 これらのドライバーは、バージョンを両方デスクトップ エディションの Windows 10 および Windows 10 Mobile、およびその他の Windows 10 で実行されます。

次の Ddi はユニバーサル オーディオ ドライバーを使用する場合に使用できます。

- [オーディオ ドライバーのイベントのセット](https://msdn.microsoft.com/library/windows/hardware/ff536195)

- [オーディオ ドライバー インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff536196)

- [オーディオ ドライバーのプロパティ セット](https://msdn.microsoft.com/library/windows/hardware/ff536197)

- [オーディオ ドライバー構造体](https://msdn.microsoft.com/library/windows/hardware/ff536198)

- [オーディオのトポロジのノード](https://msdn.microsoft.com/library/windows/hardware/ff536219)

- [高解像度オーディオ DDI 参照](https://msdn.microsoft.com/library/windows/hardware/ff536445)

- [ポート クラス オーディオ ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff537764)

## <a name="convert-an-existing-audio-driver-to-a-universal-windows-driver"></a>ユニバーサル Windows ドライバーに既存のオーディオ ドライバーの変換します。

ユニバーサル Windows ドライバーに既存のオーディオ ドライバーを変換するには、このプロセスに従います。

1. 既存のドライバー呼び出しが OneCoreUAP Windows で実行するかどうかを決定します。 リファレンス ページの [要件] セクションを確認します。 詳細については、次を参照してください。[オーディオ デバイス参照](https://msdn.microsoft.com/library/windows/hardware/ff536192)します。

2. ユニバーサル Windows ドライバーとしては、ドライバーを再コンパイルします。 プロジェクトのプロパティでは、"Universal"するターゲット プラットフォームを設定します。

3. Ddi のドライバーの呼び出しが、ユニバーサル Windows ドライバーが有効であることを確認するのに ApiValidator.exe ツールを使用します。 このツールは、Windows 10、Windows Driver Kit (WDK) の一部であるし、Visual Studio 2015 を使用している場合は、自動的に実行されます。 詳細については、次を参照してください。[ユニバーサル Windows ドライバーの検証](https://msdn.microsoft.com/windows-drivers/develop/validating_universal_drivers)です。

4. ドライバーが OneCoreUAP の一部ではないインターフェイスを呼び出す場合、コンパイラはエラーを表示します。

5. これらの呼び出しを代替の呼び出しに置き換えますコード回避策を作成または新しいドライバーを作成します。

## <a name="creating-a-componentized-audio-driver-installation"></a>コンポーネント化されたオーディオ ドライバーのインストールを作成します。

### <a name="overview"></a>概要

インストールがよりスムーズかつ信頼性の高いエクスペリエンスを作成し、コンポーネント サービスのサポートを強化するには、ドライバーのインストール プロセスを次のコンポーネントに分割します。

- DSP (ある場合) とコーデック
- APO
- OEM のカスタマイズ

必要に応じて、DSP とコーデックの個別の INF ファイルを使用できます。

この図では、コンポーネント化されたオーディオのインストールをまとめたものです。

![DSP ドライバー コーデックと時刻を示すコンポーネント化された、オーディオ スタック](images/audio-componentized-stack-diagram.png)

別個の拡張機能の INF ファイルは、特定のシステムの場合は、各基本ドライバー コンポーネントのカスタマイズに使用されます。 カスタマイズにはするには、チューニング パラメーターとその他のシステムに固有の設定が含まれます。 詳細については、次を参照してください。[拡張子 INF ファイルを使用して](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)します。

拡張機能の INF ファイルは、ユニバーサル INF ファイルである必要があります。 詳細については、次を参照してください。[ユニバーサル INF ファイルを使用して](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)します。

INF ファイルを使用してソフトウェアを追加する方法の詳細については、次を参照してください。[コンポーネントの INF ファイルを使用して](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)します。

### <a name="submitting-componentized-inf-files"></a>コンポーネント化された INF ファイルを送信します。

APO INF パッケージは、基本のドライバー パッケージからのとは別に、パートナー センターに送信する必要があります。 パッケージの作成についての詳細については、次を参照してください。 [Windows HLK Getting Started](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)します。

### <a name="sysvad--componentized-inf-files"></a>SYSVAD は、INF ファイルをコンポーネント化

調べるコンポーネント化された INF ファイルの例を参照する、 [sysvad/TabletAudioSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad/TabletAudioSample)Github でします。

| ファイル名                              | 説明                                                                    |
|----------------------------------------|--------------------------------------------------------------------------------|
| ComponentizedAudioSample.inf           | 基本のコンポーネント化されたサンプル オーディオ INF ファイルです。                                  |
| ComponentizedAudioSampleExtension.inf  | さらに OEM カスタマイズの基本 sysvad の拡張機能ドライバー。   |
| ComponentizedApoSample.inf             | APO サンプル INF 拡張子のファイルです。                                              |

従来の INF ファイルは引き続き SYSVAD サンプルで使用できます。

| ファイル名                      | 説明                                                                    |
|--------------------------------|--------------------------------------------------------------------------------|
| tabletaudiosample.inf          | すべてのドライバーをインストールするために必要な情報を含むデスクトップ monolitic INF ファイル。 |
| phoneaudiosample.inf           | すべてのドライバーをインストールするために必要な情報を含む電話の monolitic INF ファイル。   |

### <a name="apo-vendor-specific-tuning-parameters-and-feature-configuration"></a>APO ベンダーの特定のチューニング パラメーターと機能の構成

APO のすべてのベンダー固有のシステムの設定、パラメーター、およびチューニングの値は、INF 拡張機能パッケージを使用してインストールする必要があります。 この、多くの場合、簡単な方法で実行できます、 [INF AddReg ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)します。 複雑な場合は、チューニングのファイルを使用できます。  

基本のドライバー パッケージは、(ただし、もちろん機能が制限されます) に機能するためにこれらのカスタマイズに依存しない必要があります。  

### <a name="programmatically-launching-uwp-hardware-support-apps"></a>UWP アプリのハードウェア サポートをプログラムで起動します。

UWP ハードウェアのサポート、アプリをプログラムで起動する (たとえば、新しいオーディオ デバイスが接続されている場合) ドライバー イベントに基づく、Windows シェル Api を使用します。 Windows 10 のシェル Api リソースの有効化、または経由で直接ベースの UWP の UI を起動するメソッドをサポートして[IApplicationActivationManager](https://msdn.microsoft.com/library/windows/desktop/hh706903.aspx)します。 UWP アプリケーションの自動起動する方法の詳細を検索する[Windows 10 UWP アプリの起動を自動化](https://docs.microsoft.com/windows/uwp/xbox-apps/automate-launching-uwp-apps#launch-activation)します。  

### <a name="apo-and-device-driver-vendor-use-of-the-audiomodules-api"></a>AudioModules API の APO とデバイス ドライバーのベンダー使用

オーディオ モジュール API/DDI は UWP アプリケーションまたはカーネル ドライバー モジュールまたは DSP 処理ブロックへのユーザー モード サービスの間で渡されるコマンドの通信トランスポート (ただし、プロトコルではない) を標準化するために設計されています。 オーディオのモジュールには、モジュールの列挙との通信をサポートするために正しい DDI を実装するドライバーが必要です。 コマンドは、バイナリとして渡され、解釈/定義の作成者が委ねします。  

現在、オーディオのモジュールは、UWP アプリと、オーディオ エンジンで実行されているソフトウェア APO 間の直接のコミュニケーションを促進するものではありません。

オーディオのモジュールの詳細については、次を参照してください。[オーディオ モジュールの通信を実装する](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)と[とクエリの構成のオーディオ デバイス モジュール](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)します。

### <a name="apo-hwid-strings-construction"></a>APO HWID 文字列の構築  

APO ハードウェア Id では、標準的な情報およびベンダーによって定義される文字列の両方を組み込みます。

次のように構築します。

```syntax
APO\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4) &REV_r(4)
APO\VEN_v(4)&AID_a(4)&SUBSYS_ n(4)s(4)
APO\VEN_v(4)&AID_a(4)
```

各項目の意味は次のとおりです。

- v(4) は、APO デバイスの製造元の 4 文字の識別子です。 これは、Microsoft によって管理されます。  
- a(4) は、APO ベンダーによって定義された、APO の 4 文字の識別子です。  
- n(4) は、親デバイス用サブシステムのベンダーの 4 文字 PCI SIG によって割り当てられた識別子です。 これは、通常、OEM の識別子です。
- s(4) は、親デバイスの 4 文字のベンダ定義のサブシステムの識別子です。 これは、通常、OEM 製品識別子です。

### <a name="plug-and-play-inf-version-and-date-evaluation-for-driver-update"></a>ドライバーの更新のプラグ アンド プレイ INF のバージョンと日付評価

Windows のプラグ アンド プレイのシステムでは、複数のドライバーが存在する場合にインストールするドライブを確認するには、日付とドライバーのバージョンを評価します。  詳細については、次を参照してください。[ランク ドライバーをどのように Windows](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)します。

を使用する最新のドライバーを許可するのには、必ずし、日付とドライバーの新しいバージョンのバージョンを更新します。

### <a name="apo-driver-registry-key"></a>APO ドライバーのレジストリ キー

サード パーティ定義オーディオ ドライバー/APO のレジストリ キー hklm \system\currentcontrolset を除き HKR を使用します。

### <a name="use-a-windows-service-to-facilitate-uwp---apo-communication"></a>Windows サービスを使用して、UWP <> - APO コミュニケーションを促進するには

Windows サービスは APOs などのユーザー モード コンポーネントの管理に必須ではありません、ただし、設計には、UWP <> - APO の通信を容易にするよう RPC サーバーが含まれている場合をお勧めを実装することを Windows の機能サービスが、オーディオ エンジンで実行されている APO を制御します。  

## <a name="building-the-sysvad-universal-audio-sample-for-windows10-desktop"></a>Windows 10 デスクトップの Sysvad ユニバーサル オーディオ サンプルのビルド

Windows 10 デスクトップの sysvad サンプルをビルドする、次の手順を完了します。

1. デスクトップの inf ファイル (tabletaudiosample.inf) を見つけて、製造元の名前を"Contoso"などの値に設定

2. ソリューション エクスプ ローラーで 'sysvad' ソリューションを右クリックし、Configuration Manager の選択。 Windows の 64 ビット バージョンを展開する場合は、x64 をターゲット プラットフォームを設定します。 構成とプラットフォームの設定は、すべてのプロジェクトの同じことを確認します。

3. すべての sysvad ソリューション内のプロジェクトをビルドします。

4. ビルドからビルド出力ディレクトリを見つけます。 たとえばはこのようなディレクトリにある可能性があります。

   ```cmd
   C:\Program Files (x86)\Windows Kits\10\src\audio\sysvad\x64\Debug\package
   ```

5. WDK のインストールの Tools フォルダーに移動し、PnpUtil ツールを見つけます。 たとえば、次のフォルダーを探します。C:\\プログラム ファイル (x86)\\Windows キット\\10\\ツール\\x64\\PnpUtil.exe します。

6. Sysvad ドライバーをインストールするシステムには、次のファイルをコピーします。

|                            |                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------|
| TabletAudioSample.sys      | ドライバー ファイルです。                                                                  |
| tabletaudiosample.inf      | ドライバーをインストールするために必要な情報が含まれる情報 (INF) ファイル。 |
| sysvad.cat                 | カタログ ファイル。                                                                 |
| SwapAPO.dll                | パスワードを管理するための UI 用のサンプル ドライバー拡張します。                                |
| PropPageExt.dll            | プロパティ ページのサンプル ドライバー拡張します。                                    |
| KeywordDetectorAdapter.dll | サンプルのキーワード ディテクターです。                                                        |

## <a name="install-and-test-the-driver"></a>インストールして、ドライバーをテストします。

ターゲット システム上、pnputil ツールを使用してドライバーをインストールする手順に従います。

1. 開く、管理者コマンド プロンプト、ドライバー ファイルをコピーしたディレクトリでは、次の種類。

    **pnputil -i -a tabletaudiosample.inf**

2. Sysvad ドライバーのインストールを完了する必要があります。 エラーがある場合は、詳細については、このファイルを確認できます。 `%windir%\inf\setupapi.dev.log`

3. デバイス マネージャーで、[表示] メニューには、種類別のデバイスを選択します。 デバイス ツリーで、Microsoft 仮想オーディオ デバイス (WDM) - Sysvad サンプルを見つけます。 これは通常、サウンド、ビデオ、およびゲーム コント ローラー ノードの下です。

4. 対象のコンピューターに コントロール パネルを開きに移動**ハードウェアとサウンド** &gt; **オーディオ デバイスを管理する**します。 サウンド ダイアログ ボックスで、として Microsoft 仮想オーディオ デバイス (WDM) - Sysvad サンプルでは、スピーカー アイコンを選択し、既定値の設定 をクリックしてが ok をクリックしてしないでください。 これは、[サウンド] ダイアログ ボックスを開いたままです。

5. MP3 または対象のコンピューター上の他のオーディオ ファイルを見つけてダブルクリックを再生します。 [サウンド] ダイアログ ボックスで、Microsoft 仮想オーディオ デバイス (WDM) - Sysvad サンプル ドライバーが関連付けられているボリューム レベルのインジケーターにアクティビティがあることを確認します。

## <a name="building-the-sysvad-universal-audio-sample-for-windows10-mobile"></a>Windows 10 Mobile の Sysvad ユニバーサル オーディオ サンプルのビルド

Windows 10 Mobile の sysvad サンプルをビルドするには、次の手順を完了します。

1. モバイルの inf ファイル (phoneaudiosample.inf) を見つけて、製造元の名前を"Contoso"などの値に設定

2. Sysvad ソリューションでは、次のプロジェクトをビルドするには。

   - EndPointsCommon

   - PhoneAudioSample

3. ビルドからの出力ディレクトリに移動します。 たとえば、既定値は、Visual Studio での場所をこのようなディレクトリにある可能性があります。

   ```cmd
   C:\Program Files (x86)\Windows Kits\10\src\audio\sysvad\x64\Debug\package`
   ```

4. ガイダンスに従って[パッケージを作成する](https://msdn.microsoft.com/library/dn756642)モバイル イメージのドライバー ファイルを含むパッケージを作成します。

5. モバイルのドライバー パッケージ (.spkg ファイル) をインストールするには、モバイル OS イメージにパッケージを結合する必要があります。 ImgGen を使用すると、モバイル デバイスにアップデートできるし、フラッシュの完全な更新プログラム (FFU) イメージに .spkg ドライバー パッケージを追加できます。 Sysvad 仮想オーディオ ドライバーのテストのためにモバイル イメージ内に存在するその他のオーディオ ドライバーを削除する必要がある場合があります。

6. ドライバー パッケージが実行されている OS イメージが格納された後、サウンド クリップを再生し、sysvad phone オーディオ サンプルが機能しているかを検証します。 Sysvad 仮想ドライバーで、モバイル デバイスを監視する、カーネル デバッガーの接続を確立することができます。