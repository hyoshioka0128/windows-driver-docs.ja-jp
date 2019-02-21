---
title: UWP アプリのデバイスのプリンターのメンテナンスを実行する方法
description: Windows 8.1 では、UWP デバイス アプリは印刷ヘッドのアラインメントとノズルをクリーニングなどのプリンターのメンテナンスを実行できます。
ms.assetid: 52141F66-872A-4381-92C8-B04ABDABA7AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33357edbdf1213c5fc4e18e046d7922326c4b4aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558628"
---
# <a name="how-to-do-printer-maintenance-in-a-uwp-device-app"></a>UWP アプリのデバイスのプリンターのメンテナンスを実行する方法


Windows 8.1 では、UWP デバイス アプリは印刷ヘッドのアラインメントとノズルをクリーニングなどのプリンターのメンテナンスを実行できます。 このトピックでは、C#のバージョン、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)双方向通信 (Bidi) を使用して、このようなデバイスのメンテナンスを実行する方法を示すサンプル。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

C#のバージョン、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルではプリンターでのメンテナンス、 **DeviceMaintenance.xaml.cs**ファイル、 **DeviceAppForPrinters2**プロジェクト。 サンプルを Bidi を使用するでプリンターの拡張機能ライブラリを使用して、 **PrinterExtensionLibrary**プロジェクト。 プリンターの拡張機能ライブラリでは、v4 印刷ドライバーのプリンター拡張機能のインターフェイスにアクセスする便利な手段を提供します。 詳細については、次を参照してください。、[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)します。

**注**  このトピックで示すコード例に基づいています、C#のバージョン、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプル。 このサンプルも JavaScript および C++ で使用できます。 C++ は COM を直接アクセスできるため、C++ のバージョン サンプルにはが含まれていないことコード ライブラリ プロジェクトに注意してください。 コードの最新バージョンを参照するサンプルをダウンロードします。

 

## <a name="span-idprintermaintenancespanspan-idprintermaintenancespanspan-idprintermaintenancespanprinter-maintenance"></a><span id="Printer_maintenance"></span><span id="printer_maintenance"></span><span id="PRINTER_MAINTENANCE"></span>プリンターのメンテナンス


