---
title: プリンター拡張機能
description: プリンター拡張アプリは、ユーザーが Windows デスクトップで既存のアプリケーションを実行するときの印刷設定とプリンター通知をサポートしています。
ms.assetid: D617A897-D93E-4006-B42D-923CA7F29D7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9aa65c8f54186b1287527a14af9ac5cf4a2acc1
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606434"
---
# <a name="printer-extensions"></a>プリンター拡張機能

プリンター拡張アプリは、ユーザーが Windows デスクトップで既存のアプリケーションを実行するときの印刷設定とプリンター通知をサポートしています。

## <a name="introduction"></a>概要

プリンター拡張は、任意の COM 対応言語で構築できますが、Microsoft .NET Framework 4 を使用して構築するように最適化されています。 プリンター拡張は、XCopy 対応であり、オペレーティングシステムに含まれているもの以外の外部ランタイム (.NET など) に依存していない場合に、印刷ドライバーパッケージと共に配布できます。 プリンター拡張機能アプリがこれらの条件を満たしていない場合は、setup.exe または MSI パッケージに配布され、v4 マニフェストに指定されている printer Extensionurl ディレクティブを使用して、プリンターのデバイスステージエクスペリエンスで提供される可能性があります。 プリンター拡張機能アプリが MSI パッケージを介して配布される場合、印刷ドライバーをパッケージに追加するか、ドライバーをそのまま残して別に配布するかを選択できます。 Printer Extensionurl は、プリンターの設定エクスペリエンスに表示されます。

IT 管理者には、プリンターの拡張機能の配布を管理するためのオプションがいくつかあります。 アプリケーションが setup.exe または MSI にパッケージされている場合、IT 管理者は、Microsoft Endpoint Configuration Manager などの標準のソフトウェア配布ツールを使用することも、標準の OS イメージにアプリケーションを含めることもできます。 IT 管理者は、v4 マニフェストに指定されているプリンターの出力を上書きすることもできます。これを行う場合は、\_ローカル\_コンピューター\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\印刷\\プリンター\\&lt;印刷キュー名&gt;\\プリンター Driverdata\\プリンターの Url を使用します。

また、エンタープライズがプリンターの拡張機能を完全にブロックすることを選択した場合は、[コンピューターの構成\\管理用テンプレート\\\\プリンター] というグループポリシーを使用して、v4 プリンタードライバーがプリンター拡張アプリケーションを表示できないようにすることができます。

## <a name="building-a-printer-extension"></a>プリンター拡張機能のビルド

GitHub の[Printer Extension サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617945)は、を使用してC#プリンター拡張機能をビルドする方法を示しています。 UWP デバイスアプリとプリンター拡張機能の間でコードを共有できるようにするために、このサンプルでは2つのプロジェクトを使用します。このサンプルでは、printer Extensionlibrary (a C) と ExtensionSample (プリンター拡張ライブラリに依存するプリンター拡張機能) を使用します。

このトピックに示されているコードスニペットはすべて、プリンターの Extensionsample ソリューションから抜粋したものです。 C C++またはその他の COM ベースの言語でプリンター拡張機能をビルドする場合、概念は似ていますが、api は、代わりに Windows Driver Kit に含まれている、「プリンター*拡張機能 .idl*」で指定されているものと一致している必要があります。 サンプルドキュメントのプリンター Extensionlibrary のコードコメントには、特定のオブジェクトが対応している基になる COM インターフェイスを示すコードコメントも含まれています。

プリンター拡張機能を開発する際には、注意する必要がある6つの主な領域があります。 これらの対象領域を次の一覧に示します。

- 登録

- イベントの有効化

- OnDriverEvent ハンドラー

- 印刷設定

- プリンター通知

- プリンターの管理

### <a name="registration"></a>登録

プリンターの拡張機能は、レジストリキーのセットを指定するか、v4 マニフェストファイルの [プリンターの拡張] セクションでアプリケーションの情報を指定することによって、印刷システムに登録されます。

プリンター拡張の各エントリポイントをサポートする Guid が指定されています。 これらの Guid を v4 マニフェストファイルで使用する必要はありませんが、v4 ドライバーのインストールにレジストリ形式を使用するには、GUID 値を把握しておく必要があります。 次の表は、2つのエントリポイントの GUID 値を示しています。

