---
title: UWP デバイス アプリでの印刷ジョブを管理する方法
description: Windows 8.1 では、プリンター用の UWP デバイス アプリは、印刷ジョブを管理できます。
ms.assetid: 30E247DB-E5B0-4CD5-89F5-4227EE20A564
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea61ec736cb596a7c1b8d36dd379fc04923cf8aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330697"
---
# <a name="how-to-manage-print-jobs-in-a-uwp-device-app"></a>UWP デバイス アプリでの印刷ジョブを管理する方法


Windows 8.1 では、プリンター用の UWP デバイス アプリは、印刷ジョブを管理できます。 このトピックでは、C#のバージョン、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)印刷ジョブのビューを作成、それらのジョブを監視および必要に応じて、ジョブをキャンセルする方法を示すサンプル。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

C#のバージョン、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルではプリンターでのメンテナンス、 **DeviceMaintenance.xaml.cs**ファイル、 **DeviceAppForPrinters2**プロジェクト。 サンプルを Bidi を使用するでプリンターの拡張機能ライブラリを使用して、 **PrinterExtensionLibrary**プロジェクト。 プリンターの拡張機能ライブラリでは、v4 印刷ドライバーのプリンター拡張機能のインターフェイスにアクセスする便利な手段を提供します。 詳細については、次を参照してください。、[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)します。

**注**  このトピックで示すコード例に基づいています、C#のバージョン、[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプル。 このサンプルも JavaScript および C++ で使用できます。 C++ は COM を直接アクセスできるため、C++ のバージョン サンプルにはが含まれていないことコード ライブラリ プロジェクトに注意してください。 コードの最新バージョンを参照するサンプルをダウンロードします。

 

## <a name="span-idmanagingprintjobsspanspan-idmanagingprintjobsspanspan-idmanagingprintjobsspanmanaging-print-jobs"></a><span id="Managing_print_jobs"></span><span id="managing_print_jobs"></span><span id="MANAGING_PRINT_JOBS"></span>印刷ジョブの管理


