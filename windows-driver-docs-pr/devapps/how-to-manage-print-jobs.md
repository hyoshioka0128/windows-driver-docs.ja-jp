---
title: UWP デバイスアプリで印刷ジョブを管理する方法
description: Windows 8.1 では、プリンター用の UWP デバイスアプリで印刷ジョブを管理できます。
ms.assetid: 30E247DB-E5B0-4CD5-89F5-4227EE20A564
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d319ab0e926f270f08084aa9b2e4ef3b7e9aff6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829908"
---
# <a name="how-to-manage-print-jobs-in-a-uwp-device-app"></a>UWP デバイスアプリで印刷ジョブを管理する方法


Windows 8.1 では、プリンター用の UWP デバイスアプリで印刷ジョブを管理できます。 このトピックではC# 、[印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルのバージョンを使用して、印刷ジョブのビューを作成し、それらのジョブを監視し、必要に応じてジョブをキャンセルする方法を示します。 UWP デバイスアプリ全般の詳細については、 [uwp デバイスアプリの準拠](meet-uwp-device-apps.md)に関するページを参照してください。

C# [印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルのバージョンは、 **DeviceAppForPrinters2**プロジェクトの**DeviceMaintenance.xaml.cs**ファイルを使用したプリンターのメンテナンスを示しています。 このサンプルでは、Bidi を操作するために、**プリンターの拡張**機能ライブラリを使用します。 プリンター拡張ライブラリは、v4 印刷ドライバーのプリンター拡張機能インターフェイスにアクセスするための便利な方法を提供します。 詳細については、「[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)」を参照してください。

このトピックに示されているコード例は、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルのC#バージョンに基づい**て  ます**。 このサンプルは、JavaScript およびC++でも使用できます。 は COM にC++直接アクセスできるため、サンプルC++のバージョンにはコードライブラリプロジェクトが含まれていないことに注意してください。 サンプルをダウンロードして、最新バージョンのコードを確認してください。

 

## <a name="span-idmanaging_print_jobsspanspan-idmanaging_print_jobsspanspan-idmanaging_print_jobsspanmanaging-print-jobs"></a><span id="Managing_print_jobs"></span><span id="managing_print_jobs"></span><span id="MANAGING_PRINT_JOBS"></span>印刷ジョブの管理