| エントリ ポイント           | GUID                                   |
|-----------------------|----------------------------------------|
| 印刷設定     | {EC8F261F-267C-469F-B5D6-3933023C29CC} |
| プリンター通知 | {23BB1328-63DE47 293-915BA6A23D929ACB} |

プリンタードライバーの外部にインストールされているプリンターの拡張機能は、レジストリを使用して登録する必要があります。 これにより、スプーラの状態やクライアントコンピュータの v4 構成モジュールに関係なく、プリンタの拡張機能をインストールできるようになります。

PrintNotify サービスが開始されると、\[OfflineRoot\] パスの下にレジストリキーがあるかどうかを確認し、保留中の登録または登録解除を処理します。 保留中の登録または登録解除が完了すると、レジストリキーはリアルタイムで削除されます。 レジストリキーを配置するためにスクリプトまたは反復的なプロセスを使用している場合は、\\\[プリンター Driverid\] キーを指定するたびに、\\\[のプリンター Extensionid\] キーを再作成する必要があることに注意してください。 不完全または間違ったキーは削除されません。

この登録は、最初のインストール時にのみ必要です。 次の例は、プリンターの拡張機能の登録に使用される正しいレジストリキーの形式を示しています。

> [!NOTE]
> **\[OfflineRoot\]** は、HKEY の短縮形として使用されます\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\Print\\Offlineプリンター拡張機能。

```Registry
[OfflineRoot]
    \[PrinterExtensionId] {GUID}
           AppPath=[PrinterExtensionAppPath] {String}
           \[PrinterDriverId] {GUID}
                  \[PrinterExtensionReasonGuid]
(default) = ["0"|"1"] {REG_SZ 0:Unregister, 1:Register}
                  \…
                  \[PrinterExtensionReasonGuidN]
           \[PrinterDriverId2]
                  \[PrinterExtensionReasonGuid2.1]
                  \…
                  \[PrinterExtensionReasonGuid2.Z]
           …
           \[PrinterDriverIdM]
    \[PrinterExtensionId2]
    …
    \[PrinterExtensionIdT]
```

たとえば、次の一連のキーは、プリンター拡張機能を {printer*Extensionidguid*} プリンター extensionid に、完全修飾パスとして {*PrinterDriverID1Guid*} と {*PrinterDriverID2Guid*} PrinterDriverIDs の "C:\\プログラム\\\\ファイルへの完全修飾パスを登録します。これには、プリンターの設定とプリンター通知の理由があります。

```Registry
[OfflineRoot]
    \{PrinterExtensionIDGuid}
           AppPath="C:\Program Files\Fabrikam\pe.exe"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "1"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "1"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "1"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "1"
```

同じプリンター拡張機能をアンインストールするには、次の一連のキーを指定する必要があります。

```Registry
[OfflineRoot]
    \{PrinterExtensionIDGuid}
           AppPath="C:\Program Files\Fabrikam\pe.exe"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "0"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "0"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "0"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "0"
```

プリンター拡張は、ユーザーが起動したコンテキストとイベントによって起動されたコンテキストの両方で実行できるため、プリンター拡張機能が動作しているコンテキストを特定できるようにすると便利です。 これにより、アプリは、通知または印刷設定のために起動された場合に、すべてのキューの状態を列挙しないようにすることができます。 Microsoft では、ドライバーとは別にインストールされているプリンターの拡張機能を使用することをお勧めします (例: MSI または setup.exe)。 [スタート] メニューのショートカット、またはの実行中にレジストリに入力された AppPath エントリの製品. ドライバーと共にインストールされるプリンターの拡張機能は DriverStore にインストールされるため、印刷設定イベントまたはプリンター通知イベントの外部では起動されません。 この場合、コマンドラインスイッチを指定することはサポートされていません。

プリンター拡張機能によって現在のプリンターの Id が登録されると、AppPath にプリンター Driverid が含まれている必要があります。 たとえば、printer *extension .exe*という名前のプリンター拡張アプリの場合、およびプリンター driverid 値が *{GUID}* の場合、\[のプリンター拡張 apppath\] は次のようになります。

```console
"C:\program files\fabrikam\printerextension.exe {GUID}"
```

### <a name="enabling-events"></a>イベントの有効化

実行時に、プリンターの拡張機能は、現在のプリンターの Id に対してイベントのトリガーを有効にする必要があります。 これは、引数\[\] 配列を介してアプリに渡されたプリンター Driverid であり、印刷システムは印刷設定やプリンターの通知などの理由を処理するための適切なイベントコンテキストを提供できます。