Windows 8.1 には、新しい印刷ジョブを管理するために使用できる、v4 プリンター ドライバーでのプリンター拡張機能のインターフェイスが導入されています。[**IPrinterQueue2**](https://msdn.microsoft.com/library/windows/hardware/dn265389)、 [ **IPrinterQueueView**](https://msdn.microsoft.com/library/windows/hardware/dn265392)、 [ **IPrinterQueueViewEvent**](https://msdn.microsoft.com/library/windows/hardware/dn265393)、 [ **IPrintJob**](https://msdn.microsoft.com/library/windows/hardware/dn265396)、および[ **IPrintJobCollection**](https://msdn.microsoft.com/library/windows/hardware/dn265397)します。 これらのインターフェイスを使うとを監視し、印刷ジョブをキャンセルできます。 詳細については、次を参照してください。[印刷ジョブの管理 (v4 プリンター ドライバー)](https://msdn.microsoft.com/library/windows/hardware/dn265419)します。

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

     

## <a name="span-idstep1findprinterspanspan-idstep1findprinterspanspan-idstep1findprinterspanstep-1-find-printer"></a><span id="Step_1__Find_printer"></span><span id="step_1__find_printer"></span><span id="STEP_1__FIND_PRINTER"></span>手順 1: プリンターを検索します。


アプリでは、印刷ジョブを管理することには、まず、プリンターが印刷ジョブを探します。 これを行う、[印刷ジョブの管理やプリンターの管理](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルには、という名前の便利なクラスが含まれています。 `PrinterEnumeration` (で、 **PrinterEnumeration.cs**ファイル)。 このクラスは、デバイスのメタデータを使用して、アプリに関連付けられているすべてのプリンターを検索しの一覧を返します`PrinterInfo`オブジェクトで、名前と各プリンターについては、デバイス Id が含まれています。

この例では、`EnumeratePrinters_Click`メソッドで、 **PrintJobManagement.xaml.cs**ファイル。 サンプルを使用する方法を示しています、`PrinterEnumeration`クラスの一覧を取得するには、プリンターが関連付けられています。

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

**ヒント:**  の詳細については、`PrinterEnumeration`と`PrinterInfo`クラスを参照してください、 **PrinterEnumeration.cs**ファイル。

 

## <a name="span-idstep2getprinterqueuespanspan-idstep2getprinterqueuespanspan-idstep2getprinterqueuespanstep-2-get-printer-queue"></a><span id="Step_2__Get_printer_queue"></span><span id="step_2__get_printer_queue"></span><span id="STEP_2__GET_PRINTER_QUEUE"></span>手順 2: プリンター キューを取得します。


プリンターの印刷ジョブを作成、管理することを特定したら、*ビュー*に基づくオブジェクトに、印刷ジョブの`IPrinterQueueView`インターフェイス (で定義されている、 **PrinterExtensionTypes.cs**のファイル、 **PrinterExtensionLibrary**プロジェクト)。 [印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルでは、このオブジェクトの名前は`currentPrinterQueueView`とプリンターの選択が変更されるたびに再作成します。

`Printer_SelectionChanged`メソッド、サンプルの最初では、`PrinterInfo`という名前のプリンター拡張コンテキスト オブジェクトを作成するオブジェクト`context`します。 使用して、`GetPrinterQueueView`メソッドを`context`を作成する、`currentPrinterQueueView`オブジェクト。 最後に、イベント ハンドラーを処理するために追加、`currentPrinterQueueView`の`OnChanged`イベント。

この例では、`Printer_SelectionChanged`メソッドで、 **PrintJobManagement.xaml.cs**ファイル。 に基づいてプリンター キューのビュー オブジェクトを作成する方法を示します`IPrinterQueueView`します。

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

また、印刷ジョブの表示に変更があるたびにイベント ハンドラーを呼び出す、`OnPrinterQueueViewChanged`メソッド。 再バインドするため、このメソッドは、`PrintJobListBox`の IEnumerable コレクションを持つ`IPrintJob`オブジェクト。 コレクションが経由でメソッドに渡される、`PrinterQueueViewEventArgs`オブジェクトで定義されている、 **PrinterExtensionTypes.cs**ファイル。

この例では、`OnPrinterQueueViewChanged`メソッドで、 **PrintJobManagement.xaml.cs**ファイル。

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

## <a name="span-idstep3displayprintjobstatusspanspan-idstep3displayprintjobstatusspanspan-idstep3displayprintjobstatusspanstep-3-display-print-job-status"></a><span id="Step_3__Display_print_job_status"></span><span id="step_3__display_print_job_status"></span><span id="STEP_3__DISPLAY_PRINT_JOB_STATUS"></span>手順 3: 印刷ジョブの状態を表示します。


`PrintJobListBox`のコレクションにバインドされた`IPrintJob`オブジェクトの場合、ジョブの状態を表示するは非常に簡単です。 選択した印刷ジョブとしてキャスト、`IPrintJob`オブジェクト、および、そのオブジェクトのプロパティが塗りつぶしに使用、`PrintJobDetails`テキスト ボックス。

[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプルを別の印刷ジョブを選択するたびに印刷ジョブの状態が表示されます。 この更新プログラムが隠メ諶、`PrintJob_SelectionChanged`メソッド。

この例では、`PrintJob_SelectionChanged`メソッドで、 **PrintJobManagement.xaml.cs**ファイル。 に基づいて、印刷ジョブの状態を表示する方法を示します、`IPrintJob`オブジェクト。

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

印刷ジョブの状態の説明を表示できるように、`PrintJob_SelectionChanged`メソッドは、という名前の静的ディクショナリを使用して`printJobStatusDisplayNames`、わかりやすいテキスト形式ではジョブの状態の説明を表示できるようにします。

この例では、`DisplayablePrintJobStatus`クラス、 **PrintJobManagement.xaml.cs**ファイル。 このクラスにはで使用する静的メンバーが含まれています、`PrintJob_SelectionChanged`します。

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

## <a name="span-idstep4cancelprintjobspanspan-idstep4cancelprintjobspanspan-idstep4cancelprintjobspanstep-4-cancel-print-job"></a><span id="Step_4__Cancel_print_job"></span><span id="step_4__cancel_print_job"></span><span id="STEP_4__CANCEL_PRINT_JOB"></span>手順 4: 印刷ジョブをキャンセルします。


印刷ジョブの状態の表示と同様に、印刷ジョブのキャンセルはとても簡単ですがある場合、`IPrintJob`オブジェクト。 `IPrintJob`クラスには、`RequestCancel`対応する印刷ジョブの取り消しを開始するメソッド。 これは、方法については、サンプルの`CancelPrintJob_Click`メソッド。

この例では、`CancelPrintJob_Click`メソッドで、 **PrintJobManagement.xaml.cs**ファイル。

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


[ジョブの管理 (v4 プリンター ドライバー)](https://msdn.microsoft.com/library/windows/hardware/dn265419)

[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[アプリを作成する UWP デバイス (ステップ バイ ステップ ガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスのアプリ (ステップ バイ ステップ ガイド) のデバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 






