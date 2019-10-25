---
title: UWP デバイスアプリでプリンターのメンテナンスを行う方法
description: Windows 8.1 では、UWP デバイスアプリは、印刷ヘッドの調整やノズルのクリーニングなど、プリンターのメンテナンスを実行できます。
ms.assetid: 52141F66-872A-4381-92C8-B04ABDABA7AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a79ebb2a368cdefde97493870bd8e8ed6328aa96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829906"
---
# <a name="how-to-do-printer-maintenance-in-a-uwp-device-app"></a>UWP デバイスアプリでプリンターのメンテナンスを行う方法


Windows 8.1 では、UWP デバイスアプリは、印刷ヘッドの調整やノズルのクリーニングなど、プリンターのメンテナンスを実行できます。 このトピックではC# 、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルのバージョンを使用して、双方向通信 (Bidi) を使用してこのようなデバイスのメンテナンスを実行する方法を示します。 UWP デバイスアプリ全般の詳細については、 [uwp デバイスアプリの準拠](meet-uwp-device-apps.md)に関するページを参照してください。

C# [印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルのバージョンは、 **DeviceAppForPrinters2**プロジェクトの**DeviceMaintenance.xaml.cs**ファイルを使用したプリンターのメンテナンスを示しています。 このサンプルでは、Bidi を操作するために、**プリンターの拡張**機能ライブラリを使用します。 プリンター拡張ライブラリは、v4 印刷ドライバーのプリンター拡張機能インターフェイスにアクセスするための便利な方法を提供します。 詳細については、「[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)」を参照してください。

このトピックに示されているコード例は、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルのC#バージョンに基づい**て  ます**。 このサンプルは、JavaScript およびC++でも使用できます。 は COM にC++直接アクセスできるため、サンプルC++のバージョンにはコードライブラリプロジェクトが含まれていないことに注意してください。 サンプルをダウンロードして、最新バージョンのコードを確認してください。

 

## <a name="span-idprinter_maintenancespanspan-idprinter_maintenancespanspan-idprinter_maintenancespanprinter-maintenance"></a><span id="Printer_maintenance"></span><span id="printer_maintenance"></span><span id="PRINTER_MAINTENANCE"></span>プリンターのメンテナンス