Windows 8.1 には、新しいデバイスのメンテナンスを実装するために使用できる、v4 プリンター ドライバーでのプリンター拡張機能のインターフェイスが導入されています。[**IPrinterBidiSetRequestCallback**](https://msdn.microsoft.com/library/windows/hardware/dn265385)、 [ **IPrinterExtensionAsyncOperation** ](https://msdn.microsoft.com/library/windows/hardware/dn265387) 、および[ **IPrinterQueue2** ](https://msdn.microsoft.com/library/windows/hardware/dn265389). これらのインターフェイスを使用すれば、デバイスとプロトコルに固有のコマンドに変換してから、プリンターに送信できるように、ポート モニターを双方向の要求を非同期的に送信できます。 詳細については、次を参照してください。[デバイスのメンテナンス (v4 プリンター ドライバー)](https://msdn.microsoft.com/library/windows/hardware/dn265274)します。

**ヒント:**    C# JavaScript アプリは COM Api と直接動作できません。 作成する場合、C#または JavaScript UWP デバイス アプリ、プリンターの拡張機能ライブラリを使用して、これらのインターフェイス (このトピックで示す) にアクセスします。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


開始する前に。

1.  V4 印刷ドライバーを使用して、プリンターをインストールすることを確認します。 詳細については、次を参照してください。[開発 v4 印刷ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=314231)します。
2.  開発用 PC の設定を取得します。 参照してください[Getting started](getting-started.md)については、ツールをダウンロードして開発者アカウントを作成します。
3.  アプリをストアに関連付けます。 参照してください[UWP デバイスのアプリを作成](step-1--create-a-uwp-device-app.md)についてです。
4.  アプリに関連付けているプリンター用のデバイス メタデータを作成します。 参照してください[デバイス メタデータを作成する](step-2--create-device-metadata.md)の詳細についてはします。
5.  アプリのメイン ページの UI をビルドします。 表示されている全画面表示になりますが、最初からすべての UWP デバイス アプリを起動できます。 スタート エクスペリエンスを使用して、製品またはサービスに固有のブランドと一致する方法と、デバイスの機能を強調表示します。 使用できる UI コントロールの種類の特別な制限はありません。 全画面表示エクスペリエンスのデザインを開始するを参照してください。、 [Microsoft Store の設計原則](https://go.microsoft.com/fwlink/p/?LinkID=299845)します。
6.  使用してアプリを作成している記述しているかどうかはC#または JavaScript を追加、 **PrinterExtensionLibrary** UWP デバイスのアプリ ソリューションにプロジェクト。 このプロジェクトを見つけることができます、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプル。
    **注**  のための C++ COM に直接アクセスできる、C アプリの場合は、COM ベースのプリンター デバイス コンテキストを使用する別のライブラリを必要としません。

     

## <a name="span-idstep1preparebidirequestspanspan-idstep1preparebidirequestspanspan-idstep1preparebidirequestspanstep-1-prepare-bidi-request"></a><span id="Step_1__Prepare_Bidi_request"></span><span id="step_1__prepare_bidi_request"></span><span id="STEP_1__PREPARE_BIDI_REQUEST"></span>手順 1:双方向の要求を準備します。


デバイスのメンテナンス インターフェイスは、双方向の要求は、文字列の形式で XML データである必要があります。 アプリで意味がある場所では、双方向の要求を構築できます。 たとえば、文字列定数として、双方向の要求を保存したり、ユーザー入力に基づいて動的に作成します。 [印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルの動作の既定の要求を構築する`OnNavigatedTo`メソッド。 双方向に関する詳細については、次を参照してください。[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)します。

この例は、`OnNavigatedTo`のメソッド、 **DeviceMaintenance.xaml.cs**ファイル。

```CSharp
string defaultBidiQuery =
    "<bidi:Set xmlns:bidi=\"http://schemas.microsoft.com/windows/2005/03/printing/bidi\">\r\n" +
    "    <Query schema=&#39;\\Printer.Maintenance:CleanHead&#39;>\r\n" +
    "        <BIDI_BOOL>false</BIDI_BOOL>\r\n" +
    "    </Query>\r\n" +
    "</bidi:Set>";
```

## <a name="span-idstep2findprinterspanspan-idstep2findprinterspanspan-idstep2findprinterspanstep-2-find-printer"></a><span id="Step_2__Find_printer"></span><span id="step_2__find_printer"></span><span id="STEP_2__FIND_PRINTER"></span>手順 2:プリンターを検索します。


アプリは、プリンターにコマンドを送信できる、これには、まず、プリンターを探します。 これを行う、[印刷ジョブの管理やプリンターの管理](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルには、という名前の便利なクラスが含まれています。 `PrinterEnumeration` (で、 **PrinterEnumeration.cs**ファイル)。 このクラスは、デバイスのメタデータを使用して、アプリに関連付けられているすべてのプリンターを検索しの一覧を返します`PrinterInfo`オブジェクトで、名前と各プリンターについては、デバイス Id が含まれています。

この例は、`EnumeratePrinters_Click`のメソッド、 **DeviceMaintenance.xaml.cs**ファイル。 サンプルを使用する方法を示しています、`PrinterEnumeration`クラスの一覧を取得するには、プリンターが関連付けられています。

```CSharp
private async void EnumeratePrinters_Click(object sender, RoutedEventArgs e)
{
    try
    {
        rootPage.NotifyUser("Enumerating printers. Please wait", NotifyType.StatusMessage);

        // Retrieve the running app&#39;s package family name, and enumerate associated printers.
        string currentPackageFamilyName = Windows.ApplicationModel.Package.Current.Id.FamilyName;

        // Enumerate associated printers.
        PrinterEnumeration pe = new PrinterEnumeration(currentPackageFamilyName);
        List<PrinterInfo> associatedPrinters = await pe.EnumeratePrintersAsync();

        // Update the data binding source on the combo box that displays the list of printers.
        PrinterComboBox.ItemsSource = associatedPrinters;
        if (associatedPrinters.Count > 0)
        {
            PrinterComboBox.SelectedIndex = 0;
            rootPage.NotifyUser(associatedPrinters.Count + " printers enumerated", NotifyType.StatusMessage);
        }
        else
        {
            rootPage.NotifyUser(DisplayStrings.NoPrintersEnumerated, NotifyType.ErrorMessage);
        }
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

**ヒント:**  の詳細については、`PrinterEnumeration`と`PrinterInfo`クラスを参照してください、 **PrinterEnumeration.cs**ファイル。

 

## <a name="span-idstep3sendbidirequestspanspan-idstep3sendbidirequestspanspan-idstep3sendbidirequestspanstep-3-send-bidi-request"></a><span id="Step_3__Send_Bidi_request"></span><span id="step_3__send_bidi_request"></span><span id="STEP_3__SEND_BIDI_REQUEST"></span>手順 3:双方向の要求を送信します。


Bidi 文字列およびコールバックを双方向の要求を送信するには、デバイスのメンテナンス インターフェイスが必要です。 `SendBidiRequest_Click`メソッド、サンプルの最初では、`PrinterInfo`という名前のプリンター拡張コンテキスト オブジェクトを作成するオブジェクト`context`します。 `PrinterBidiSetRequestCallback`オブジェクトが作成され、コールバックを処理するイベント ハンドラーを追加`OnBidiResponseReceived`イベント。 最後に、プリンター拡張コンテキストの`SendBidiSetRequestAsync`双方向の文字列とコールバックを送信するメソッドを使用します。

この例は、`SendBidiRequest_Click`のメソッド、 **DeviceMaintenance.xaml.cs**ファイル。

```CSharp
private void SendBidiRequest_Click(object sender, RoutedEventArgs e)
{
    try
    {
        PrinterInfo queue = (PrinterInfo)PrinterComboBox.SelectedItem;

        // Retrieve a COM IPrinterExtensionContext object, using the static WinRT factory.
        // Then instantiate one "PrinterExtensionContext" object that allows operations on the COM object.
        Object comComtext = Windows.Devices.Printers.Extensions.PrintExtensionContext.FromDeviceId(queue.DeviceId);
        PrinterExtensionContext context = new PrinterExtensionContext(comComtext);

        // Create an instance of the callback object, and perform an asynchronous &#39;bidi set&#39; operation.
        PrinterBidiSetRequestCallback callback = new PrinterBidiSetRequestCallback();

        // Add an event handler to the callback object&#39;s OnBidiResponseReceived event.
        // The event handler will be invoked once the Bidi response is received.
        callback.OnBidiResponseReceived += OnBidiResponseReceived;

        // Send the Bidi "Set" query asynchronously.
        IPrinterExtensionAsyncOperation operationContext
            = context.Queue.SendBidiSetRequestAsync(BidiQueryInput.Text, callback);

        // Note: The &#39;operationContext&#39; object can be used to cancel the operation if required.
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

## <a name="span-idstep4receivebidiresponsespanspan-idstep4receivebidiresponsespanspan-idstep4receivebidiresponsespanstep-4-receive-bidi-response"></a><span id="Step_4__Receive_Bidi_response"></span><span id="step_4__receive_bidi_response"></span><span id="STEP_4__RECEIVE_BIDI_RESPONSE"></span>手順 4:双方向の応答を受信します。


双方向「設定」操作が完了すると、コールバック オブジェクトの型の`PrinterBidiSetRequestCallback`が呼び出されます。 このコールバック エラー HRESULT 応答から処理を行います、し、トリガー、`OnBidiResponseReceived`イベント、イベント パラメーターを介して Bidi 応答を送信します。

この例では、`PrinterBidiSetRequestCallback`クラスの定義、 **DeviceMaintenance.xaml.cs**ファイル。

```CSharp
internal class PrinterBidiSetRequestCallback : IPrinterBidiSetRequestCallback
{
    /// <summary>
    /// This method is invoked when the asynchronous Bidi "Set" operation is completed.
    /// </summary>
    public void Completed(string response, int statusHResult)
    {
        string result;

        if (statusHResult == (int)HRESULT.S_OK)
        {
            result = "The response is \r\n" + response;
        }
        else
        {
            result = "The HRESULT received is: 0x" + statusHResult.ToString("X") + "\r\n" +
                     "No Bidi response was received";
        }

        // Invoke the event handlers when the Bidi response is received.
        OnBidiResponseReceived(null, result);
    }

    /// <summary>
    /// This event will be invoked when the Bidi &#39;set&#39; response is received.
    /// </summary>
    public event EventHandler<string> OnBidiResponseReceived;
}
```

Bidi 応答に送信し、`OnBidiResponseReceived`メソッド、場所、 `Dispatcher` UI スレッドに結果を表示するために使用します。

この例は、`OnBidiResponseReceived`のメソッド、 **DeviceMaintenance.xaml.cs**ファイル。

```CSharp
internal async void OnBidiResponseReceived(object sender, string bidiResponse)
{
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        BidiResponseOutput.Text = bidiResponse;
    });
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
    **注**  デバイスのメタデータをまだ作成していない場合は、次を参照してください。 [UWP デバイス アプリのデバイス メタデータを作成する](https://go.microsoft.com/fwlink/p/?LinkId=313644)します。

     

    1.  場合、**デバイス メタデータの作成ウィザード**が開くまだ、開始から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\x86 により、ダブルクリック**DeviceMetadataWizard.exe**します。
    2.  クリックして**デバイス メタデータの編集**します。 これからは、既存のデバイス メタデータ パッケージを編集できます。
    3.  **オープン** ダイアログ ボックスで、UWP デバイス アプリに関連付けられている、デバイス メタデータ パッケージを見つけます。 (これが、 **devicemetadata ms**ファイル拡張子)。
    4.  **指定 UWP デバイスのアプリ情報** ページで、Microsoft Store アプリの情報を入力、 **UWP デバイス アプリ**ボックス。 をクリックして**インポート UWP アプリのマニフェスト ファイル**自動的に入力する、**パッケージ名**、**パブリッシャー名**と**UWP アプリの ID**します。
    5.  場合は、アプリは、プリンターの通知の登録は、入力、**通知ハンドラー**ボックス。 **イベント ID**、印刷イベント ハンドラーの名前を入力します。 **イベント資産**、そのコードが存在するファイルの名前を入力します。

    6.  完了したら、クリックして **[次へ]** に到達するまで、**完了**ページ。
    7.  **デバイス メタデータ パッケージの確認** ページで、すべての設定が正しいことと選択するかどうかを確認、**デバイス メタデータ パッケージをローカル コンピューター上のメタデータ ストアにコピー**チェック ボックスをオンします。 クリックして**保存**します。

6.  デバイスが接続されている場合、その Windows が更新されたデバイスのメタデータを読み取り、プリンターに再接続します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイスのメンテナンス (v4 プリンター ドライバー)](https://msdn.microsoft.com/library/windows/hardware/dn265274)

[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[アプリを作成する UWP デバイス (ステップ バイ ステップ ガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスのアプリ (ステップ バイ ステップ ガイド) のデバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 