Windows 8.1 では、印刷ジョブの管理に使用できる、 [**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)、 [**iIPrinterQueueViewEvent queueview**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueview)、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueviewevent)、 [**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjob)、および[**iprinterqueueview**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjobcollection)の新しいプリンター拡張インターフェイスが v4 プリンタードライバーに導入されています。 これらのインターフェイスを使用すると、印刷ジョブを監視および取り消すことができます。 詳細については、「[印刷ジョブの管理 (V4 プリンタードライバー)](https://docs.microsoft.com/windows-hardware/drivers/print/job-management)」を参照してください。

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

     

## <a name="span-idstep_1__find_printerspanspan-idstep_1__find_printerspanspan-idstep_1__find_printerspanstep-1-find-printer"></a><span id="Step_1__Find_printer"></span><span id="step_1__find_printer"></span><span id="STEP_1__FIND_PRINTER"></span>手順 1: プリンターを検索する


アプリで印刷ジョブを管理するには、まず印刷ジョブがあるプリンターを見つける必要があります。 これを行うために、[印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルには、( **PrinterEnumeration.cs**ファイルに) `PrinterEnumeration` という便利なクラスが含まれています。 このクラスは、デバイスメタデータを使用してアプリに関連付けられているすべてのプリンターを検索し、各プリンターの名前とデバイス Id を含む `PrinterInfo` オブジェクトの一覧を返します。

この例は、 **PrintJobManagement.xaml.cs**ファイルの `EnumeratePrinters_Click` メソッドを示しています。 このサンプルでは、`PrinterEnumeration` クラスを使用して、関連付けられているプリンターの一覧を取得する方法を示します。

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

 

## <a name="span-idstep_2__get_printer_queuespanspan-idstep_2__get_printer_queuespanspan-idstep_2__get_printer_queuespanstep-2-get-printer-queue"></a><span id="Step_2__Get_printer_queue"></span><span id="step_2__get_printer_queue"></span><span id="STEP_2__GET_PRINTER_QUEUE"></span>手順 2: プリンターキューを取得する


管理する印刷ジョブがあるプリンターを特定したら、`IPrinterQueueView` インターフェイス **(プリンターの** **PrinterExtensionTypes.cs**ファイルで定義されている) に基づくオブジェクトを使用して、印刷ジョブの*ビュー*を作成します。 [印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルでは、このオブジェクトの名前は `currentPrinterQueueView` で、プリンターの選択が変更されるたびに再作成されます。

`Printer_SelectionChanged` メソッドでは、サンプルはまず `PrinterInfo` オブジェクトを使用して、`context`という名前のプリンター拡張コンテキストオブジェクトを作成します。 次に、`context` の `GetPrinterQueueView` メソッドを使用して、`currentPrinterQueueView` オブジェクトを作成します。 最後に、イベントハンドラーを追加して、`currentPrinterQueueView`の `OnChanged` イベントを処理します。

この例は、 **PrintJobManagement.xaml.cs**ファイルの `Printer_SelectionChanged` メソッドを示しています。 `IPrinterQueueView`に基づいてプリンターキュービューオブジェクトを作成する方法を示します。

```CSharp
private void Printer_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    try
    {
        // Remove the current printer queue view (if any) before displaying the new view.
        if (currentPrinterQueueView != null)
        {
            currentPrinterQueueView.OnChanged -= OnPrinterQueueViewChanged;
            currentPrinterQueueView = null;
        }

        // Retrieve a COM IPrinterExtensionContext object, using the static WinRT factory.
        // Then instantiate one "PrinterExtensionContext" object that allows operations on the COM object.
        PrinterInfo queue = (PrinterInfo)PrinterComboBox.SelectedItem;
        Object comComtext = Windows.Devices.Printers.Extensions.PrintExtensionContext.FromDeviceId(queue.DeviceId);
        PrinterExtensionContext context = new PrinterExtensionContext(comComtext);

        // Display the printer queue view.
        const int FirstPrintJobEnumerated = 0;
        const int LastPrintJobEnumerated = 10;

        currentPrinterQueueView = context.Queue.GetPrinterQueueView(FirstPrintJobEnumerated, LastPrintJobEnumerated);
        currentPrinterQueueView.OnChanged += OnPrinterQueueViewChanged;
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

また、印刷ジョブのビューが変更されるたびに、イベントハンドラーは `OnPrinterQueueViewChanged` メソッドを呼び出します。 このメソッドは、`IPrintJob` オブジェクトの IEnumerable コレクションで `PrintJobListBox` を再バインドする役割を担います。 コレクションは、 **PrinterExtensionTypes.cs**ファイルで定義されている `PrinterQueueViewEventArgs` オブジェクトを介してメソッドに渡されます。

この例は、 **PrintJobManagement.xaml.cs**ファイルの `OnPrinterQueueViewChanged` メソッドを示しています。

```CSharp
private async void OnPrinterQueueViewChanged(object sender, PrinterQueueViewEventArgs e)
{
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        // Update the data binding on the ListBox that displays print jobs.
        PrintJobListBox.ItemsSource = e.Collection;
        if (PrintJobListBox.Items.Count > 0)
        {
            // If there are print jobs in the current view, mark the first job as selected.
            PrintJobListBox.SelectedIndex = 0;
        }
    });
}
```

## <a name="span-idstep_3__display_print_job_statusspanspan-idstep_3__display_print_job_statusspanspan-idstep_3__display_print_job_statusspanstep-3-display-print-job-status"></a><span id="Step_3__Display_print_job_status"></span><span id="step_3__display_print_job_status"></span><span id="STEP_3__DISPLAY_PRINT_JOB_STATUS"></span>手順 3: 印刷ジョブの状態を表示する


`PrintJobListBox` は `IPrintJob` オブジェクトのコレクションにバインドされているため、ジョブの状態を表示するのは非常に簡単です。 選択した印刷ジョブは `IPrintJob` オブジェクトとしてキャストされ、そのオブジェクトのプロパティを使用して `PrintJobDetails` テキストボックスに入力されます。

[印刷ジョブの管理とプリンターのメンテナンス](https://go.microsoft.com/fwlink/p/?LinkID=299829)のサンプルでは、印刷ジョブの状態は、別の印刷ジョブが選択されるたびに表示されます。 この更新は、`PrintJob_SelectionChanged` 方法によって行われます。

この例は、 **PrintJobManagement.xaml.cs**ファイルの `PrintJob_SelectionChanged` メソッドを示しています。 ここでは、`IPrintJob` オブジェクトに基づいて印刷ジョブの状態を表示する方法を示します。

```CSharp
private void PrintJob_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    try
    {
        // Display details of the selected print job.
        IPrintJob job = (IPrintJob)PrintJobListBox.SelectedItem;
        if (job != null)
        {
            PrintJobDetails.Text =
                "Details of print job: " + job.Name + "\r\n" +
                "Pages printed: " + job.PrintedPages + "/" + job.TotalPages + "\r\n" +
                "Submission time: " + job.SubmissionTime + "\r\n" +
                "Job status: " + DisplayablePrintJobStatus.ToString(job.Status);
        }
        else
        {
            PrintJobDetails.Text = "Please select a print job";
        }
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

印刷ジョブの状態の説明を表示するために、`PrintJob_SelectionChanged` 方法では、`printJobStatusDisplayNames`という名前の静的ディクショナリを使用して、ユーザーにわかりやすいテキスト形式のジョブの状態の説明を表示します。

この例は、 **PrintJobManagement.xaml.cs**ファイルの `DisplayablePrintJobStatus` クラスを示しています。 このクラスには、`PrintJob_SelectionChanged`によって使用される静的メンバーが含まれています。

```CSharp
internal class DisplayablePrintJobStatus
{
    /// <summary>
    /// Converts the PrintJobStatus bit fields to a display string.
    /// </summary>
    internal static string ToString(PrintJobStatus printJobStatus)
    {
        StringBuilder statusString = new StringBuilder();

        // Iterate through each of the PrintJobStatus bits that are set and convert it to a display string.
        foreach (var printJobStatusDisplayName in printJobStatusDisplayNames)
        {
            if ((printJobStatusDisplayName.Key & printJobStatus) != 0)
            {
                statusString.Append(printJobStatusDisplayName.Value);
            }
        }

        int stringlen = statusString.Length;
        if (stringlen > 0)
        {
            // Trim the trailing comma from the string.
            return statusString.ToString(0, stringlen - 1);
        }
        else
        {
            // If no print job status field was set, display "Not available".
            return "Not available";
        }
    }

    /// <summary>
    /// Static constructor that initializes the display name for the PrintJobStatus field.
    /// </summary>
    static DisplayablePrintJobStatus()
    {
        printJobStatusDisplayNames = new Dictionary<PrintJobStatus, string>();

        printJobStatusDisplayNames.Add(PrintJobStatus.Paused, "Paused,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Error, "Error,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Deleting, "Deleting,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Spooling, "Spooling,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Printing, "Printing,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Offline, "Offline,");
        printJobStatusDisplayNames.Add(PrintJobStatus.PaperOut, "Out of paper,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Printed, "Printed,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Deleted, "Deleted,");
        printJobStatusDisplayNames.Add(PrintJobStatus.BlockedDeviceQueue, "Blocked device queue,");
        printJobStatusDisplayNames.Add(PrintJobStatus.UserIntervention, "User intervention required,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Restarted, "Restarted,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Complete, "Complete,");
        printJobStatusDisplayNames.Add(PrintJobStatus.Retained, "Retained,");
    }
    
    /// <summary>
    /// Private constructor to prevent default instantiation.
    /// </summary>
    private DisplayablePrintJobStatus() { }

    /// <summary>
    /// Contains the mapping between PrintJobStatus fields and display strings.
    /// </summary>
    private static Dictionary<PrintJobStatus, string> printJobStatusDisplayNames;
}
```

## <a name="span-idstep_4__cancel_print_jobspanspan-idstep_4__cancel_print_jobspanspan-idstep_4__cancel_print_jobspanstep-4-cancel-print-job"></a><span id="Step_4__Cancel_print_job"></span><span id="step_4__cancel_print_job"></span><span id="STEP_4__CANCEL_PRINT_JOB"></span>手順 4: 印刷ジョブをキャンセルする


印刷ジョブの状態を表示するのと同様に、`IPrintJob` オブジェクトがある場合、印刷ジョブをキャンセルするのは非常に簡単です。 `IPrintJob` クラスには、対応する印刷ジョブの取り消しを開始する `RequestCancel` メソッドが用意されています。 これは、サンプルの `CancelPrintJob_Click` メソッドに示されています。

この例は、 **PrintJobManagement.xaml.cs**ファイルの `CancelPrintJob_Click` メソッドを示しています。

```CSharp
private void CancelPrintJob_Click(object sender, RoutedEventArgs e)
{
    try
    {
        IPrintJob job = (IPrintJob)PrintJobListBox.SelectedItem;
        job.RequestCancel();
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
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


[ジョブ管理 (v4 プリンタードライバー)](https://docs.microsoft.com/windows-hardware/drivers/print/job-management)

[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[UWP デバイスアプリを作成する (ステップバイステップガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスアプリのデバイスメタデータを作成する (ステップバイステップガイド)](step-2--create-device-metadata.md)

 

 