Windows 8.1 では、デバイスのメンテナンスを実装するために使用できる、v4 プリンタードライバーに新しいプリンター拡張インターフェイスが導入されています。 [**Iprinter Bidisetrequestcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterbidisetrequestcallback)、 [**IPrinterExtensionAsyncOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensionasyncoperation) 、および[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)。 これらのインターフェイスを使用すると、ポートモニターに対して非同期的に Bidi 要求を送信して、デバイスやプロトコルに固有のコマンドに変換してから、プリンターに送信することができます。 詳細については、「[デバイスのメンテナンス (V4 プリンタードライバー)](https://docs.microsoft.com/windows-hardware/drivers/print/device-maintenance)」を参照してください。

**ヒント**  C#と JavaScript アプリが COM api を直接操作することはできません。 C#または JAVASCRIPT の UWP デバイスアプリを作成する場合は、このトピックに示すように、プリンター拡張ライブラリを使用してこれらのインターフェイスにアクセスします。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


作業を開始する前に:

1.  プリンターが v4 印刷ドライバーを使用してインストールされていることを確認します。 詳細については、「 [v4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)」を参照してください。
2.  開発用 PC のセットアップを開始します。 ツールのダウンロードと開発者アカウントの作成に関する情報については、「[作業の開始](getting-started.md)」を参照してください。
3.  アプリをストアに関連付けます。 詳細については[、「UWP デバイスアプリの作成](step-1--create-a-uwp-device-app.md)」を参照してください。
4.  アプリに関連付けられているプリンターのデバイスメタデータを作成します。 詳細については、「[デバイスメタデータの作成](step-2--create-device-metadata.md)」を参照してください。
5.  アプリのメインページの UI を作成します。 すべての UWP デバイスアプリはスタート画面から起動でき、全画面表示されます。 スタート画面を使用して、お使いのデバイスのブランドと機能に合わせて製品やサービスを強調表示します。 使用できる UI コントロールの種類に特別な制限はありません。 全画面表示のエクスペリエンスのデザインを開始するには、 [Microsoft Store 設計の原則](https://go.microsoft.com/fwlink/p/?LinkID=299845)に関するページを参照してください。
6.  または JavaScript を使用C#してアプリを作成する場合は、UWP デバイスアプリソリューションに**プリンター extensionlibrary**プロジェクトを追加します。 このプロジェクトは、[印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルで見つけることができます。
    は、がC++ com に直接アクセスできるC++ため、アプリケーションは com ベースのプリンターデバイスコンテキストを操作するために個別のライブラリを必要としないため、  に**注意**してください。

     

## <a name="span-idstep_1__prepare_bidi_requestspanspan-idstep_1__prepare_bidi_requestspanspan-idstep_1__prepare_bidi_requestspanstep-1-prepare-bidi-request"></a><span id="Step_1__Prepare_Bidi_request"></span><span id="step_1__prepare_bidi_request"></span><span id="STEP_1__PREPARE_BIDI_REQUEST"></span>手順 1: Bidi 要求を準備する


デバイスメンテナンスインターフェイスでは、Bidi 要求が文字列形式の XML データである必要があります。 アプリケーションでは、任意の場所で Bidi 要求を構築できます。 たとえば、Bidi 要求を文字列定数として保存したり、ユーザー入力に基づいて動的に作成したりすることができます。 [印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルは、`OnNavigatedTo` メソッドで既定の要求を構築するために発生します。 Bidi の詳細については、「[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)」を参照してください。

この例は、 **DeviceMaintenance.xaml.cs**ファイルの `OnNavigatedTo` メソッドからのものです。

```CSharp
string defaultBidiQuery =
    "<bidi:Set xmlns:bidi=\"http://schemas.microsoft.com/windows/2005/03/printing/bidi\">\r\n" +
    "    <Query schema='\\Printer.Maintenance:CleanHead'>\r\n" +
    "        <BIDI_BOOL>false</BIDI_BOOL>\r\n" +
    "    </Query>\r\n" +
    "</bidi:Set>";
```

## <a name="span-idstep_2__find_printerspanspan-idstep_2__find_printerspanspan-idstep_2__find_printerspanstep-2-find-printer"></a><span id="Step_2__Find_printer"></span><span id="step_2__find_printer"></span><span id="STEP_2__FIND_PRINTER"></span>手順 2: プリンターを検索する


アプリがプリンターにコマンドを送信する前に、まずプリンターを検索する必要があります。 これを行うために、[印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルには、( **PrinterEnumeration.cs**ファイルに) `PrinterEnumeration` という便利なクラスが含まれています。 このクラスは、デバイスメタデータを使用してアプリに関連付けられているすべてのプリンターを検索し、各プリンターの名前とデバイス Id を含む `PrinterInfo` オブジェクトの一覧を返します。

この例は、 **DeviceMaintenance.xaml.cs**ファイルの `EnumeratePrinters_Click` メソッドからのものです。 このサンプルでは、`PrinterEnumeration` クラスを使用して、関連付けられているプリンターの一覧を取得する方法を示します。

```CSharp
private async void EnumeratePrinters_Click(object sender, RoutedEventArgs e)
{
    try
    {
        rootPage.NotifyUser("Enumerating printers. Please wait", NotifyType.StatusMessage);

        // Retrieve the running app's package family name, and enumerate associated printers.
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

**ヒント**  `PrinterEnumeration` と `PrinterInfo` クラスの詳細については、 **PrinterEnumeration.cs**ファイルを参照してください。

 

## <a name="span-idstep_3__send_bidi_requestspanspan-idstep_3__send_bidi_requestspanspan-idstep_3__send_bidi_requestspanstep-3-send-bidi-request"></a><span id="Step_3__Send_Bidi_request"></span><span id="step_3__send_bidi_request"></span><span id="STEP_3__SEND_BIDI_REQUEST"></span>手順 3: Bidi 要求を送信する


Bidi 要求を送信するには、デバイスメンテナンスインターフェイスに、Bidi 文字列とコールバックが必要です。 `SendBidiRequest_Click` メソッドでは、サンプルはまず `PrinterInfo` オブジェクトを使用して、`context`という名前のプリンター拡張コンテキストオブジェクトを作成します。 次に、`PrinterBidiSetRequestCallback` オブジェクトが作成され、コールバックの `OnBidiResponseReceived` イベントを処理するためのイベントハンドラーが追加されます。 最後に、プリンター拡張コンテキストの `SendBidiSetRequestAsync` メソッドを使用して、Bidi 文字列とコールバックを送信します。

この例は、 **DeviceMaintenance.xaml.cs**ファイルの `SendBidiRequest_Click` メソッドからのものです。

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

        // Create an instance of the callback object, and perform an asynchronous 'bidi set' operation.
        PrinterBidiSetRequestCallback callback = new PrinterBidiSetRequestCallback();

        // Add an event handler to the callback object's OnBidiResponseReceived event.
        // The event handler will be invoked once the Bidi response is received.
        callback.OnBidiResponseReceived += OnBidiResponseReceived;

        // Send the Bidi "Set" query asynchronously.
        IPrinterExtensionAsyncOperation operationContext
            = context.Queue.SendBidiSetRequestAsync(BidiQueryInput.Text, callback);

        // Note: The 'operationContext' object can be used to cancel the operation if required.
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

## <a name="span-idstep_4__receive_bidi_responsespanspan-idstep_4__receive_bidi_responsespanspan-idstep_4__receive_bidi_responsespanstep-4-receive-bidi-response"></a><span id="Step_4__Receive_Bidi_response"></span><span id="step_4__receive_bidi_response"></span><span id="STEP_4__RECEIVE_BIDI_RESPONSE"></span>手順 4: Bidi 応答を受信する


Bidi の "set" 操作が完了すると、`PrinterBidiSetRequestCallback`型のコールバックオブジェクトが呼び出されます。 このコールバックは、HRESULT 応答からのエラー処理を処理し、イベントパラメーターを使用して Bidi 応答を送信して、`OnBidiResponseReceived` イベントをトリガーします。

この例は、 **DeviceMaintenance.xaml.cs**ファイル内の `PrinterBidiSetRequestCallback` クラス定義を示しています。

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
    /// This event will be invoked when the Bidi 'set' response is received.
    /// </summary>
    public event EventHandler<string> OnBidiResponseReceived;
}
```

次に、Bidi 応答を `OnBidiResponseReceived` メソッドに送信します。このメソッドは、`Dispatcher` を使用して UI スレッドの結果を表示します。

この例は、 **DeviceMaintenance.xaml.cs**ファイルの `OnBidiResponseReceived` メソッドからのものです。

```CSharp
internal async void OnBidiResponseReceived(object sender, string bidiResponse)
{
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        BidiResponseOutput.Text = bidiResponse;
    });
}
```

## <a name="span-idtestingspanspan-idtestingspantesting"></a><span id="testing"></span><span id="TESTING"></span>調べる


UWP デバイスアプリをテストするには、デバイスメタデータを使用してプリンターにリンクされている必要があります。

-   デバイスアプリ情報を追加するには、プリンターのデバイスメタデータパッケージのコピーが必要です。 デバイスメタデータを持っていない場合は、「 [UWP デバイスアプリのデバイスメタデータの作成](https://go.microsoft.com/fwlink/p/?LinkId=313644)」の説明に従って、**デバイスメタデータ作成ウィザード**を使用して作成できます。

    **注**  **デバイスメタデータ作成ウィザード**を使用するには、このトピックの手順を実行する前に、Windows 8.1 用の Microsoft Visual Studio Professional、Microsoft Visual Studio Ultimate、または[スタンドアロン SDK](https://go.microsoft.com/fwlink/p/?linkid=309209)をインストールする必要があります。 Windows 用の Microsoft Visual Studio Express をインストールすると、ウィザードを含まないバージョンの SDK がインストールされます。

     

次の手順では、アプリをビルドし、デバイスのメタデータをインストールします。

1.  テスト署名を有効にします。
    1.  DeviceMetadataWizard をダブルクリックして、 *% ProgramFiles (x86)%* \\Windows kit\\8.1\\bin\\x86 から、**デバイスメタデータ作成ウィザード**を開始し**ます。**
    2.  **[ツール]** メニューの **[テスト署名を有効にする]** を選択します。

2.  コンピューターを再起動する
3.  ソリューション (.sln) ファイルを開いて、ソリューションをビルドします。 F7 キーを押すか、サンプルが読み込まれた後で、上部のメニューから [**ビルド-&gt;ビルド**] をクリックします。

4.  プリンタを切断し、アンインストールします。 この手順は、デバイスが次回検出されたときに、更新されたデバイスメタデータを Windows が読み取るようにするために必要です。
5.  デバイスメタデータを編集して保存します。 デバイスアプリをデバイスにリンクするには、デバイスアプリをデバイスに関連付ける必要があります。
    **注**  デバイスのメタデータをまだ作成していない場合は、「 [UWP デバイスアプリのデバイスメタデータを作成](https://go.microsoft.com/fwlink/p/?LinkId=313644)する」を参照してください。

     

    1.  **デバイスメタデータの作成ウィザード**がまだ開いていない場合は、 **DeviceMetadataWizard**をダブルクリックして、 *% ProgramFiles (X86)%* \\Windows kit\\8.1\\bin\\x86 から起動します。
    2.  **[デバイスメタデータの編集]** をクリックします。 これにより、既存のデバイスメタデータパッケージを編集できるようになります。
    3.  **[開く]** ダイアログボックスで、UWP デバイスアプリに関連付けられているデバイスメタデータパッケージを見つけます。 ( **Devicemetadata**ファイル拡張子が付いています)。
    4.  **[Uwp デバイスアプリ情報の指定]** ページで、 **[uwp デバイスアプリ]** ボックスに Microsoft Store アプリ情報を入力します。 **[UWP アプリケーションマニフェストファイルのインポート]** をクリックすると、**パッケージ名**、**発行者名**、および**UWP アプリ ID**が自動的に入力されます。
    5.  アプリがプリンター通知に登録されている場合は、 **[通知ハンドラー]** ボックスに入力します。 **[イベント ID]** に、印刷イベントハンドラーの名前を入力します。 **[イベントアセット]** に、そのコードが存在するファイルの名前を入力します。

    6.  完了したら、 **[完了]** ページが表示されるまで **[次へ]** をクリックします。
    7.  **[デバイスメタデータパッケージの確認]** ページで、すべての設定が正しいことを確認し、 **[ローカルコンピューターのメタデータストアにデバイスメタデータパッケージをコピーする]** チェックボックスをオンにします。 **[保存]** をクリックします。

6.  デバイスが接続されているときに、Windows によって更新されたデバイスメタデータが読み取られるように、プリンターを再接続します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイスのメンテナンス (v4 プリンタードライバー)](https://docs.microsoft.com/windows-hardware/drivers/print/device-maintenance)

[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[UWP デバイスアプリを作成する (ステップバイステップガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスアプリのデバイスメタデータを作成する (ステップバイステップガイド)](step-2--create-device-metadata.md)

 

 






