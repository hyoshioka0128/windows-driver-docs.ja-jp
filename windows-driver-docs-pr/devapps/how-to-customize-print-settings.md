---
title: 印刷の設定 (UWP デバイス アプリ) をカスタマイズする方法
description: このトピックでは、高度な印刷設定のフライアウトが導入されていて、表示する方法、C#の印刷設定と印刷通知のサンプルでは、既定のフライアウトはカスタム ポップアップ付きのバージョン。
ms.assetid: 099BD9B2-1AA6-49A5-AB84-0AF6FA0EFB26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 653724ee75540e1bcff7b23853696cd43d53edd1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330683"
---
# <a name="how-to-customize-print-settings-uwp-device-apps"></a>印刷の設定 (UWP デバイス アプリ) をカスタマイズする方法


Windows 8.1 では、UWP デバイス アプリは、カスタマイズの詳細設定のフライアウトを表示するプリンタの製造元を使用できます。 このトピックでは、高度な印刷設定のフライアウトが導入されていて、表示方法、C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル カスタム ポップアップ付きの既定のフライアウトが置き換えられます。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)使用して、 **Preferences.xaml**カスタム ポップアップの UI を示すためにページの印刷設定の詳細。 印刷のヘルパー クラスは、デバイス コンテキスト (IPrinterExtensionContext) を作成し、デバイス クエリの実行に使用されます。 **PrinterHelperClass.cs**ファイルは、 **DeviceAppForPrintersLibrary**プロジェクトで定義されている Api を使用して、 **PrinterExtensionLibrary**プロジェクト。 プリンターの拡張機能ライブラリでは、v4 印刷ドライバーのプリンター拡張機能のインターフェイスにアクセスする便利な手段を提供します。 詳細については、次を参照してください。、[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)します。

**注**  このトピックで示すコード例に基づいています、C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル。 このサンプルも JavaScript および C++ で使用できます。 C++ は COM を直接アクセスできるため、C++ のバージョン サンプルにはが含まれていないことコード ライブラリ プロジェクトに注意してください。 コードの最新バージョンを参照するサンプルをダウンロードします。

 

## <a name="span-idadvancedprintsettingsspanspan-idadvancedprintsettingsspanspan-idadvancedprintsettingsspanadvanced-print-settings"></a><span id="Advanced_print_settings"></span><span id="advanced_print_settings"></span><span id="ADVANCED_PRINT_SETTINGS"></span>高度な印刷設定


高度な印刷設定のエクスペリエンスは、ユーザーが [印刷] ウィンドウではご利用いただけません印刷設定を選択するときに、プリンターが提供される機能です。 アクセスできる、**詳細設定**[印刷] ウィンドウでリンクします。 全画面エクスペリエンスではありませんが、フライアウトを表示内では、ユーザーがクリックするか、外部でタップしたときに終了した軽量でコンテキストのユーザー インターフェイスを表示するためのコントロールが表示されます。

このエクスペリエンスは、ドキュメントのページに透かしを適用するには、セキュリティで保護された印刷オプション、または画像拡張機能のオプションが提供されて、プリンター機能などの差別化を強調表示機能を使用できます。

プリンターの UWP デバイスのアプリがインストールされていないときに、Windows は、既定の印刷設定のエクスペリエンスを提供します。 Windows ことを検出した場合、プリンターの UWP デバイスのアプリがインストールされていると、アプリで選択をする、`windows.printTaskSettings`拡張機能では、アプリが Windows によって提供される既定のエクスペリエンスを置き換えます。

高度な印刷設定のフライアウトを呼び出すには。

1.  印刷をサポートする UWP アプリを開く
2.  (または、Windows ロゴ キー + C を使用して)、画面の右側にある方向のスワイプ操作によって、チャームへのアクセスします。
3.  タップして、**デバイス**チャーム
4.  タップ**印刷**
5.  プリンターをタップします。
6.  **印刷**ウィンドウが開きます
7.  をクリックして、**詳細設定**リンクを**印刷**ウィンドウ
8.  高度な印刷設定のフライアウトが表示されます。
    -   *Flyout の既定*プリンター用の UWP デバイス アプリがインストールされていない場合に表示されます
    -   A*カスタム フライアウト*プリンター用の UWP デバイス アプリがインストールされている場合に表示されます

![既定とカスタムのフライアウトの高度な印刷設定の例。](images/373072-printer-settings-launch.png)

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


開始する前に。

