---
title: UWP デバイス アプリでカメラ オプションをカスタマイズする方法
description: Windows 8.1、UWP デバイス アプリはデバイスの製造元が一部のカメラ アプリでカメラの他のオプションを表示するポップアップのカスタマイズを使用できます。
ms.assetid: 4BA34A3F-3C0D-4DDC-BA0A-E62AE9A6A93A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a715334377e827f67d42361fad6d39538b801fec
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419586"
---
# <a name="how-to-customize-camera-options-with-a-uwp-device-app"></a>UWP デバイス アプリでカメラ オプションをカスタマイズする方法

Windows 8.1、UWP デバイス アプリはデバイスの製造元が一部のカメラ アプリでカメラの他のオプションを表示するポップアップのカスタマイズを使用できます。 このトピックでは、**より多くのオプション**フライアウトを表示する、CameraCatureUI API をし、表示方法、C#のバージョン、[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプルでは、既定のフライアウトで、カスタムのフライアウトです。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

> [!NOTE]
> Windows 8.1、組み込みのカメラ アプリが表示されませんが、**より多くのオプション**ボタンをクリックし、そのため、カメラの他のオプションを表示する UWP デバイス アプリを表示することはできません。 ただし、 [CameraCaptureUI クラス](https://go.microsoft.com/fwlink/p/?LinkId=317985)、すべての UWP アプリで使用できるは、**より多くのオプション**ボタンをクリックし、そこから UWP デバイス アプリを表示することができます。

C#のバージョン、[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)使用して、 **DeviceAppPage.xaml**カメラ オプションの詳細についてカスタム ポップアップの UI を示すためにページ。 このサンプルでは、カメラ driver MFT (メディア ファンデーション変換) を使用してカメラの効果も適用されます。 詳細については、次を参照してください。[カメラ driver MFT 作成](creating-a-camera-driver-mft.md)です。

> [!NOTE]
> このトピックで示すコード例に基づいています、C#のバージョン、[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプル。 このサンプルも JavaScript および C++ で使用できます。 コードの最新バージョンを参照するサンプルをダウンロードします。

## <a name="more-options-for-cameras"></a>カメラの他のオプション

複数のカメラ オプションがエクスペリエンスは、UWP アプリの場合、別のアプリがキャプチャまたはを使用して、カメラからビデオをプレビューするときに、UWP デバイスのアプリが提供する機能、 [CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API。 アクセスできる、**より多くのオプション**カメラ オプション ウィンドウ内のリンク。 全画面表示ではありませんが、これは、ユーザーがクリックするか、外部でタップしたときに終了した軽量でコンテキストのユーザー インターフェイスを表示するためのコントロール内、フライアウトが表示されます。

このエクスペリエンスは、カスタムのビデオ効果を適用する機能など、カメラの差別化を強調表示機能を使用できます。

カメラ用 UWP デバイスのアプリがインストールされていない、Windows は経験はカメラ オプション、既定値を提供します。 Windows ことを検出した場合、カメラの UWP デバイスのアプリがインストールされていると、アプリで選択をする、`windows.cameraSettings`拡張機能では、アプリが Windows によって提供される既定のエクスペリエンスを置き換えます。

カメラ オプションの詳細については、flyout を呼び出すには。

1. 使用する UWP アプリを開き、 [CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API (、 [CameraCaptureUI サンプル](https://go.microsoft.com/fwlink/p/?linkid=228589)など)
2. タップして、**オプション**UI のボタン
3. 開き、**カメラ オプション**解像度とビデオの安定化を設定するための基本的なを示すフライアウト オプション
4. **カメラ オプション**フライアウトを表示 をタップ**より多くのオプション**
5. **より多くのオプション**フライアウトが表示されます
    - *Flyout の既定*カメラ用の UWP デバイス アプリがインストールされていない場合に表示されます
    - A*カスタム フライアウト*カメラ用の UWP デバイス アプリがインストールされている場合に表示されます

![カメラ オプションの詳細については、既定のフライアウトとカスタムのフライアウトのサイド バイ サイドでのイメージ](images/372745-cameraoptionslaunching.png)

このイメージは、カスタムのフライアウトの例の横にあるカメラ オプションの詳細について既定のフライアウトを示しています。

## <a name="prerequisites"></a>前提条件

開始する前に。

1. 開発用 PC の設定を取得します。 参照してください[Getting started](getting-started.md)については、ツールをダウンロードして開発者アカウントを作成します。
2. アプリをストアに関連付けます。 参照してください[UWP デバイスのアプリを作成](step-1--create-a-uwp-device-app.md)についてです。
3. アプリに関連付けているプリンター用のデバイス メタデータを作成します。 参照してください[デバイス メタデータを作成する](step-2--create-device-metadata.md)の詳細についてはします。
4. アプリのメイン ページの UI をビルドします。 表示されている全画面表示になりますが、最初からすべての UWP デバイス アプリを起動できます。 スタート エクスペリエンスを使用して、製品またはサービスに固有のブランドと一致する方法と、デバイスの機能を強調表示します。 使用できる UI コントロールの種類の特別な制限はありません。 全画面表示エクスペリエンスのデザインを開始するを参照してください。、 [Microsoft Store の設計原則](https://go.microsoft.com/fwlink/p/?LinkID=299845)します。

## <a name="step-1-register-the-extension"></a>手順 1:拡張機能を登録します。

Windows アプリでカメラ オプションの詳細についてカスタム フライアウトを供給できることを認識するには、カメラの設定の拡張機能を登録する必要があります。 この拡張機能が宣言されている、`Extension`要素で、`Category`属性の値に設定`windows.cameraSettings`します。 C#と C++ のサンプル、`Executable`属性に設定されて`DeviceAppForWebcam.exe`と`EntryPoint`属性に設定されて`DeviceAppForWebcam.App`します。

カメラの設定の拡張機能を追加することができます、**宣言**Microsoft Visual Studio でのマニフェスト デザイナーのタブ。 編集することも、アプリ パッケージ マニフェスト XML 手動で、XML (テキスト) エディターを使用します。 右クリックし、 **Package.appxmanifest**ファイル**ソリューション エクスプ ローラー**の編集オプション。

この例は、カメラの設定の拡張機能で、`Extension`アプリ パッケージのマニフェスト ファイルに要素が表示されます**Package.appxmanifest**します。

```XML
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
  <Identity Name="Microsoft.SDKSamples.DeviceAppForWebcam.CPP" Publisher="CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US" Version="1.0.0.0" />
  <Properties>
    <DisplayName>DeviceAppForWebcam CPP sample</DisplayName>
    <PublisherDisplayName>Microsoft Corporation</PublisherDisplayName>
    <Logo>Assets\storeLogo-sdk.png</Logo>
  </Properties>
  <Prerequisites>
    <OSMinVersion>6.3.0</OSMinVersion>
    <OSMaxVersionTested>6.3.0</OSMaxVersionTested>
  </Prerequisites>
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
  <Applications>
    <Application Id="DeviceAppForWebcam.App" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForWebcam.App">
      <VisualElements DisplayName="DeviceAppForWebcam CPP sample" Logo="Assets\squareTile-sdk.png" SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForWebcam CPP sample" ForegroundText="light" BackgroundColor="#00b2f0">
        <DefaultTile ShortName="DeviceApp CPP" ShowName="allLogos" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
      <Extensions>
        <Extension Category="windows.cameraSettings" Executable="DeviceAppForWebcam.exe" EntryPoint="DeviceAppForWebcam.App" />
      </Extensions>
    </Application>
  </Applications>
</Package>
```

## <a name="step-2-build-the-ui"></a>手順 2:UI を構築します。

アプリを構築する前に、デザイナーを使用する必要があり、ユーザーを設計するマーケティング チームが発生します。 ユーザー エクスペリエンスは、プロジェクトの自分の会社のブランド化の側面と、ユーザーとの接続を作成するため必要があります。

### <a name="design-guidelines"></a>設計ガイドライン

確認することが重要、 [UWP アプリのフライアウト ガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=317078)カスタムのフライアウトを設計する前にします。 ガイドラインは、フライアウトが他の UWP アプリで一貫性のある直感的な経験を提供することを確認するのに役立ちます。

アプリのメイン ページでは、Windows 8.1 が 1 つのモニターでさまざまなサイズで複数のアプリを表示できる注意してください。 画面サイズとウィンドウ サイズと向きの間で、アプリを適切にリフローできる方法の詳細については、次のガイドラインを参照してください。

- [ウィンドウ サイズと画面をスケーリングするためのガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=311830)
- [高さと幅の狭いレイアウトにウィンドウのサイズ変更するためのガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="flyout-dimensions"></a>フライアウトのディメンション

複数のカメラ オプションを表示するポップアップは 625 ピクセル、高さ、幅 340 ピクセルです。 領域を含む、**より多くのオプション**上部にあるテキストは Windows によって提供される、約 65 ピクセル高、まま 560 ピクセル カスタム ポップアップの表示可能領域の。 カスタムのフライアウトは 340 ピクセル幅を超えることはできません。

![カメラ オプションの詳細についてフライアウト ディメンション。](images/372776-camera-options-layout.png)

> [!NOTE]
> カスタムのフライアウトが複数の 560 ピクセルの場合は、ユーザーはスライドか、スクロール可能な領域の上下には、フライアウトの部分を表示することがあります。

### <a name="suggested-effects"></a>推奨の効果

- 色の効果。 たとえば、グレースケール、セピア、や solarizing 画像全体。
- 顔の追跡の効果。 顔が、画像と、hat や、眼鏡のペアなど、オーバーレイで識別されると、その上に追加されます。
- シーンのモード。 これらは、さまざまな照明条件のプリセットの露出とフォーカス モードです。

### <a name="suggested-settings"></a>おすすめの設定

- UWP デバイス アプリのカスタムのフライアウトは、製造元で提供される色補正パターンなどのハードウェア実装設定を有効にするためのスイッチを指定できます。
- UWP デバイス アプリによって公開されているその他の設定を補足する基本的なプロパティを実装します。 たとえば、多くのデバイスは、明るさ、コントラスト、ちらつき、フォーカス、および露出を調整するためのコントロールが公開される可能性が、明るさとコントラストを自動的に調整する true カラーを実装するデバイスは、これらの設定を指定する必要はありません。

### <a name="restrictions"></a>制限

- メイン アプリから UWP デバイス アプリのカスタムのフライアウトを開かないでください (呼び出すことによって、`CameraOptionsUI.Show`メソッド) と、アプリがストリーミングされるかをキャプチャします。

- プレビューを提供したり、それ以外の場合、UWP デバイス アプリのカスタム フライアウト内から、ビデオ ストリームの所有権を取得しないでください。 カスタムのフライアウトは、ビデオをキャプチャする別のアプリに対応するとして機能します。 キャプチャ アプリでは、ビデオ ストリームの所有権を保持します。 低レベルの Api を使用して、ビデオ ストリームにアクセスしようとすることはできません。 キャプチャ アプリが、ストリームへのアクセスを失い、予期しない動作が発生する可能性があります。

- カスタムのフライアウトの解像度を調整できません。

- ポップアップ、通知、またはカスタムのフライアウトのためのもので、領域外のダイアログ ボックスを表示しようとしないでください。 これらの種類のダイアログが許可されていません。

- カスタムのフライアウト内でのオーディオまたはビデオのキャプチャを開始できません。 カスタムのフライアウトは自体キャプチャを開始するのではなく、ビデオをキャプチャしている別のアプリを拡張するためのもの。 さらに、システム ダイアログで、トリガーする可能性がオーディオまたはビデオのキャプチャと、ポップアップ ダイアログ ボックスはカスタムのフライアウト内で許可されていません。

## <a name="step-3-handle-activation"></a>手順 3:アクティブ化の処理

これを実装する必要があります、アプリには、カメラの設定の拡張機能が宣言されているが場合、`OnActivated`アプリ アクティブ化イベントを処理するメソッド。 UWP アプリの場合、このイベントがトリガーされますを使用して、 [CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985)クラスを呼び出し、 [CameraOptionsUI.Show](https://go.microsoft.com/fwlink/p/?LinkId=317995)メソッド。 アプリのアクティブ化は、ときに、アプリはアプリの起動時にどのページが起動を選択できます。 アプリでカメラの設定の拡張機能が宣言されている、Windows はアクティブ化イベントの引数でビデオのデバイスに渡します。Windows.ApplicationModel.Activation.IActivatedEventArgs します。

アクティブ化は、カメラの設定の意図する UWP デバイスのアプリを確認できます (ユーザーがタップされただけを**より多くのオプション**で、**カメラ オプション**ダイアログ) ときに、イベント引数の`kind`プロパティは Windows.ApplicationModel.Activation.ActivationKind.CameraSettings です。

この例ではアクティブ化イベント ハンドラーを示しています、`OnActivated`ほどのメソッドに表示されます、 **App.xaml.cs**ファイル。 イベントの引数が Windows.ApplicationModel.Activation.CameraSettingsActivatedEventArgs としてキャストし、に送信される、`Initialize`カスタム ポップアップのメソッド (**DeviceAppPage.xaml.cs**)。

```CSharp
protected override void OnActivated(IActivatedEventArgs args)
{
    if (args.Kind == ActivationKind.CameraSettings)
    {
        base.OnActivated(args);
        DeviceAppPage page = new DeviceAppPage();
        Window.Current.Content = page;
        page.Initialize((CameraSettingsActivatedEventArgs)args);

        Window.Current.Activate();
    }
}
```

## <a name="step-4-control-settings-and-effects"></a>手順 4:制御の設定と効果

ときに、`Initialize`カスタム ポップアップのメソッド (**DeviceAppPage.xaml.cs**) が呼び出され、ビデオ デバイスがイベント引数を使用、フライアウトに渡されます。 これらの引数は、カメラを制御するためのプロパティを公開します。

- **引数。VideoDeviceController** Windows.Media.Devices.VideoDeviceController 型のオブジェクトのプロパティを提供します。 このオブジェクトは、標準の設定を調整するためのメソッドを提供します。
- **引数。VideoDeviceExtension**プロパティはカメラ driver MFT へのポインター。 このプロパティは、Driver MFT インターフェイスは公開されない場合は null になります。 カメラ ドライバーの仕様に関する詳細については、次を参照してください。[カメラ driver MFT 作成](creating-a-camera-driver-mft.md)です。

この例の一部を示しています、`Initialize`ほどのメソッドに表示されます、 **DeviceAppPage.xaml.cs**ファイル。 ここでは、ビデオ デバイスのコント ローラー (videoDevController オブジェクト) とカメラ driver MFT (lcWrapper オブジェクト) が作成され、現在のカメラ設定フライアウトが表示されます。

```CSharp
public void Initialize(CameraSettingsActivatedEventArgs args)
{
    videoDevController = (VideoDeviceController)args.VideoDeviceController;

    if (args.VideoDeviceExtension != null)
    {
        lcWrapper = new WinRTComponent();
        lcWrapper.Initialize(args.VideoDeviceExtension);
    }

    bool bAuto = false;
    double value = 0.0;

    if (videoDevController.Brightness.Capabilities.Step != 0)
    {
        slBrt.Minimum = videoDevController.Brightness.Capabilities.Min;
        slBrt.Maximum = videoDevController.Brightness.Capabilities.Max;
        slBrt.StepFrequency = videoDevController.Brightness.Capabilities.Step;
        videoDevController.Brightness.TryGetValue(out value);
        slBrt.Value = value;
    }
    else
    {
        slBrt.IsEnabled = false;
    }
    if (videoDevController.Brightness.Capabilities.AutoModeSupported)
    {
        videoDevController.Brightness.TryGetAuto(out bAuto);
        tsBrtAuto.IsOn = bAuto;
    }
    else
    {
        tsBrtAuto.IsOn = false;
        tsBrtAuto.IsEnabled = false;
    }

    if (videoDevController.Contrast.Capabilities.Step != 0)
    {
        slCrt.Minimum = videoDevController.Contrast.Capabilities.Min;
        slCrt.Maximum = videoDevController.Contrast.Capabilities.Max;
        slCrt.StepFrequency = videoDevController.Contrast.Capabilities.Step;
        videoDevController.Contrast.TryGetValue(out value);
        slCrt.Value = value;
    }
    else
    {
        slCrt.IsEnabled = false;
    }
    // . . .
    // . . .
    // . . .
```

MFT 方法については、カメラ ドライバー、 [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプル。 カメラ ドライバーの仕様に関する詳細については、次を参照してください。[カメラ driver MFT 作成](creating-a-camera-driver-mft.md)です。

## <a name="step-5-apply-changes"></a>手順 5:変更を適用します。

フライアウトのコントロールに変更を行ったときに、対応するコントロールの Changed イベントは、ビデオ デバイス コント ローラー (videoDevController オブジェクト) とカメラ driver MFT (lcWrapper オブジェクト) に変更を適用に使用されます。

この例に表示されるように、ビデオ デバイスのコント ローラーとカメラ driver MFT、変更を適用する変更されたメソッドを示します、 **DeviceAppPage.xaml.cs**ファイル。

```CSharp
protected void OnBrtAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Brightness.TrySetAuto(tsBrtAuto.IsOn);
    slBrt.IsEnabled = !tsBrtAuto.IsOn;
}

protected void OnBrtSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Brightness.TrySetValue(slBrt.Value);
}

protected void OnCrtAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Contrast.TrySetAuto(tsCrtAuto.IsOn);
    slCrt.IsEnabled = !tsCrtAuto.IsOn;
}

protected void OnCrtSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Contrast.TrySetValue(slCrt.Value);
}

protected void OnFocusAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Focus.TrySetAuto(tsFocusAuto.IsOn);
    slFocus.IsEnabled = !tsFocusAuto.IsOn;
}

protected void OnFocusSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Focus.TrySetValue(slFocus.Value);
}

protected void OnExpAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Exposure.TrySetAuto(tsExpAuto.IsOn);
    slExp.IsEnabled = !tsExpAuto.IsOn;
}

protected void OnExpSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Exposure.TrySetValue(slExp.Value);
}

protected void OnEffectEnabledToggleChanged(object sender, RoutedEventArgs e)
{
    if (tsEffectEnabled.IsOn)
    {
        lcWrapper.Enable();
    }
    else
    {
        lcWrapper.Disable();
    }
    slEffect.IsEnabled = tsEffectEnabled.IsOn;
}

protected void OnEffectSliderValueChanged(object sender, RoutedEventArgs e)
{
    lcWrapper.UpdateDsp(Convert.ToInt32(slEffect.Value));
}
```

## <a name="testing-your-app"></a>アプリのテスト

このセクションのカスタムのフライアウトを提供する UWP デバイス アプリをインストールする方法を説明します**より多くのオプション**で示した、カメラの[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプル。

UWP デバイス アプリをテストする前に、デバイス メタデータを使用して、カメラにリンクする必要があります。

- デバイスのアプリ情報を追加するプリンターのデバイス メタデータ パッケージのコピーする必要があります。 使用してビルドできるデバイス メタデータを持っていない場合、**デバイス メタデータの作成ウィザード**、トピックの説明に従って[UWP デバイス アプリのデバイス メタデータを作成する](https://go.microsoft.com/fwlink/p/?LinkId=313644)します。

    > [!NOTE]
    > 使用する、**デバイス メタデータの作成ウィザード**、Microsoft Visual Studio Professional、Microsoft、Visual Studio Ultimate をインストールする必要がありますまたは[スタンドアロン Windows 8.1 の SDK](https://go.microsoft.com/fwlink/p/?linkid=309209)、完了する前に、このトピックの手順を実行します。 Microsoft Visual Studio Express for Windows をインストールすると、ウィザードが含まれていない SDK のバージョンがインストールされます。

次の手順では、アプリをビルドし、デバイスのメタデータをインストールします。

1. テスト署名を有効にします。
    1. 開始、**デバイス メタデータの作成ウィザード**から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\をダブルクリックして、x86**DeviceMetadataWizard.exe**
    2. **ツール**メニューの **テスト署名を有効にする**します。

2. コンピューターを再起動します
3. ソリューション (.sln) ファイルを開くには、ソリューションをビルドします。 F7 キーを押すか**ビルド -&gt;ソリューションのビルド**サンプルが読み込まれた後は、上部のメニューから。

4. 接続を切断し、プリンターをアンインストールします。 Windows が次に、デバイスが検出されたときに更新済みのデバイス メタデータの読み取りができるように、この手順が必要です。
5. 編集し、デバイスのメタデータを保存します。 デバイス アプリをデバイスにリンクするには、デバイスでデバイス アプリを関連付ける必要があります。
    > [!NOTE]
    > デバイスのメタデータをまだ作成していない場合は、次を参照してください。 [UWP デバイス アプリのデバイス メタデータを作成する](https://go.microsoft.com/fwlink/p/?LinkId=313644)します。

    1. 場合、**デバイス メタデータの作成ウィザード**が開くまだ、開始から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\x86 により、ダブルクリック**DeviceMetadataWizard.exe**します。
    2. クリックして**デバイス メタデータの編集**します。 これからは、既存のデバイス メタデータ パッケージを編集できます。
    3. **オープン** ダイアログ ボックスで、UWP デバイス アプリに関連付けられている、デバイス メタデータ パッケージを見つけます。 (これが、 **devicemetadata ms**ファイル拡張子)。
    4. **指定 UWP デバイスのアプリ情報** ページで、Microsoft Store アプリの情報を入力、 **UWP デバイス アプリ**ボックス。 をクリックして**インポート UWP アプリのマニフェスト ファイル**自動的に入力する、**パッケージ名**、**パブリッシャー名**と**UWP アプリの ID**します。
    5. 完了したら、クリックして **[次へ]** に到達するまで、**完了**ページ。
    6. **デバイス メタデータ パッケージの確認** ページで、すべての設定が正しいことと選択するかどうかを確認、**デバイス メタデータ パッケージをローカル コンピューター上のメタデータ ストアにコピー**チェック ボックスをオンします。 クリックして**保存**します。

6. デバイスが接続されている場合、その Windows が更新されたデバイスのメタデータを読み取り、デバイスを再接続します。
    - 外部のカメラがあれば、単にカメラを接続します。
    - 内部のカメラを使っている場合は、デバイスとプリンター フォルダー内のコンピューターを更新します。 ハードウェアの変更をスキャンするには、デバイス マネージャーを使用します。 デバイスが検出されたときに、Windows は、更新されたメタデータをお読みください。

> [!NOTE]
> カメラ driver MFT をインストールする方法の詳細については、テスト」セクションを参照してください。[カメラ driver MFT 作成](creating-a-camera-driver-mft.md)です。

## <a name="testing-the-samples"></a>サンプルのテスト

オプションのカメラ エクスペリエンスをテストするには、まずこれらのサンプルをダウンロードします。

- [カメラのサンプルについては、UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)
- [カメラ キャプチャ UI サンプル](https://go.microsoft.com/fwlink/p/?linkid=228589)
- [Driver MFT サンプル](https://go.microsoft.com/fwlink/p/?LinkID=251566)

上の指示をテストするサンプルを次に、に従って、 [Driver MFT サンプル](https://go.microsoft.com/fwlink/p/?LinkID=251566)ページ。
