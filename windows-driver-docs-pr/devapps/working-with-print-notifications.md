---
title: UWP デバイス アプリでの印刷通知の操作
description: このトピックでは、印刷の通知が導入されていて、表示する方法、C#バージョンの印刷設定と印刷通知のサンプルでは、バック グラウンド タスクを使用して、印刷通知に応答します。
ms.assetid: 39A06A8A-5603-44AB-8884-C12B8E2F1A45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 468b48b01067b8387ec7f4be7a3850c37f789156
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350133"
---
# <a name="working-with-print-notifications-in-a-uwp-device-app"></a>UWP デバイス アプリでの印刷通知の操作


Windows 8.1 で UWP デバイス アプリは、v4 印刷ドライバーから送信される双方向通信 (Bidi) イベントに応答できます。 このトピックでは、印刷の通知が導入されていて、表示方法、C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルでは、バック グラウンド タスクを使用して、印刷通知に応答します。 バック グラウンド タスクでは、ローカルのアプリ データの詳細の保存、トーストを送信、タイルおよびバッジの更新の通知を保存する方法を示します。 一般に UWP デバイス アプリの詳細について、[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)を参照してください。

C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルでは、アプリのバック グラウンド部分 (*バック グラウンド タスク*) で、 **BackgroundTask**プロジェクト。 バック グラウンド タスクのコードは、 **PrintBackgroundTask.cs**ファイル。 *フォア グラウンド アプリ*、[スタート] から起動できる全画面表示アプリは、 **DeviceAppForPrinters**プロジェクト。 **InkLevel.xaml.cs**ファイルは、通知の詳細をフォア グラウンド アプリからアクセスできることという 1 つの方法を示します。 サンプルを印刷通知を使用するでプリンターの拡張機能ライブラリを使用して、 **PrinterExtensionLibrary**プロジェクト。 プリンターの拡張機能ライブラリでは、v4 印刷ドライバーのプリンター拡張機能のインターフェイスにアクセスする便利な手段を提供します。 詳細については、、[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)を参照してください。

**注**  このトピックで示すコード例に基づいています、C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル。 このサンプルも JavaScript および C++ で使用できます。 C++ は COM を直接アクセスできるため、C++ のバージョン サンプルにはが含まれていないことコード ライブラリ プロジェクトに注意してください。 コードの最新バージョンを参照するサンプルをダウンロードします。

 

## <a name="span-idprintnotificationsspanspan-idprintnotificationsspanspan-idprintnotificationsspanprint-notifications"></a><span id="Print_notifications"></span><span id="print_notifications"></span><span id="PRINT_NOTIFICATIONS"></span>印刷の通知


印刷の通知は、紙詰まりなどの印刷、プリンターのドア、低のインク レベル、またはプリンターの紙不足エラーを開くときに重要なプリンター イベントをユーザーに通知 UWP デバイス アプリを使用できます。 プリンターには、通知がトリガーされた場合は、システム イベント ブローカーは、アプリのバック グラウンド タスクを実行します。 そこから、バック グラウンド タスクできます通知の詳細を保存、トーストを送信、タイルを更新、更新、バッジ、または何もしません。 通知の詳細を保存することによって、アプリがユーザーを把握し、そのプリンターの問題の解決に役立つ、エクスペリエンスを提供できます。

**注**  プリンタの製造元は、UWP デバイス アプリを使用して印刷通知の使用は、v4 印刷ドライバーで Bidi と DriverEvent XML ファイルを実装する必要があります。 詳細については、[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)を参照してください。

 