そのため、アプリケーションでは、現在のプリンター Driverid に対して新しい PrinterExtensionManager を作成し、OnDriverEvent イベントを処理するデリゲートを登録し、プリンター Driverid を指定して EnableEvents メソッドを呼び出す必要があります。 次のコードスニペットは、この方法を示しています。

```csharp
PrinterExtensionManager mgr = new PrinterExtensionManager();
mgr.OnDriverEvent += OnDriverEvent;
mgr.EnableEvents(new Guid(PrinterDriverID1));
```

アプリが5秒以内に EnableEvents を呼び出さない場合、Windows はタイムアウトし、標準 UI を起動します。 これを軽減するために、プリンターの拡張機能は、次のような最新のパフォーマンスのベストプラクティスに従う必要があります。

- EnableEvents を呼び出すまで、できるだけ多くのアプリの初期化を遅延させます。 その後、非同期メソッドを使用して UI の応答性を優先し、初期化中に UI スレッドをブロックしません。

- インストール中にネイティブイメージを生成するには、ngen を使用します。 詳細については、「[ネイティブイメージジェネレーター](https://docs.microsoft.com/dotnet/framework/tools/ngen-exe-native-image-generator)」を参照してください。

- パフォーマンス測定ツールを使用して、読み込み時のパフォーマンスの問題を見つけます。 詳細については、「 [Windows パフォーマンス分析ツール](https://docs.microsoft.com/windows-hardware/test/wpt/)」を参照してください。

### <a name="driverevent-handler"></a>DriverEvent ハンドラー

OnDriverEvent ハンドラーが登録され、イベントが有効になると、印刷設定またはプリンターの通知を処理するためにプリンターの拡張機能が起動された場合、ハンドラーが呼び出されます。 前のコードスニペットでは、OnDriverEvent というメソッドがイベントハンドラーとして登録されていました。 次のコードスニペットでは、printer *Extensioneventargs*パラメーターは、印刷設定とプリンター通知シナリオを構築できるようにするオブジェクトです。 *プリンター extensioneventargs*は、 [**iプリンター extensioneventargs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)のラッパーです。

```csharp
static void OnDriverEvent(object sender, PrinterExtensionEventArgs eventArgs)
{
    //
    // Display the print preferences window.
    //

    if (eventArgs.ReasonId.Equals(PrinterExtensionReason.PrintPreferences))
    {
        PrintPreferenceWindow printPreferenceWindow = new PrintPreferenceWindow();
        printPreferenceWindow.Initialize(eventArgs);

        //
        // Set the caller application's window as parent/owner of the newly created printing preferences window.
        //

        WindowInteropHelper wih = new WindowInteropHelper(printPreferenceWindow);
        wih.Owner = eventArgs.WindowParent;

        //
        // Display a modal/non-modal window based on the 'WindowModal' parameter.
        //

        if (eventArgs.WindowModal)
        {
            printPreferenceWindow.ShowDialog();
        }
        else
        {
            printPreferenceWindow.Show();
        }
    }

    //
    // Handle driver events.
    //

    else if (eventArgs.ReasonId.Equals(PrinterExtensionReason.DriverEvent))
    {
        // Handle driver events here.
    }
}
```

クラッシュまたは低速のプリンター拡張に関連する不適切なユーザーエクスペリエンスを防ぐために、アプリの起動後に短い時間内に EnableEvents が呼び出されない場合、Windows はタイムアウトを実装します。 デバッグを有効にするために、PrintNotify サービスにデバッガーがアタッチされている場合、このタイムアウトは無効になります。

ただし、ほとんどの場合、必要なアプリ関連のすべてのコードは、OnDriverEvent コールバックの実行中または後に実行されます。 開発時に、OnDriverEvent コールバックから印刷設定またはプリンター通知エクスペリエンスを開始する前に、メッセージボックスを表示すると便利な場合もあります。 メッセージボックスが表示されたら、Visual Studio に戻り &gt; **[デバッグ]** をクリックして**プロセスにアタッチ**し、プロセスの名前を選択します。 最後に、MessageBox に戻り、[OK] をクリックして再開します。 これにより、例外が表示され、その時点からブレークポイントがヒットします。

今後、新しい理由 Id がサポートされる可能性があります。 そのため、プリンター拡張では、理由 Id を明示的に確認する必要があり、"else" ステートメントを使用して最後の既知の理由 Id を検出することはできません。 理由 Id が受信され、不明な場合は、アプリを正常に終了する必要があります。

### <a name="print-preferences"></a>印刷設定

印刷設定は、PrintSchemaEventArgs. Ticket オブジェクトによって駆動されます。 このオブジェクトは、デバイスの機能とオプションを記述する PrintTicket と PrintCapabilities の両方のドキュメントをカプセル化します。 基になる XML も利用できますが、オブジェクトモデルを使用すると、これらの形式を簡単に操作できます。

各[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)オブジェクトまたは[**Iprintschemacapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)オブジェクトの中には、特徴 ([**IPrintSchemaFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemafeature)) とオプション ([**iprintschemaoption**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemaoption)) があります。 機能とオプションに使用されるインターフェイスは、オリジンに関係なく同じですが、基になる XML の結果として動作が多少異なります。 たとえば、PrintCapabilities documents では、機能ごとに多くのオプションが指定されていますが、PrintTicket ドキュメントでは選択した (または既定の) オプションのみが指定されています。 同様に、PrintCapabilities ドキュメントではローカライズされた表示文字列を指定しますが、PrintTicket ドキュメントでは指定しません。

プリンター [Extensionsample](https://go.microsoft.com/fwlink/p/?LinkId=617945)は、データバインディングを使用して、プリンターの基本設定用の ComboBox コントロールを作成します。 データバインディングを使用することをお勧めします。これにより、拡散を減らすことでコードをより簡単に管理できるようになります。 WPF でのデータバインディングの詳細については、「[データバインディングの概要](https://docs.microsoft.com/dotnet/framework/wpf/data/data-binding-overview)」を参照してください。

パフォーマンスを最大化するために、GetPrintCapabilities の呼び出しは PrintCapabilities ドキュメントの更新が必要な場合にのみ実行することをお勧めします。

ユーザーがデータバインドコンボボックスコントロールを使用して選択を行うと、PrintTicket オブジェクトが自動的に更新されます。 ユーザーが最後に **[OK]** をクリックすると、非同期検証と完了のチェーンが開始されます。 この非同期パターンは、実行時間の長いタスクが UI スレッド上で発生し、印刷設定 UI または印刷中のアプリでハングが発生するのを防ぐために広く使用されています。 ユーザーが **[OK]** をクリックした後に、PrintTicket の変更を処理するために使用される手順の一覧を次に示します。

1. PrintSchemaTicket は、 [**IPrintSchemaTicket:: ValidateAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprintschematicket-validateasync)メソッドを使用して asynchrously を検証します。

1. 非同期検証が完了すると、共通言語ランタイム (CLR) によって PrintTicketValidateCompleted メソッドが呼び出されます。

    1. 検証が成功した場合は、 [**IPrintSchemaTicket:: CommitAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprintschematicket-commitasync)メソッドを呼び出して、コミットされたメソッドを呼び出します。 また、更新プログラムの PrintTicket が正常に完了すると、PrintTicketCommitCompleted メソッドが呼び出されます。これは、印刷の設定が完了したことを示すために、print Extensioneventargs. Request. Complete メソッドを呼び出す便利なメソッドを呼び出します。次に、アプリを閉じます。

    1. それ以外の場合は、制約の状況を処理するための UI がユーザーに表示されます。

ユーザーが [キャンセル] をクリックするか、[印刷設定] ウィンドウを直接閉じた場合、プリンターの拡張機能は、エラーログに対応する HRESULT 値とメッセージを使用して、Iprinter Extensioneventargs. Request. Cancel を呼び出します。

プリンター拡張機能のプロセスが閉じられていて、前の段落で説明したとおりに Complete メソッドまたは Cancel メソッドが呼び出されていない場合、印刷システムは Microsoft が提供する UI を自動的に使用するように切り替えます。

デバイスの状態情報を取得するために、プリンター拡張では、Bidi を使用して印刷デバイスを照会できます。 たとえば、デバイスに関するインクの状態またはその他の種類の状態を表示するには、プリンターの拡張機能を使用して、デバイスに対して Bidi クエリを発行することができます。 最新の Bidi ステータスを取得するには、OnBidiResponseReceived イベントのイベントハンドラーを設定し、有効な Bidi クエリを使用して SendBidiQuery メソッドを呼び出すという、2段階のプロセスを実行します。 次のコードスニペットは、この2つの手順を示しています。

```csharp
PrinterQueue.OnBidiResponseReceived += new
EventHandler<PrinterQueueEventArgs>(OnBidiResponseReceived);
PrinterQueue.SendBidiQuery("\\Printer.consumables");
```

Bidi 応答を受信すると、次のイベントハンドラーが呼び出されます。 このイベントハンドラーにはモックインクステータスの実装も含まれていることに注意してください。これは、デバイスが使用できない場合に開発に役立つことがあります。 プリンター Queueeventargs オブジェクトには、HRESULT と Bidi XML 応答の両方が含まれています。 Bidi XML 応答の詳細については、「 [Bidi 要求および応答スキーマ](https://docs.microsoft.com/previous-versions/dd183368(v=vs.85))」を参照してください。

```csharp
private void OnBidiResponseReceived(object sender, PrinterQueueEventArgs e)
{
    if (e.StatusHResult != (int)HRESULT.S_OK)
    {
        MockInkStatus();
        return;
    }

    //
    // Display the ink levels from the data.
    //

    BidiHelperSource = new BidiHelper(e.Response);
    if (PropertyChanged != null)
    {
        PropertyChanged(this, new PropertyChangedEventArgs("BidiHelperSource"));
    }
    InkStatusTitle = "Ink status (Live data)";
}
```

### <a name="printer-notifications"></a>プリンター通知

プリンター通知は、印刷設定とまったく同じ方法で呼び出されます。 OnDriverEvent ハンドラーで、Iプリンター Extensioneventargs が DriverEvents GUID と一致することを示した場合、このイベントを処理するエクスペリエンスを構築できます。

プリンター [Extensionsample](https://go.microsoft.com/fwlink/p/?LinkId=617945)プロジェクトは、機能的なプリンター通知エクスペリエンスを示すものではありませんが、次の変数はこの処理に最も役立ちます。

- BidiNotification –イベントがトリガーされる原因となった Bidi XML を格納します。

- DetailedReasonId –ドライバーイベント xml ファイルからの eventID GUID を含みます。

通知用の Iプリンター Extensioneventargs オブジェクトの最も重要な属性は、BidiNotification プロパティです。 これにより、イベントがトリガーされた Bidi XML が格納されます。 Bidi XML 応答の詳細については、「 [Bidi 要求および応答スキーマ](https://docs.microsoft.com/previous-versions/dd183368(v=vs.85))」を参照してください。

### <a name="managing-printers"></a>プリンターの管理

プリンター拡張機能の役割を、プリンターの管理と維持のためのハブとして使用できるアプリとしてサポートするために、現在のプリンター拡張機能が登録されている印刷キューを列挙し、各キューの状態を取得することができます。 これは、プリンターの Extensionsample プロジェクトでは説明されていませんが、App.xaml.cs の Main メソッドに次のコードスニペットを追加して、イベントハンドラーを登録することができます。

```csharp
mgr.OnPrinterQueuesEnumerated += new EventHandler<PrinterQueuesEnumeratedEventArgs>(mgr_OnPrinterQueuesEnumerated);
```

キューが列挙されると、イベントハンドラーが呼び出され、状態操作が実行されます。 このイベントは、アプリの有効期間中に定期的に発生し、列挙された印刷キューのリストが最新のものであることを確認します。これは、ユーザーが開いた後にキューを追加した場合でも同様です。 このため、イベントハンドラーは、実行されるたびに新しいウィンドウを作成しないことが重要です。これを次のコードスニペットに示します。

```csharp
static void mgr_OnPrinterQueuesEnumerated(object sender, PrinterQueuesEnumeratedEventArgs e)
{
    foreach (IPrinterExtensionContext pContext in e)
    {
        // show status
    }
}
```

プリンター拡張機能を使用してメンテナンスタスクを実行するには、次の擬似コードに示されているように、レガシ WritePrinter API を使用することをお勧めします。

```Pseudocode
OpenPrinter
    StartDocPrinter
        StartPagePrinter
          WritePrinter
        EndPagePrinter
    EndDocPrinter
ClosePrinter
```

これらのレガシ Api を .NET にマーシャリングする方法の詳細については、「 [Visual C# .net を使用してプリンターに生データを送信する方法](https://support.microsoft.com/help/322091)」または「 [Visual Basic .net を使用してプリンターに生データを送信する](https://support.microsoft.com/help/322090)方法」を参照してください。

## <a name="printer-extension-performance-best-practices"></a>プリンター拡張機能のパフォーマンスに関するベストプラクティス

最適なユーザーエクスペリエンスを実現するために、プリンターの拡張機能をできるだけ高速に読み込むように設計する必要があります。 Printer Extension サンプルプロジェクトは .NET アプリケーションです。つまり、中間言語 (IL) に組み込まれています。これは、実行時にネイティブプロセッサアーキテクチャに適した形式にコンパイルする必要があることを意味します。 インストール中に、アプリケーションがネイティブシステムアーキテクチャ用にコンパイルされていることを確認するために、ベストプラクティスに従ってプリンターの拡張機能をインストールすることをお勧めします。 コードのコンパイルとインストールのベストプラクティスの詳細については、「[デスクトップアプリケーションの起動パフォーマンスの向上](https://devblogs.microsoft.com/dotnet/improving-launch-performance-for-your-desktop-applications/)」を参照してください。

また、Microsoft では、EnableEvents メソッドが呼び出されるまで、リソースの読み込みなどの初期化タスクを、プリンター拡張で延期することをお勧めします。 これにより、プリンター拡張の5秒のタイムアウトの前に、アプリが EnableEvents を呼び出す可能性が最小限に抑えられます。

OnDriverEvent 呼び出しの後、プリンターの拡張機能は UI を初期化し、できるだけ早く描画します。これにより、可能な限り非同期メソッドを使用して応答性を確保することができます。 印刷設定またはプリンター通知の初期ウィンドウ状態を作成するには、プリンターの拡張機能がネットワーク呼び出しまたは Bidi に依存していない必要があります。

ユーザーが、PrintTicket に影響を与える画面上の UI を使用して選択を行うと、プリンターの拡張機能は、できるだけ早く変更を検証するために IPrintSchemaTicket:: ValidateAsync メソッドを使用する必要があります。 最後に、 [**IPrintSchemaTicket:: CommitAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprintschematicket-commitasync)メソッドを使用して、PrintTicket の変更をコミットする必要があります。

プリンターの拡張機能は、呼び出されたプロセスから常にプロセス外で実行されます。 そのため、プリンター拡張機能を開発するときは、ウィンドウの動作を考慮する必要があります。

- [**Iプリンター Extensioneventargs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)の**windowparent**プロパティは、アプリを呼び出したウィンドウへのハンドルを指定します。
- [**Iprinter Extensioneventargs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)の**windowmodal**プロパティは、プリンター拡張機能 (印刷設定モード) をモーダルで実行するかどうかを指定します。

プリンター拡張のサンプルでは、通常、最上位のウィンドウとして起動される UI を作成する方法を示します。 ただし、ui が呼び出される原因となったプロセスが別の整合性レベルで実行されている場合や、プロセスが別のプロセッサアーキテクチャ用にコンパイルされた場合など、UI がフォアグラウンドに表示されない場合もあります。 この場合、プリンターの拡張機能は FlashWindowEx を呼び出して、タスクバーのアイコンを点滅させることにより、ユーザーのアクセス許可をフォアグラウンドに要求する必要があります。

## <a name="related-topics"></a>関連トピック

[Bidi の要求と応答のスキーマ](https://docs.microsoft.com/previous-versions/dd183368(v=vs.85))

[データ バインディングの概要](https://docs.microsoft.com/dotnet/framework/wpf/data/data-binding-overview)

[Visual Basic .NET を使用してプリンターに生データを送信する方法](https://support.microsoft.com/help/322090)

[Visual C# .net を使用してプリンターに生データを送信する方法](https://support.microsoft.com/help/322091)

[デスクトップアプリケーションの起動パフォーマンスの向上](https://devblogs.microsoft.com/dotnet/improving-launch-performance-for-your-desktop-applications/)

[ネイティブイメージジェネレーター](https://docs.microsoft.com/dotnet/framework/tools/ngen-exe-native-image-generator)

[印刷スキーマインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)

[プリンター拡張機能のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617945)

[Windows パフォーマンス分析ツール](https://docs.microsoft.com/windows-hardware/test/wpt/)