1.  V4 印刷ドライバーを使用して、プリンターをインストールすることを確認します。 詳細については、次を参照してください。[開発 v4 印刷ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=314231)します。
2.  開発用 PC の設定を取得します。 参照してください[Getting started](getting-started.md)については、ツールをダウンロードして開発者アカウントを作成します。
3.  アプリをストアに関連付けます。 参照してください[UWP デバイスのアプリを作成](step-1--create-a-uwp-device-app.md)についてです。
4.  アプリに関連付けているプリンター用のデバイス メタデータを作成します。 参照してください[デバイス メタデータを作成する](step-2--create-device-metadata.md)の詳細についてはします。
5.  アプリのメイン ページの UI をビルドします。 表示されている全画面表示になりますが、最初からすべての UWP デバイス アプリを起動できます。 スタート エクスペリエンスを使用して、製品またはサービスに固有のブランドと一致する方法と、デバイスの機能を強調表示します。 使用できる UI コントロールの種類の特別な制限はありません。 全画面表示エクスペリエンスのデザインを開始するを参照してください。、 [Microsoft Store の設計原則](https://go.microsoft.com/fwlink/p/?LinkID=299845)します。
6.  使用してアプリを作成している記述しているかどうかはC#または JavaScript を追加、 **PrinterExtensionLibrary**と**DeviceAppForPrintersLibrary** UWP デバイスのアプリ ソリューションにプロジェクト。 これらのプロジェクト内の各を見つけることができます、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル。
    **注**  のための C++ COM に直接アクセスできる、C アプリの場合は、COM ベースのプリンター デバイス コンテキストを使用する別のライブラリを必要としません。

     

## <a name="span-idstep1registertheextensionspanspan-idstep1registertheextensionspanspan-idstep1registertheextensionspanstep-1-register-the-extension"></a><span id="Step_1__Register_the_extension"></span><span id="step_1__register_the_extension"></span><span id="STEP_1__REGISTER_THE_EXTENSION"></span>手順 1: 拡張機能を登録します。


Windows アプリが高度な印刷設定のカスタムのフライアウトを供給できることを認識するためには、印刷タスク設定の拡張機能の登録にする必要があります。 この拡張機能が宣言されている、`Extension`要素で、`Category`属性の値に設定`windows.printTaskSettings`します。 C#と C++ のサンプル、`Executable`属性に設定されて`$targetnametoken$.exe`と`EntryPoint`属性に設定されて`DeviceAppForPrinters.App`します。

印刷タスク設定の拡張機能を追加することができます、**宣言**Microsoft Visual Studio でのマニフェスト デザイナーのタブ。 編集することも、アプリ パッケージ マニフェスト XML 手動で、XML (テキスト) エディターを使用します。 右クリックし、 **Package.appxmanifest**ファイル**ソリューション エクスプ ローラー**の編集オプション。

この例は、印刷タスク設定の拡張機能で、`Extension`アプリ パッケージのマニフェスト ファイルに要素が表示されます**Package.appxmanifest**します。

```XML
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
  <Identity Name="Microsoft.SDKSamples.DeviceAppForPrinters.CS" Publisher="CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US" Version="1.0.0.0" />
  <Properties>
    <DisplayName>Device App For Printers C# sample</DisplayName>
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
    <Application Id="DeviceAppForPrinters" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App">
      <VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
<DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
<SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
      <Extensions>
<Extension Category="windows.backgroundTasks" EntryPoint="BackgroundTask.PrintBackgroundTask">
  <BackgroundTasks>
    <Task Type="systemEvent" />
  </BackgroundTasks>
</Extension>
<Extension Category="windows.printTaskSettings" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App" />
      </Extensions>
    </Application>
  </Applications>
</Package>
```

## <a name="span-idstep2buildtheuispanspan-idstep2buildtheuispanspan-idstep2buildtheuispanstep-2-build-the-ui"></a><span id="Step_2__Build_the_UI"></span><span id="step_2__build_the_ui"></span><span id="STEP_2__BUILD_THE_UI"></span>手順 2: UI を構築します。


アプリを構築する前に、デザイナーを使用する必要があり、ユーザーを設計するマーケティング チームが発生します。 ユーザー エクスペリエンスは、プロジェクトの自分の会社のブランド化の側面と、ユーザーとの接続を作成するため必要があります。

### <a name="span-iddesignguidelinesspanspan-iddesignguidelinesspanspan-iddesignguidelinesspandesign-guidelines"></a><span id="Design_guidelines"></span><span id="design_guidelines"></span><span id="DESIGN_GUIDELINES"></span>デザイン ガイドライン

確認することが重要、 [UWP アプリのフライアウト ガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=317078)カスタムのフライアウトを設計する前にします。 ガイドラインは、フライアウトが他の UWP アプリで一貫性のある直感的な経験を提供することを確認するのに役立ちます。

アプリのメイン ページでは、Windows 8.1 が 1 つのモニターでさまざまなサイズで複数のアプリを表示できる注意してください。 画面サイズとウィンドウ サイズと向きの間で、アプリを適切にリフローできる方法の詳細については、次のガイドラインを参照してください。

-   [ウィンドウ サイズと画面をスケーリングするためのガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=311830)
-   [高さと幅の狭いレイアウトにウィンドウのサイズ変更するためのガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="span-idflyoutdimensionsspanspan-idflyoutdimensionsspanspan-idflyoutdimensionsspanflyout-dimensions"></a><span id="Flyout_dimensions"></span><span id="flyout_dimensions"></span><span id="FLYOUT_DIMENSIONS"></span>フライアウトのディメンション

印刷の詳細設定のフライアウトを表示する 646 ピクセルが少なくとも 768 ピクセル高 (実際の高さは、ユーザーの画面の解像度によって異なります)。 フライアウトのタイトル領域の [戻る] ボタンは、Windows によって提供されます。 「アプリのタイトル」テキストは、アプリ マニフェストからのアプリのタイトルです。 タイトル領域は、80 のピクセルを高、カスタムのポップアップの表示可能領域の読み込みに 688 ピクセルのままです。

![高度なプリンターの設定のフライアウト ディメンション。](images/439446-printer-options-layout.png)

**注**  ユーザーがスライドまたはスクロール可能な領域の上下には、フライアウトの部分を表示する、カスタムのフライアウトが複数の読み込みに 688 ピクセルの場合は、します。

 

### <a name="span-iddefiningtheapptitlecolorandiconspanspan-iddefiningtheapptitlecolorandiconspanspan-iddefiningtheapptitlecolorandiconspandefining-the-app-title-color-and-icon"></a><span id="Defining_the_app_title_color_and_icon"></span><span id="defining_the_app_title_color_and_icon"></span><span id="DEFINING_THE_APP_TITLE_COLOR_AND_ICON"></span>アプリのタイトルの色とアイコンを定義します。

タイトル、背景色、テキストの色、およびカスタムのフライアウトの小さいロゴがから取得されます、`VisualElements`アプリ パッケージのマニフェスト ファイル内の要素。

この例では、タイトルとアイコンで定義されている、`VisualElements`アプリ パッケージのマニフェスト ファイル内の要素 (**Package.appxmanifest**)。

```XML
      <VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
        <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
```

### <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>ベスト プラクティス

-   **同じルック アンド フィールを維持します。** 開始エクスペリエンス (アプリのメイン ページ) の設計では、カスタムのフライアウトを配置、フォント、色、およびコントロールなどの要素を含むです。 アプリは、呼び出すことに関係なくユーザーに理解します。

-   **相互作用をシンプルにするには。** 時間のかかるまたは複雑な相互作用を回避します。 ほとんどの場合、プリンターを設定する、状態の表示、インク、順序付け、およびトラブルシューティングなどのアクションが最適なスタート エクスペリエンス内で実行します。

-   **ナビゲーションを最小限にしてください。** ユーザー、カスタムのフライアウトの複数のページ間を前後へ移動しないようにします。 代わりに、プログレッシブの公開コントロール、ドロップダウン リストを使って、インライン エラー メッセージなど、垂直方向のスクロールまたはインライン コントロールを使用します。

-   **ライトを使用しないフライアウトを無視します。** 印刷時の動作は、ライトを既に使用してフライアウトを無視します。 カスタム内の要素を無視するもう 1 つのライトを含むフライアウトは、ユーザーを混乱させることができます。

-   **印刷時の動作からユーザーのリンクを無効にします。** ユーザーがコンテンツを印刷するときは、印刷のコンテキストで常にしておくに手順を実行する必要があります。 たとえば、アプリに (ホーム ページか、またはインクの購入のページなど)、アプリの他の領域へのリンクがある場合は、する必要があります無効にするにユーザーは、高度な印刷設定のエクスペリエンスを誤って移動しないように。

## <a name="span-idstep3spanspan-idstep3spanstep-3-handle-activation"></a><span id="step3"></span><span id="STEP3"></span>手順 3:アクティブ化の処理


これを実装する必要があります、アプリには、印刷タスク設定の拡張機能が宣言されているが場合、`OnActivated`アプリ アクティブ化イベントを処理するメソッド。 アプリのアクティブ化は、ときに、アプリはアプリの起動時にどのページが起動を選択できます。 印刷タスク設定の拡張機能が宣言されているアプリ、Windows はアクティブ化イベントの引数で印刷タスク拡張機能のコンテキストに渡します。Windows.ApplicationModel.Activation.IActivatedEventArgs します。

UWP デバイスのアプリは、アクティブ化は、印刷の詳細設定を確認できます (ユーザーがタップされただけを**より多くのオプション**印刷設定 ダイアログ) ときに、イベント引数の`kind`プロパティと等しいWindows.ApplicationModel.Activation.ActivationKind.printTaskSettings します。

**注**  場合によっては、起動後すぐに、ユーザーがアプリを閉じる場合、例外スローされる可能性が、ライセンス認証ハンドラー内で。 これを避けるために、ライセンス認証ハンドラーが効率的に完了し、リソースを消費する処理を実行しないを確認します。

 

この例ではアクティブ化イベント ハンドラーを示しています、`OnActivated`ほどのメソッドに表示されます、 **Constants.cs**ファイル。 イベントの引数は、Windows.ApplicationModel.Activation.PrintTaskSettingsActivatedEventArgs としてし、キャストされます。 このサンプルでは、このコードが含まれますが、 **Constants.cs**ファイルで定義されている App クラスの一部では実際には、 **App.xaml.cs**ファイル。

```CSharp
partial class App : Application
{
    protected override void OnActivated(IActivatedEventArgs args)
    {
        if (args.Kind == ActivationKind.PrintTaskSettings)
        {
            Frame rootFrame = new Frame();
            if (null == Window.Current.Content)
            {
                rootFrame.Navigate(typeof(MainPage));
                Window.Current.Content = rootFrame;
            }
            Window.Current.Activate();

            MainPage mainPage = (MainPage)rootFrame.Content;

            // Load advanced printer preferences scenario
            mainPage.LoadAdvancedPrintSettingsContext((PrintTaskSettingsActivatedEventArgs)args);
        }
    }
}
```

## <a name="span-idstep4displaysettingsspanspan-idstep4displaysettingsspanspan-idstep4displaysettingsspanstep-4-display-settings"></a><span id="Step_4__Display_settings"></span><span id="step_4__display_settings"></span><span id="STEP_4__DISPLAY_SETTINGS"></span>手順 4: ディスプレイの設定


ときに、`LoadAdvancedPrintSettingsContext`メソッドが呼び出されると、印刷タスク構成のコンテキストは MainPage クラスの変数に割り当てられます。 これにより、印刷の設定へのアクセスの起動時にカスタムのポップアップが許可されます。

渡されるイベント引数、`LoadAdvancedPrintSettingsContext`メソッドにアクセスすると、プリンターを制御するプロパティを公開します。

-   **Args.configuration** Windows.Devices.Printers.Extensions.PrintTaskConfiguration 型のオブジェクトのプロパティを提供します。 このオブジェクトは、印刷タスク拡張機能のコンテキストにアクセスできるように、印刷チケットを更新するイベント ハンドラーを追加することもできます。
-   **Args.configuration.printerExtensionContext** Windows.Devices.Printers.Extensions.PrinterExtensionContext 型のオブジェクトのプロパティを提供します。 このオブジェクトは、印刷スキーマでは、PrintTicket、PrinterExtensionLibrary インターフェイスへのポインターし、キュー情報を出力します。 インターフェイスは公開されない場合は null になります。 詳細については、次を参照してください。[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)します。

この例では、`LoadAdvancedPrintSettingsContext`ほどのメソッドに表示されます、 **Constants.cs**ファイル。

```CSharp
public PrintTaskConfiguration Config;
public Object Context;

public void LoadAdvancedPrintSettingsContext(PrintTaskSettingsActivatedEventArgs args)
{
    Config = args.Configuration;
    Context = Config.PrinterExtensionContext;
    LoadScenario(typeof(DeviceAppForPrinters.Preferences));
}
```

カスタムのフライアウト ページで、 **Preferences.xaml.cs**、という名前のクラス`rootPage`印刷タスク拡張機能のコンテキストと、プリンター デバイス コンテキストは、ポップアップからアクセスできるように、MainPage クラスへのポインターとして機能します。

この例では、ポインターを示しますの一部で`Preferences`クラスから、 **Preferences.xaml.cs**ファイル。 ダウンロード、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルを完全なコードを参照してください。

```CSharp
public sealed partial class Preferences : SDKTemplate.Common.LayoutAwarePage
{
    // A pointer back to the main page.  
    MainPage rootPage = MainPage.Current;

    // To listen for save requests.
    PrintTaskConfiguration configuration;

    // To create the printer device context.
    Object printerExtensionContext;
    PrintHelperClass printHelper;

    // The features in this sample were chosen because they're available on a wide range of printer drivers.
    private string[] features = { "PageOrientation", "PageOutputColor", "PageMediaSize", "PageMediaType" };
    private string[] selections = { null, null, null, null };

    // . . .
    // . . .
    // . . .
```

ときにページのコンス トラクターの**Preferences.xaml.cs**が呼び出されると、印刷タスクの拡張コンテキストのオブジェクトは作成されます (、`PrintTaskConfiguraton`という名前のオブジェクト`configuration`) と、プリンター デバイス コンテキスト (、`PrintHelperClass`という名前のオブジェクト`printHelper`).

プリンター デバイス コンテキストが使用されるこれらのオブジェクトが作成された後、 `DisplaySettings` Textblock と ComboBoxs を読み込みます。 JavaScript とは異なりを選択範囲の変更は、アプリの残りの部分と同じスレッドでは起動されません。 後で使用するユーザーの選択項目のローカル キャッシュを管理する必要があります。

この例は、カスタムのポップアップ ページのコンス トラクターを示しています。 `DisplaySettings`、およびその他のヘルパー メソッド、 **Preferences.xaml.cs**ファイル。

```CSharp
public Preferences()
{
    this.InitializeComponent();

    configuration = rootPage.Config;
    printerExtensionContext = rootPage.Context;
    printHelper = new PrintHelperClass(printerExtensionContext);

    // Disable scenario navigation by hiding the scenario list UI elements
    ((UIElement)rootPage.FindName("Scenarios")).Visibility = Windows.UI.Xaml.Visibility.Collapsed;
    ((UIElement)rootPage.FindName("ScenarioListLabel")).Visibility = Windows.UI.Xaml.Visibility.Collapsed;
    ((UIElement)rootPage.FindName("DescriptionText")).Visibility = Windows.UI.Xaml.Visibility.Collapsed;

    DisplaySettings();
}


private void DisplaySettings(bool constraints=false)
{
    PrintOptions.Visibility = Windows.UI.Xaml.Visibility.Visible;
    WaitPanel.Visibility = Windows.UI.Xaml.Visibility.Collapsed;

    // Fill in the drop-down select controls for some common printing features.
    TextBlock[] featureLabels = { PageOrientationLabel, PageOutputColorLabel, PageMediaSizeLabel, PageMediaTypeLabel };
    ComboBox[] featureBoxes = { PageOrientationBox, PageOutputColorBox, PageMediaSizeBox, PageMediaTypeBox };

    for (int i = 0; i < features.Length; i++)
    {
        // Only display a feature if it exists
        featureLabels[i].Visibility = Windows.UI.Xaml.Visibility.Collapsed;
        featureBoxes[i].Visibility = Windows.UI.Xaml.Visibility.Collapsed;

        string feature = features[i];

        // Check whether the currently selected printer's capabilities include this feature.
        if (!printHelper.FeatureExists(feature))
        {
            continue;
        }

        // Fill in the labels so that they display the display name of each feature.
        featureLabels[i].Text = printHelper.GetFeatureDisplayName(feature);
        string[] index = printHelper.GetOptionInfo(feature, "Index");
        string[] displayName = printHelper.GetOptionInfo(feature, "DisplayName");
        string selectedOption = printHelper.GetSelectedOptionIndex(feature);

        // Unless specified, do not get constraints
        bool[] constrainedList = constraints ? printHelper.GetOptionConstraints(feature) : new bool[index.Length];

        // Populate the combo box with the options for the current feature.
        PopulateBox(featureBoxes[i], index, displayName, selectedOption, constrainedList);
        selections[i] = selectedOption;

        // Every time the selection for a feature changes, we update our local cached set of selections.
        featureBoxes[i].SelectionChanged += OnFeatureOptionsChanged;

        // Show existing features
        featureLabels[i].Visibility = Windows.UI.Xaml.Visibility.Visible;
        featureBoxes[i].Visibility = Windows.UI.Xaml.Visibility.Visible;
    }
}

void PopulateBox(ComboBox box, string[] index, string[] displayName, string selectedOption, bool[] constrainedList)
{
    // Clear the combobox of any options from previous UI refresh before repopulating it.
    box.SelectionChanged -= OnFeatureOptionsChanged;
    box.Items.Clear();
    // There should be only one displayName for each possible option.
    if (index.Length == displayName.Length)
    {
        for (int i = 0; i < index.Length; i++)
        {
            // Create a new DisplayItem so the user will see the friendly displayName instead of the index.
            ComboBoxItem newItem = new ComboBoxItem();
            newItem.Content = displayName[i];
            newItem.DataContext = index[i];
            newItem.Foreground = constrainedList[i] ? new SolidColorBrush(Colors.Red) : new SolidColorBrush(Colors.Black);
            box.Items.Add(newItem);

            // Display current selected option as selected in the combo box.
            if (selectedOption == index[i])
            {
                box.SelectedIndex = i;
                box.Foreground = newItem.Foreground;
            }
        }
    }
}

private void OnFeatureOptionsChanged(object sender, SelectionChangedEventArgs args)
{
    ComboBox comboBox = sender as ComboBox;

    for (int i = 0; i < features.Length; i++)
    {
        if (features[i] + "Box" == comboBox.Name)
        {
            selections[i] = (comboBox.SelectedItem as ComboBoxItem).DataContext as string;
        }
    }
}
```

## <a name="span-idstep5savesettingsspanspan-idstep5savesettingsspanspan-idstep5savesettingsspanstep-5-save-settings"></a><span id="Step_5__Save_settings"></span><span id="step_5__save_settings"></span><span id="STEP_5__SAVE_SETTINGS"></span>手順 5: 設定を保存します。


Microsoft Store のデバイス アプリをユーザーに戻る前に、変更を保存する必要があります、ユーザーは、高度な印刷設定が完了したら、**印刷**ウィンドウ。 そのためには、アプリは、ユーザーがタップすると、リッスンする必要があります、**戻る**(カスタム フライアウト ページ) からボタンをクリックします。 その場合、`SaveRequested`印刷タスク拡張コンテキストのイベント (、`configuration`オブジェクト) がトリガーされます。

この例でのイベント リスナー`SaveRequested`で追加される、`OnNavigatedTo`カスタム フライアウトのイベント ハンドラーで、 **Preferences.xaml.cs**ファイル。 ときに、`SaveRequested`イベントがトリガーされる、`OnSaveRequested`メソッドが呼び出されます (そのメソッドにも格納されます、 **Preferences.xaml.cs**ファイル)。

```CSharp
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    if (null == configuration)
    {
        rootPage.NotifyUser("Configuration arguments cannot be null", NotifyType.ErrorMessage);
        return;
    }

    // Add an event listener for saverequested (the back button of the flyout is pressed).
    configuration.SaveRequested += OnSaveRequested;
}
```

`OnSaveRequested`メソッドでは、アプリが最初使用して、`printHelper`プリンター拡張のコンテキストで各機能の現在選択されているオプションを設定するオブジェクト。 呼び出して、`Save`メソッドを`request`オブジェクトへの引数として渡される、`OnSaveRequested`メソッド。 `Save` Windows.Devices.Printers.Extensions.PrintTaskConfigurationSaveRequest クラスからのメソッドでは、プリンター拡張のコンテキストを使用して、印刷チケットの検証を印刷タスクの構成を保存します。

**重要な**  印刷チケットが何らかの方法で有効でない場合、`Save`メソッドは、アプリを扱う必要がある例外をスローします。 アプリでは、例外を処理しない場合、フローが停止している、光にユーザーを強制的、ポップアップを閉じるし、印刷のフローが再起動します。

 

この例では、`OnSaveRequested`メソッドで、 **Preferences.xaml.cs**ファイル。 `SaveRequested`イベントは、UI スレッドで発生せず、Windows.UI.Core.CoreDispatcher を使用して、検証やチケットの保存中に適切なメッセージを表示する UI スレッドにメッセージを送信する必要があります。

```CSharp
async private void OnSaveRequested(object sender, PrintTaskConfigurationSaveRequestedEventArgs args)
{
    if (null == printHelper || null == printerExtensionContext || null == args)
    {
        await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
        {
            rootPage.NotifyUser("onSaveRequested: args, printHelper, and context cannot be null", NotifyType.ErrorMessage);
        });
        return;
    }

    // Get the request object, which has the save method that allows saving updated print settings.
    PrintTaskConfigurationSaveRequest request = args.Request;

    if (null == request)
    {
        await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
        {
            rootPage.NotifyUser("onSaveRequested: request cannot be null", NotifyType.ErrorMessage);
        });
        return;
    }

    PrintTaskConfigurationSaveRequestedDeferral deferral = request.GetDeferral();

    // Two separate messages are dispatched to:
    // 1) put up a popup panel,
    // 2) set the each options to the print ticket and attempt to save it,
    // 3) tear down the popup panel if the print ticket could not be saved.
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        PrintOptions.Visibility = Windows.UI.Xaml.Visibility.Collapsed;
        WaitPanel.Visibility = Windows.UI.Xaml.Visibility.Visible;
    });

    // Go through all the feature select elements, look up the selected
    // option name, and update the context
    // for each feature
    for (var i = 0; i < features.Length; i++)
    {
        // Set the feature's selected option in the context's print ticket.
        // The printerExtensionContext object is updated with each iteration of this loop
        printHelper.SetFeatureOption(features[i], selections[i]);
    }
    
    bool ticketSaved;
    try
    {
        // This save request will throw an exception if ticket validation fails.
        // When the exception is thrown, the app flyout will remain.
        // If you want the flyout to remain regardless of outcome, you can call
        // request.Cancel(). This should be used sparingly, however, as it could
        // disrupt the entire the print flow and will force the user to 
        // light dismiss to restart the entire experience.
        request.Save(printerExtensionContext);

        if (configuration != null)
        {
            configuration.SaveRequested -= OnSaveRequested;
        }
        ticketSaved = true;
    }
    catch (Exception exp)
    {
        // Check if the HResult from the exception is from an invalid ticket, otherwise rethrow the exception
        if (exp.HResult.Equals(unchecked((int)0x8007000D))) // E_INVALID_DATA
        {
            ticketSaved = false;
        }
        else
        {
            throw;
        }
    }

    // If ticket isn't saved, refresh UI and notify user
    if (!ticketSaved)
    {
        await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
        {
            rootPage.NotifyUser("Failed to save the print ticket", NotifyType.ErrorMessage);
            DisplaySettings(true);
        });
    }
    deferral.Complete();
}
```

### <a name="span-idsavingoptionsthatrequireuserinputspanspan-idsavingoptionsthatrequireuserinputspanspan-idsavingoptionsthatrequireuserinputspansaving-options-that-require-user-input"></a><span id="Saving_options_that_require_user_input"></span><span id="saving_options_that_require_user_input"></span><span id="SAVING_OPTIONS_THAT_REQUIRE_USER_INPUT"></span>ユーザー入力を必要とするオプションを保存しています

[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルは、ほとんどの印刷オプションの対象とする定義済みの機能を設定する方法を示します。 ただし、いくつかのオプションでは、ユーザー指定の値を取得するためのカスタム UI が必要です。 たとえば、アプリは、カスタム ページのサイズを指定する高度な印刷設定を使用する場合は、ユーザーが指定した値を保存する次の手順がかかるは。

1.  アプリのアクティブ化中に印刷チケットを取得します。 印刷設定アプリのアクティブ化が前に説明されている[手順 3。アクティブ化処理](#step3)します。

2.  ページ サイズのオプションが指定されているかどうかを確認します。 C# JS アプリでは、印刷のヘルパー クラスは、このオプションを確認できますか。 C++ アプリでの QueryInterface IPrintSchemaPageMediaSizeOption を取得する IPrintSchemaOption を呼び出します。

    この例では、ページ サイズのオプションが指定されているかどうかにチェックする印刷ヘルパー クラスでメソッドを示します。

    ```CSharp
    public bool ShouldShowCustomUI(string index)
    {
        if (null != index)
        {
            string feature = "PageMediaSize";
            int i = int.Parse(index);
            IPrintSchemaOption selectedOption = GetCachedFeatureOptions(feature)[i];
            if (selectedOption.Name.Equals("CustomMediaSize", StringComparison.CurrentCulture) 
                || selectedOption.Name.Equals("PSCustomMediaSize", StringComparison.CurrentCulture))
            {
                return true;
            }
        }
        return false;
    }
    ```

3.  カスタムのフライアウトでは、カスタム UI ページの高さと幅をユーザーに要求を表示し、IPrintSchemaPageMediaSizeOption からユーザーが指定した高さと幅を取得します。

    この例では、ページの高さと幅のユーザーを確認するカスタム ポップアップのメソッドを使用します。

    ```CSharp
    private void ShowCustomPageMediaSizeUI(string index, bool keepValue)
    {
        //Hide custom media size UI unless needed
        if (IsCustomSizeSelected(index))
        {
           if (keepValue && (!customWidth.Equals("")) && (!customHeight.Equals("")))
           {
                        CustomWidthBox.Text = customWidth;
                        CustomHeightBox.Text = customHeight;
           }
           else
           {
              // Use a helper function from the WinRT helper component
              CustomWidthBox.Text = printHelper.GetCustomWidth(index);
              CustomHeightBox.Text = printHelper.GetCustomHeight(index);
           }
           CustomUIPanel.Visibility = Windows.UI.Xaml.Visibility.Visible;
           CustomWidthBox.KeyDown += OnCustomValueEntered;
           CustomHeightBox.KeyDown += OnCustomValueEntered;
        }
        else
        {
           CustomUIPanel.Visibility = Windows.UI.Xaml.Visibility.Collapsed;
           CustomWidthBox.KeyDown -= OnCustomValueEntered;
           CustomHeightBox.KeyDown -= OnCustomValueEntered;
        }
    }
    ```

4.  更新プログラム、`IPrintSchemaPageMediaSizeOption`ユーザーが指定した値し、高さと幅が、ユーザーが指定した値と一致することを検証します。

    この例は、更新するためのヘルパー メソッド、`IPrintSchemaPageMediaSizeOption`プリンター ヘルパー クラス内のオブジェクト。 `OnSaveRequested`カスタム ページ サイズのオプションが要求されたと判断した場合、カスタム フライアウトのハンドラーはこの関数を呼び出すとします。

    ```CSharp
    public void SetCustomMediaSizeDimensions(string width, string height)
    {
      if ((null == width) && (null == height) && (null == Capabilities))
      {
                    return;
      }
      try
      {
                    CheckSizeValidity(width, height);
      }
      catch (FormatException e)
      {
                    throw new ArgumentException(e.Message);
      }
      catch (OverflowException e)
      {
                    throw new ArgumentException(e.Message);
      }

      // The context is retrieved during app activation.
      IPrintSchemaTicket ticket = context.Ticket;

      //
      // Input XML as Stream
      //
      XElement ticketRootXElement = null;
      using (Stream ticketReadStream = ticket.GetReadStream())
      {
         ticketRootXElement = XElement.Load(ticketReadStream);
      }

      XNamespace psfNs = PrintSchemaConstants.FrameworkNamespaceUri;
      XNamespace pskNs = PrintSchemaConstants.KeywordsNamespaceUri;
      string pskPrefix = ticketRootXElement.GetPrefixOfNamespace(pskNs);

      // Modify the MediaSizeHeight and MediaSizeWidth
      IEnumerable<XElement> parameterInitCollection = 
        from c in ticketRootXElement.Elements(psfNs + "ParameterInit")
                                                                
      select c;

      foreach (XElement parameterInit in parameterInitCollection)
      {
        if (0 == String.Compare((string)parameterInit.Attribute("name"), pskPrefix + ":PageMediaSizePSWidth"))
        {
          IEnumerable<XElement> valueCollection = from c in parameterInit.Elements(psfNs + "Value")
          select c;
          valueCollection.ElementAt(0).Value = width;
        }

         else if (0 == String.Compare((string)parameterInit.Attribute("name"), pskPrefix + ":PageMediaSizePSHeight"))
        {
          IEnumerable<XElement> valueCollection = from c in parameterInit.Elements(psfNs + "Value")
          select c;
          valueCollection.ElementAt(0).Value = height;
         }
      }

      //
      // Write XLinq changes back to DOM
      //
       using (Stream ticketWriteStream = ticket.GetWriteStream())
       {
         ticketRootXElement.Save(ticketWriteStream);
       }
    }
    ```

## <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>テスト


UWP デバイス アプリをテストする前に、デバイス メタデータを使用して、プリンターにリンクする必要があります。

-   デバイスのアプリ情報を追加するプリンターのデバイス メタデータ パッケージのコピーする必要があります。 使用してビルドできるデバイス メタデータを持っていない場合、**デバイス メタデータの作成ウィザード**、トピックの説明に従って[UWP デバイス アプリのデバイス メタデータを作成する](https://go.microsoft.com/fwlink/p/?LinkId=313644)します。

    **注**  を使用する、**デバイス メタデータの作成ウィザード**、Microsoft Visual Studio Professional、Microsoft、Visual Studio Ultimate をインストールする必要がありますまたは[スタンドアロン Windows 8.1 の SDK](https://go.microsoft.com/fwlink/p/?linkid=309209)、このトピックの手順を完了する前にします。 Microsoft Visual Studio Express for Windows をインストールすると、ウィザードが含まれていない SDK のバージョンがインストールされます。

     

次の手順では、アプリをビルドし、デバイスのメタデータをインストールします。

1.  テスト署名を有効にします。
    1.  開始、**デバイス メタデータの作成ウィザード**から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\をダブルクリックして、x86**DeviceMetadataWizard.exe**
    2.  **ツール**メニューの **テスト署名を有効にする**します。

2.  コンピューターを再起動します
3.  ソリューション (.sln) ファイルを開くには、ソリューションをビルドします。 F7 キーを押すか**ビルド -&gt;ソリューションのビルド**サンプルが読み込まれた後は、上部のメニューから。

4.  接続を切断し、プリンターをアンインストールします。 Windows が次に、デバイスが検出されたときに更新済みのデバイス メタデータの読み取りができるように、この手順が必要です。
5.  編集し、デバイスのメタデータを保存します。 デバイス アプリをデバイスにリンクするには、デバイスでデバイス アプリを関連付ける必要があります**注**  デバイスのメタデータをまだ作成していない場合は、次を参照してください[UWPデバイスアプリのデバイスメタデータを作成する](https://go.microsoft.com/fwlink/p/?LinkId=313644).

     

    1.  場合、**デバイス メタデータの作成ウィザード**が開くまだ、開始から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\x86 により、ダブルクリック**DeviceMetadataWizard.exe**します。
    2.  クリックして**デバイス メタデータの編集**します。 これからは、既存のデバイス メタデータ パッケージを編集できます。
    3.  **オープン** ダイアログ ボックスで、UWP デバイス アプリに関連付けられている、デバイス メタデータ パッケージを見つけます。 (これが、 **devicemetadata ms**ファイル拡張子)。
    4.  **指定 UWP デバイスのアプリ情報** ページで、Microsoft Store アプリの情報を入力、 **UWP デバイス アプリ**ボックス。 をクリックして**インポート UWP アプリのマニフェスト ファイル**自動的に入力する、**パッケージ名**、**パブリッシャー名**と**UWP アプリの ID**します。
    5.  場合は、アプリは、プリンターの通知の登録は、入力、**通知ハンドラー**ボックス。 **イベント ID**、印刷イベント ハンドラーの名前を入力します。 **イベント資産**、そのコードが存在するファイルの名前を入力します。

    6.  完了したら、クリックして **[次へ]** に到達するまで、**完了**ページ。
    7.  **デバイス メタデータ パッケージの確認** ページで、すべての設定が正しいことと選択するかどうかを確認、**デバイス メタデータ パッケージをローカル コンピューター上のメタデータ ストアにコピー**チェック ボックスをオンします。 クリックして**保存**します。

6.  デバイスが接続されている場合、その Windows が更新されたデバイスのメタデータを読み取り、プリンターに再接続します。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>トラブルシューティング


### <a name="span-idissueadvancedprintsettingsshowsdefaultflyoutinsteadofcustomflyoutspanspan-idissueadvancedprintsettingsshowsdefaultflyoutinsteadofcustomflyoutspanspan-idissueadvancedprintsettingsshowsdefaultflyoutinsteadofcustomflyoutspanissue-advanced-print-settings-shows-default-flyout-instead-of-custom-flyout"></a><span id="Issue__Advanced_print_settings_shows_default_flyout_instead_of_custom_flyout"></span><span id="issue__advanced_print_settings_shows_default_flyout_instead_of_custom_flyout"></span><span id="ISSUE__ADVANCED_PRINT_SETTINGS_SHOWS_DEFAULT_FLYOUT_INSTEAD_OF_CUSTOM_FLYOUT"></span>問題:カスタムのフライアウトではなく印刷設定示します既定フライアウトの詳細

高度な印刷設定フライアウトにより、アプリを実装するカスタムのフライアウトの代わりに既定のフライアウトが表示されます.

-   **考えられる原因:** テスト署名が有効になっていません。 有効にする方法については、このトピックでは、"デバッグ"を参照してください。

-   **考えられる原因:** アプリには、右側のパッケージ ファミリ名のクエリいないいます。 コード内のパッケージ ファミリ名を確認します。 開いて**package.appxmanifest**で Visual Studio を確認する、パッケージ ファミリ名のクエリには構造と一致する、**パッケージ** タブのパッケージ ファミリ名のフィールド。

-   **考えられる原因:** デバイス メタデータは、パッケージ ファミリ名に関連付けられています。 使用して、**デバイス メタデータの作成ウィザード**をデバイスのメタデータを開き、パッケージ ファミリ名を確認します。 ウィザードを開始します *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\をダブルクリックして、x86 **DeviceMetadataWizard.exe**します。

### <a name="span-idissueappislaunchedinflyoutthenisimmediatelydismissedspanspan-idissueappislaunchedinflyoutthenisimmediatelydismissedspanspan-idissueappislaunchedinflyoutthenisimmediatelydismissedspanissue-app-is-launched-in-flyout-then-is-immediately-dismissed"></a><span id="Issue__App_is_launched_in_flyout_then_is_immediately_dismissed"></span><span id="issue__app_is_launched_in_flyout_then_is_immediately_dismissed"></span><span id="ISSUE__APP_IS_LAUNCHED_IN_FLYOUT_THEN_IS_IMMEDIATELY_DISMISSED"></span>問題:アプリは、フライアウトでを起動しがすぐに閉じられます

場合は、カスタムのフライアウトの高度な印刷設定は後すぐに表示されなくなりますが起動しています.

-   **考えられる原因:** Windows 8 では、既知の問題、フライアウトを内は、UWP アプリをデバッガーで破棄がすることです。 ライセンス認証の動作がわかると、今度のデバッグを無効にします。 デバッグ印刷チケットを保存する必要がある場合は、アクティブ化の後、デバッガーをアタッチします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[プリンター拡張機能インターフェイス (v4 印刷ドライバー)](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[アプリを作成する UWP デバイス (ステップ バイ ステップ ガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスのアプリ (ステップ バイ ステップ ガイド) のデバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 