DriverEvent が発生すると、UWP デバイス アプリのバック グラウンド タスクを開始、アプリは、続行する方法に関していくつかのオプションが。 タスクの起動に潜在顧客のフローに関する詳細については、[UI のカスタマイズのドライバー サポート](https://msdn.microsoft.com/library/windows/hardware/jj659898)を参照してください。

バック グラウンド タスクを選択できます。

-   何もしない
-   通知の詳細を保存[アプリのローカル データ ストア](https://go.microsoft.com/fwlink/p/?LinkId=317216)
-   更新プログラム、 [UWP アプリのタイル通知](https://go.microsoft.com/fwlink/p/?LinkId=317195)
-   更新プログラム、 [UWP アプリの通知のバッジ](https://go.microsoft.com/fwlink/p/?LinkId=317196)
-   送信、 [UWP アプリのトースト通知](https://go.microsoft.com/fwlink/p/?LinkId=317197)

タイル通知、トースト通知は、ユーザーを簡単にフォア グラウンド アプリを起動させることができます。 フォア グラウンド アプリが起動され、ときに使用できる、`OnLaunched`メソッド**App.xaml.cs**タイルやトーストによって起動されたかどうかにチェックします。 フォア グラウンド アプリから、印刷通知の詳細でアクセスした場合、[アプリのローカル データ ストア](https://go.microsoft.com/fwlink/p/?LinkId=317216)します。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


開始する前に。

1.  V4 印刷ドライバーを使用して、プリンターをインストールすることを確認します。 詳細については、[開発 v4 印刷ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=314231)を参照してください。
2.  開発用 PC の設定を取得します。 参照してください[Getting started](getting-started.md)については、ツールをダウンロードして開発者アカウントを作成します。
3.  アプリをストアに関連付けます。 参照してください[UWP デバイスのアプリを作成](step-1--create-a-uwp-device-app.md)についてです。
4.  アプリに関連付けているプリンター用のデバイス メタデータを作成します。 参照してください[デバイス メタデータを作成する](step-2--create-device-metadata.md)の詳細についてはします。
5.  アプリのメイン ページの UI をビルドします。 表示されている全画面表示になりますが、最初からすべての UWP デバイス アプリを起動できます。 スタート エクスペリエンスを使用して、製品またはサービスに固有のブランドと一致する方法と、デバイスの機能を強調表示します。 使用できる UI コントロールの種類の特別な制限はありません。 全画面表示エクスペリエンスのデザインを開始するを参照してください。、 [Microsoft Store の設計原則](https://go.microsoft.com/fwlink/p/?LinkID=299845)します。
6.  使用してアプリを作成している記述しているかどうかはC#または JavaScript を追加、 **PrinterExtensionLibrary**と**DeviceAppForPrintersLibrary** UWP デバイスのアプリ ソリューションにプロジェクト。 これらのプロジェクト内の各を見つけることができます、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル。
    **注**  のための C++ COM に直接アクセスできる、C アプリの場合は、COM ベースのプリンター デバイス コンテキストを使用する別のライブラリを必要としません。

     

## <a name="span-idstep1registerbackgroundtaskspanspan-idstep1registerbackgroundtaskspanspan-idstep1registerbackgroundtaskspanstep-1-register-background-task"></a><span id="Step_1__Register_background_task"></span><span id="step_1__register_background_task"></span><span id="STEP_1__REGISTER_BACKGROUND_TASK"></span>手順 1: バック グラウンド タスクを登録します。


Windows アプリが印刷通知を処理できることを認識するためには、印刷通知のバック グラウンド タスクの拡張機能の登録にする必要があります。 この拡張機能が宣言されている、`Extension`要素で、`Category`属性に設定`windows.backgroundTasks`と`EntryPoint`属性に設定`BackgroundTask.PrintBackgroundTask`します。 拡張機能も含まれています、`Task`要素をサポートしていることを示す`systemEvent`タスクの種類。

印刷のバック グラウンド タスクの拡張機能を追加することができます、**宣言**Microsoft Visual Studio でのマニフェスト デザイナーのタブ。 編集することも、アプリ パッケージ マニフェスト XML 手動で、XML (テキスト) エディターを使用します。 右クリックし、 **Package.appxmanifest**ファイル**ソリューション エクスプ ローラー**の編集オプション。

この例は、バック グラウンド タスクの拡張機能で、`Extension`アプリ パッケージのマニフェスト ファイルに要素が表示されます**Package.appxmanifest**します。

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
      <VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" 
                      SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" 
                      ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
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

## <a name="span-idstep2configuredevicemetadataspanspan-idstep2configuredevicemetadataspanspan-idstep2configuredevicemetadataspanstep-2-configure-device-metadata"></a><span id="Step_2__Configure_device_metadata"></span><span id="step_2__configure_device_metadata"></span><span id="STEP_2__CONFIGURE_DEVICE_METADATA"></span>手順 2: デバイスのメタデータを構成します。


使用している場合、**デバイス メタデータの作成ウィザード**にアプリをデバイスに関連付ける、完全なことを確認する、**通知ハンドラー**ボックスに、**指定 UWP デバイスのアプリ情報**ページ。 これにより、その印刷通知中に、アプリのバック グラウンド タスクが呼び出されることを確認できます。

デバイスのメタデータを編集する方法の詳しい手順については、「、[テスト](#testing)セクション。

## <a name="span-idstep3buildtheuispanspan-idstep3buildtheuispanspan-idstep3buildtheuispanstep-3-build-the-ui"></a><span id="Step_3__Build_the_UI"></span><span id="step_3__build_the_ui"></span><span id="STEP_3__BUILD_THE_UI"></span>手順 3: UI を構築します。


アプリを構築する前に、デザイナーを使用する必要があり、ユーザーを設計するマーケティング チームが発生します。 ユーザー エクスペリエンスは、プロジェクトの自分の会社のブランド化の側面と、ユーザーとの接続を作成するため必要があります。

### <a name="span-iddesignguidelinesspanspan-iddesignguidelinesspanspan-iddesignguidelinesspandesign-guidelines"></a><span id="Design_guidelines"></span><span id="design_guidelines"></span><span id="DESIGN_GUIDELINES"></span>デザイン ガイドライン

タイルおよびバッジのエクスペリエンスを設計する前に、Microsoft Store アプリのガイドラインを確認するのには重要です。 ガイドラインように、アプリが他の UWP アプリで一貫性のある直感的な経験を提供します。

-   [タイルとバッジのガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=317194)
-   [トースト通知のガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=317193)

アプリのメイン ページでは、Windows 8.1 が 1 つのモニターでさまざまなサイズで複数のアプリを表示できる注意してください。 画面サイズとウィンドウ サイズと向きの間で、アプリを適切にリフローできる方法の詳細については、次のガイドラインを参照してください。

-   [ウィンドウ サイズと画面をスケーリングするためのガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=311830)
-   [高さと幅の狭いレイアウトにウィンドウのサイズ変更するためのガイドライン](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>ベスト プラクティス

-   **通知アクションの単語は含まれていません。** 通知メッセージには、プッシュ を押すと、または 通知 をクリックするユーザーを示すテキストを使用しないでください。 ユーザーは、詳細情報を調べるためのトーストを押すことができますを既に理解しています。 たとえばだけ書き込み「、プリンターはインクが不足」の代わりに"プリンターはインクが不足します。 キーを押してのトラブルシューティングを行う"。

-   **相互作用をシンプルにするには。** 通知のエクスペリエンスに表示されるすべての通知に関連付ける必要があります。 たとえば、用紙が詰まるについての通知 ページは、リンクとその問題を解決する方法についてする必要がありますのみ含まれます。 含めることはできません関連のないエクスペリエンスへのリンクこのような購入インクまたは他のサポート情報。

-   **マルチ メディアを使用します。** 使用して実際の写真、ビデオ、またはイラストを簡単にユーザーがデバイスの問題の解決がデバイスを使用します。

-   **アプリのコンテキスト内でユーザーを保持します。** 問題に関する情報を提供するときに、オンライン、またはその他のサポート資料はリンクしません。 アプリのコンテキストでユーザーを保持します。

## <a name="span-idstep4createbackgroundtaskspanspan-idstep4createbackgroundtaskspanspan-idstep4createbackgroundtaskspanstep-4-create-background-task"></a><span id="Step_4__Create_background_task"></span><span id="step_4__create_background_task"></span><span id="STEP_4__CREATE_BACKGROUND_TASK"></span>手順 4: バック グラウンド タスクを作成します。


印刷通知のバック グラウンド タスクを登録すると、アプリの場合、バック グラウンド タスクのアクティブ化のハンドラーが必要です。 [設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルでは、`PrintBackgroundTask`クラスは、印刷の通知を処理します。

**注**  場合は、プリンターの状態が直接ユーザーの介入を必要としない、タイルの更新ではなく、トーストを表示します。 たとえば、低のインクの条件では、タイルの更新で十分です。 ただし、プリンターが完全にインクが不足の場合、アプリでトースト通知を表示可能性があります。

 

### <a name="span-idsavingnotificationdetailsspanspan-idsavingnotificationdetailsspanspan-idsavingnotificationdetailsspansaving-notification-details"></a><span id="Saving_notification_details"></span><span id="saving_notification_details"></span><span id="SAVING_NOTIFICATION_DETAILS"></span>通知の詳細を保存しています

バック グラウンド タスクでは、フォア グラウンド アプリを直接起動することはできません、ユーザーのみができます: から、タイル、トースト、または開始します。 これを確実に印刷通知の詳細をフォア グラウンド アプリがアクセスできること、バック グラウンド タスクは、それらをローカル ストレージに保存します。 ローカル ストレージの使用方法の詳細については、[クイック スタート: アプリのローカル データ](https://go.microsoft.com/fwlink/p/?LinkId=317216)を参照してください。

Windows が呼び出すことによって、バック グラウンド タスクを実行する印刷通知がトリガーされたときにその`Run`メソッド。 通知のデータは、バック グラウンド タスクに Windows.Devices.Printers.Extensions.PrintNotificationEventDetails を型にキャストする必要がありますメソッド パラメーターで渡されます。 `PrinterName`と`EventData`そのオブジェクトのプロパティは、プリンター名と双方向のメッセージをそれぞれ実行します。

この例は、バック グラウンド タスクの`Run`メソッドで、 **PrintBackgroundTask.cs**ファイル、印刷通知の詳細は、トーストの前に、アプリ設定に保存されますが、タイルとバッジのメソッドと呼ばれます。

```CSharp
public void Run(Windows.ApplicationModel.Background.IBackgroundTaskInstance taskInstance)
{
    // Save notification details to local storage
    PrintNotificationEventDetails details = (PrintNotificationEventDetails)taskInstance.TriggerDetails;
    settings.Values[keyPrinterName] = details.PrinterName;
    settings.Values[keyAsyncUIXML] = details.EventData;
    
    // Demonstrate possible actions
    ShowToast(details.PrinterName, details.EventData);
    UpdateTile(details.PrinterName, details.EventData);
    UpdateBadge();
}
```

### <a name="span-idupdatingatilespanspan-idupdatingatilespanspan-idupdatingatilespanupdating-a-tile"></a><span id="Updating_a_tile"></span><span id="updating_a_tile"></span><span id="UPDATING_A_TILE"></span>タイルの更新

印刷通知の詳細に送信されると、`UpdateTile`メソッド、サンプルのバック グラウンド タスクは、タイルに表示する方法を示します。 タイルの詳細については、[タイルとタイル通知の概要](https://go.microsoft.com/fwlink/p/?LinkId=317195)を参照してください。

この例は、バック グラウンド タスクの`UpdateTile`メソッドで、 **PrintBackgroundTask.cs**ファイル。
```CSharp
void UpdateTile(string printerName, string bidiMessage)
{
    TileUpdater tileUpdater = TileUpdateManager.CreateTileUpdaterForApplication();
    tileUpdater.Clear();

    XmlDocument tileXml = TileUpdateManager.GetTemplateContent(TileTemplateType.TileWide310x150Text09);
    XmlNodeList tileTextAttributes = tileXml.GetElementsByTagName("text");
    tileTextAttributes[0].InnerText = printerName;
    tileTextAttributes[1].InnerText = bidiMessage;

    TileNotification tileNotification = new TileNotification(tileXml);
    tileNotification.Tag = "tag01";
    tileUpdater.Update(tileNotification);
}
```

### <a name="span-idupdatingabadgespanspan-idupdatingabadgespanspan-idupdatingabadgespanupdating-a-badge"></a><span id="Updating_a_badge"></span><span id="updating_a_badge"></span><span id="UPDATING_A_BADGE"></span>バッジの更新

`UpdateBadge`メソッド BadgeNotification クラスを使用して、バッジを更新する方法を示しています。 タイルの詳細については、[バッジの概要](https://go.microsoft.com/fwlink/p/?LinkId=317196)を参照してください。

この例は、バック グラウンド タスクの`UpdateBadge`メソッドで、 **PrintBackgroundTask.cs**ファイル。

```CSharp
void UpdateBadge()
{
    XmlDocument badgeXml = BadgeUpdateManager.GetTemplateContent(BadgeTemplateType.BadgeGlyph);
    XmlElement badgeElement = (XmlElement)badgeXml.SelectSingleNode("/badge");
    badgeElement.SetAttribute("value", "error");

    var badgeNotification = new BadgeNotification(badgeXml);
    BadgeUpdateManager.CreateBadgeUpdaterForApplication().Update(badgeNotification);
}
```

### <a name="span-idraisingatoastspanspan-idraisingatoastspanspan-idraisingatoastspanraising-a-toast"></a><span id="Raising_a_toast"></span><span id="raising_a_toast"></span><span id="RAISING_A_TOAST"></span>トーストを発生させる

トースト通知は、関連する、時間を区別する情報を格納し、アプリに関連するコンテンツにすばやくアクセスできることをユーザーに一時的なメッセージです。 トースト通知は、徹底的に関心のある何か、アプリに戻るための招待としてユーザーに表示する必要があります。 詳細については、[トースト通知の概要](https://go.microsoft.com/fwlink/p/?LinkId=317197)を参照してください。

トースト通知を有効にするには、アプリを登録するトースト対応のアプリのパッケージ マニフェストである必要があります。 `VisualElements`要素、設定、`ToastCapable`属性を true にします。

**重要な**  常に、トースト、特にの非実用的なイベントを示す勧めされません。 ユーザーの面倒になるし、アプリからのすべてのトースト通知をオフにすることがありますこの可能性があります。 ユーザーの早急な措置を必要としないイベントの場合、タイルとバッジの更新およびトーストが表示されていないお勧めします。

 

この例では、`ToastCapable`属性、`VisualElements`アプリ パッケージのマニフェスト ファイルに要素が表示されます**Package.appxmanifest**します。

```XML
<VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" 
                SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" 
                ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
  <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
  <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
</VisualElements>
```

この例は、`ShowToast`のメソッド、 **PrintBackgroundTask.cs**ファイル。 という名前の 2 つの文字列に基づくトーストを発生させる方法を示します`title`と`body`します。
```CSharp
void ShowToast(string title, string body)
{
    //
    // Get Toast template
    //
    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(ToastTemplateType.ToastText02);

    //
    // Pass to app as eventArgs.detail.arguments
    //
    ((XmlElement)toastXml.SelectSingleNode("/toast")).SetAttribute("launch", title);

    //
    // The ToastText02 template has 2 text nodes (a header and a body)
    // Assign title to the first one, and body to the second one
    //
    XmlNodeList textList = toastXml.GetElementsByTagName("text");
    textList[0].AppendChild(toastXml.CreateTextNode(title));
    textList[1].AppendChild(toastXml.CreateTextNode(body));

    //
    // Show the Toast
    //
    ToastNotification toast = new ToastNotification(toastXml);
    ToastNotificationManager.CreateToastNotifier().Show(toast);
}
```

## <a name="span-idstep5handleactivationspanspan-idstep5handleactivationspanspan-idstep5handleactivationspanstep-5-handle-activation"></a><span id="Step_5__Handle_activation"></span><span id="step_5__handle_activation"></span><span id="STEP_5__HANDLE_ACTIVATION"></span>手順 5: アクティブ化の処理


印刷の通知には、バック グラウンド タスクがトリガーされた後は、トースト通知またはタイルをタップしてアプリを起動できます。 パラメーターを使用してアプリに渡されるいずれかから、アプリがアクティブになる場合`LaunchActivatedEventArgs.arguments`プロパティ。 ライセンス認証と Microsoft Store アプリのライフ サイクルについての詳細については、[アプリケーションのライフ サイクル](https://go.microsoft.com/fwlink/p/?LinkId=317387)を参照してください。

かどうかは、アプリがいずれかの場合、これらのアクティブ化を確認するのには、処理、`OnLaunched`イベント、イベント ハンドラーに渡されるイベント引数を確認します。 イベント引数が null の場合、アプリが最初からユーザーによって有効化されました。 イベント引数が null でない場合は、アプリがトーストまたはタイルから起動されました。

この例は、`OnLaunched`のメソッド、 **App.xaml.cs**ファイル。 トースト、タイルからアクティブ化を処理する方法を示します。
```CSharp
protected override async void OnLaunched(LaunchActivatedEventArgs args)
{
    Frame rootFrame = Window.Current.Content as Frame;

    // Do not repeat app initialization when the Window already has content,
    // just ensure that the window is active
    
    if (rootFrame == null)
    {
        // Create a Frame to act as the navigation context and navigate to the first page
        rootFrame = new Frame();
        // Associate the frame with a SuspensionManager key                                
        SuspensionManager.RegisterFrame(rootFrame, "AppFrame");

        if (args.PreviousExecutionState == ApplicationExecutionState.Terminated)
        {
            // Restore the saved session state only when appropriate
            try
            {
                await SuspensionManager.RestoreAsync();
            }
            catch (SuspensionManagerException)
            {
                //Something went wrong restoring state.
                //Assume there is no state and continue
            }
        }

        // Place the frame in the current Window
        Window.Current.Content = rootFrame;
    }
    if (rootFrame.Content == null || !String.IsNullOrEmpty(args.Arguments))
    {
        // When the navigation stack isn't restored or there are launch arguments
        // indicating an alternate launch (e.g.: via toast or secondary tile), 
        // navigate to the appropriate page, configuring the new page by passing required 
        // information as a navigation parameter
        if (!rootFrame.Navigate(typeof(MainPage), args.Arguments))
        {
            throw new Exception("Failed to create initial page");
        }
    }
    // Ensure the current window is active
    Window.Current.Activate();
}
```

## <a name="span-idstep6accessnotificationdetailsspanspan-idstep6accessnotificationdetailsspanspan-idstep6accessnotificationdetailsspanstep-6-access-notification-details"></a><span id="Step_6__Access_notification_details"></span><span id="step_6__access_notification_details"></span><span id="STEP_6__ACCESS_NOTIFICATION_DETAILS"></span>手順 6: アクセス通知の詳細


バック グラウンド タスクは、フォア グラウンド アプリを直接起動ことはできません、ために、印刷通知の詳細は、フォア グラウンド アプリがアクセスできるように、アプリの設定に保存する必要があります。 ローカル ストレージの使用方法の詳細については、[クイック スタート: アプリのローカル データ](https://go.microsoft.com/fwlink/p/?LinkId=317216)を参照してください。

この例では、プリンター名と双方向のメッセージがから取得する方法でアプリの設定では、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル。 コードは、`DisplayBackgroundTaskTriggerDetails`のメソッド、 **InkLevel.xaml.cs**ファイル。 なおキー インデックスの値`keyPrinterName`と`keyAsyncUIXML`、バック グラウンド タスクで使用される同じ文字列の定数**PrintBackgroundTask.cs**します。
```CSharp
void DisplayBackgroundTaskTriggerDetails()
{
    String outputText = "\r\n";

    try
    {
        string printerName = settings.Values[keyPrinterName].ToString();
        outputText += ("Printer name from background task triggerDetails: " + printerName);
    }
    catch (Exception)
    {
        outputText += ("No printer name retrieved from background task triggerDetails ");
    }

    outputText += "\r\n";
    try
    {
        string asyncUIXML = settings.Values[keyAsyncUIXML].ToString();
        outputText += ("AsyncUI xml from background task triggerDetails: " + asyncUIXML);
    }
    catch (Exception)
    {
        outputText += ("No asyncUI xml retrieved from background task triggerDetails ");
    }

    ToastOutput.Text += outputText;
}
```

## <a name="span-idtestingspanspan-idtestingspantesting"></a><span id="testing"></span><span id="TESTING"></span>テスト


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
5.  編集し、デバイスのメタデータを保存します。 デバイス アプリをデバイスにリンクするには、デバイスでデバイス アプリを関連付ける必要があります。
    **注**  デバイスのメタデータをまだ作成していない場合は、[UWP デバイス アプリのデバイス メタデータを作成する](https://go.microsoft.com/fwlink/p/?LinkId=313644)を参照してください。

     

    1.  場合、**デバイス メタデータの作成ウィザード**が開くまだ、開始から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\x86 により、ダブルクリック**DeviceMetadataWizard.exe**します。
    2.  クリックして**デバイス メタデータの編集**します。 これからは、既存のデバイス メタデータ パッケージを編集できます。
    3.  **オープン** ダイアログ ボックスで、UWP デバイス アプリに関連付けられている、デバイス メタデータ パッケージを見つけます。 (これが、 **devicemetadata ms**ファイル拡張子)。
    4.  **指定 UWP デバイスのアプリ情報** ページで、Microsoft Store アプリの情報を入力、 **UWP デバイス アプリ**ボックス。 をクリックして**インポート UWP アプリのマニフェスト ファイル**自動的に入力する、**パッケージ名**、**パブリッシャー名**と**UWP アプリの ID**します。
    5.  場合は、アプリは、プリンターの通知の登録は、入力、**通知ハンドラー**ボックス。 **イベント ID**、印刷イベント ハンドラーの名前を入力します。 **イベント資産**、そのコードが存在するファイルの名前を入力します。

    6.  完了したら、クリックして **[次へ]** に到達するまで、**完了**ページ。
    7.  **デバイス メタデータ パッケージの確認** ページで、すべての設定が正しいことと選択するかどうかを確認、**デバイス メタデータ パッケージをローカル コンピューター上のメタデータ ストアにコピー**チェック ボックスをオンします。 クリックして**保存**します。

6.  デバイスが接続されている場合、その Windows が更新されたデバイスのメタデータを読み取り、プリンターに再接続します。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>トラブルシューティング


### <a name="span-idissuenodefaulttoastnotificationappearsspanspan-idissuenodefaulttoastnotificationappearsspanspan-idissuenodefaulttoastnotificationappearsspanissue-no-default-toast-notification-appears"></a><span id="Issue__No_default_toast_notification_appears"></span><span id="issue__no_default_toast_notification_appears"></span><span id="ISSUE__NO_DEFAULT_TOAST_NOTIFICATION_APPEARS"></span>問題:既定のトースト通知は表示されません。

既定の通知印刷しない場合は、予想される場合に表示されます.

-   **考えられる原因:** テスト署名が有効になっていません。 有効にする方法については、このトピックでは、"デバッグ"を参照してください。

-   **考えられる原因:** ドメイン ポリシーには、トースト通知が無効にします。 ドメインのままにし、もう一度やり直してください。

-   **考えられる原因:** プリンターは DriverEvents を実装していません。 Bidi と DriverEvents v4 ドライバーをサポートしていることを確認します。 詳細については、[UI のカスタマイズのドライバー サポート](https://msdn.microsoft.com/library/windows/hardware/jj659898)を参照してください。

-   **考えられる原因:** コンピューターには、プリンター キュー内の最近のジョブがありません。 プリンターのアイコンが画面の右下隅に表示されることを確認します。 ない場合は、別の印刷ジョブを送信します。

-   **考えられる原因:** バック グラウンド タスクのエントリ ポイント (`IBackgroundTask`) は、フォア グラウンド アプリと同じプロジェクト内です。 これは許可されていません。 バック グラウンド タスク ハンドラーのまったく新しいクラスを独立しました。

-   **考えられる原因:** アプリで通知のエントリ ポイントであるクラスが正しくのマニフェストまたはデバイスのメタデータを原因で、アプリのクラッシュ、backgroundhost 内と任意のトーストが表示されていないで与えられます。 次の点を確認します。

    -   エントリ ポイントが正しく指定されたかどうかを確認、**宣言**マニフェスト デザイナーのタブ。 Namespace.ClassName の形式でなければなりませんC#および C++ です。 の JavaScript 用の .js ファイルの相対ディレクトリ パスが必要です。
    -   終了したら、JavaScript アプリは close() を呼び出す必要があります。
    -   C#クラス Windows.ApplicationModel.Background.IBackgroundTask を実装する必要があり、されているので、public void`Run(Windows.ApplicationModel.Background.IBackgroundTaskInstance taskInstance)`メソッド。
    -   あり Windows::ApplicationModel::Background::IBackgroundTask を実装する C++ クラスを`virtual void Run(Windows::ApplicationModel::Background::IBackgroundTaskInstance^ taskInstance) `メソッド。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[バッジの概要 (UWP アプリ)](https://go.microsoft.com/fwlink/p/?LinkId=317196)

[タイルし、タイル通知の概要 (UWP アプリ)](https://go.microsoft.com/fwlink/p/?LinkId=317195)

[タイルとバッジ (UWP アプリ) のガイドラインとチェックリスト](https://go.microsoft.com/fwlink/p/?LinkId=317194)

[トースト通知の概要 (UWP アプリ)](https://go.microsoft.com/fwlink/p/?LinkId=317197)

[トースト通知 (UWP アプリ) のガイドラインとチェックリスト](https://go.microsoft.com/fwlink/p/?LinkId=317193)

[カスタマイズした UI のドライバー サポート](https://msdn.microsoft.com/library/windows/hardware/jj659898)

[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[プリンター拡張機能インターフェイス (v4 印刷ドライバー)](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[アプリを作成する UWP デバイス (ステップ バイ ステップ ガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスのアプリ (ステップ バイ ステップ ガイド) のデバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 






