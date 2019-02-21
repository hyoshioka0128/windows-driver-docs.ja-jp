---
title: プリンターの拡張機能
description: プリンター拡張アプリは、ユーザーが Windows デスクトップで既存のアプリケーションを実行すると、印刷設定とプリンターの通知をサポートします。
ms.assetid: D617A897-D93E-4006-B42D-923CA7F29D7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ac419a9f97ecb648733dd3244c41e632ff722b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549642"
---
# <a name="printer-extensions"></a>プリンターの拡張機能

プリンター拡張アプリは、ユーザーが Windows デスクトップで既存のアプリケーションを実行すると、印刷設定とプリンターの通知をサポートします。

## <a name="introduction"></a>概要

プリンター拡張は、任意の COM 対応の言語で構築できますは Microsoft .NET Framework 4 を使用してビルドするように最適化されます。 XCopy できるされていて、たとえば、.NET など、オペレーティング システムに含まれているもの以外の外部のランタイムに依存関係があるない場合、プリンターの拡張機能は、印刷ドライバー パッケージと共に配布されます。 プリンター拡張アプリでは、これらの条件を満たしていない場合、setup.exe または MSI パッケージで配布し、v4 のマニフェストで指定された PrinterExtensionUrl ディレクティブを使用してプリンターの Device Stage エクスペリエンスで提供される可能性があります。 プリンター拡張アプリは、MSI パッケージを使用して配布するときに、印刷ドライバーをパッケージに追加またはしておくと、ドライバーを個別に配布するオプションがあります。 PrinterExtensionUrl プリンター基本設定のエクスペリエンスに表示されます。

IT 管理者では、プリンターの拡張機能の配布を管理するためのいくつかのオプションがあります。 場合は、アプリケーションは、setup.exe または MSI にパッケージ化は、IT 管理者は標準のソフトウェア配布ツール System Center Configuration Manager (SCCM) などを使用して、またはアプリケーションの標準 OS イメージに含めることができます。 HKEY を編集する場合、IT 管理者は、v4 マニフェストで指定された PrinterExtensionUrl を上書きもできます\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\印刷\\プリンター\\&lt;印刷キュー名&gt;\\PrinterDriverData\\PrinterExtensionUrl します。

呼ばれるグループ ポリシーを使用して実行する場合は、企業は、プリンターの拡張機能を完全にブロックするが、この"コンピューターの構成\\管理用テンプレート\\プリンター\\v4 プリンター ドライバーを表示するには許可しません。プリンター拡張アプリ"。

## <a name="building-a-printer-extension"></a>プリンターの拡張機能を構築

[プリンター拡張機能サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617945)github を使用してプリンター拡張機能を構築する方法を示しています。C#します。 UWP デバイス アプリとプリンターの拡張機能間のコード共有を許可するためには、このサンプルは、2 つのプロジェクトを使用します。PrinterExtensionLibrary (C) と ExtensionSample (、PrinterExtensionLibrary に依存しているプリンター拡張)。

このトピックで示すコード スニペットはすべて PrinterExtensionSample ソリューションから取得します。 C、C++ またはその他の COM ベース言語でのプリンター拡張機能を構築する場合は、概念は似ていますが、Api で指定されている一致する必要があります代わりに*PrinterExtension.IDL*、Windows ドライバー キットに含まれています。 サンプル ドキュメントから PrinterExtensionLibrary でコードのコメントには、特定のオブジェクトに対応する基になる COM インターフェイスを示すコードのコメントも含まれます。

プリンターの拡張機能を開発するときのフォーカスを意識する必要のある 6 つの主な領域があります。 これらの分野は、次の一覧に表示されます。

- 登録

- イベントを有効にします。

- OnDriverEvent ハンドラー

- 印刷設定

- プリンターの通知

- プリンターの管理

### <a name="registration"></a>登録

プリンターの拡張機能は、レジストリ キーのセットを指定するか、v4 のマニフェスト ファイルの PrinterExtensions セクションでは、アプリケーションの情報を指定することによって、印刷システムに登録されます。

異なるエントリ ポイントの各プリンターの拡張をサポートする Guid を指定します。 V4 のマニフェスト ファイルでこれらの Guid を使用する必要はありませんが、v4 ドライバーのインストールのレジストリの形式を使用する GUID 値を知る必要があります。 次の表では、2 つのエントリ ポイントの GUID 値を示します。

| エントリ ポイント           | GUID                                   |
|-----------------------|----------------------------------------|
| 印刷設定     | {EC8F261F-267C-469F-B5D6-3933023C29CC} |
| プリンターの通知 | {23BB1328-63DE-4293-915B-A6A23D929ACB} |

プリンター ドライバーの外部でインストールされているプリンターの拡張機能は、レジストリを使用して登録する必要があります。 これにより、そのプリンターがスプーラー、またはクライアント コンピューターに v4 の構成のモジュールの状態に関係なく、拡張機能をインストールできます。

PrintNotify サービスを開始するとは、下のレジストリ キーの確認、 \[OfflineRoot\]パスの登録または unregistrations 保留中の処理とします。 保留中の登録または unregistrations を完了すると、リアルタイムでレジストリ キーが削除されます。 レジストリ キーを配置するスクリプトまたは反復的なプロセスを使用する場合は、再作成する必要があります、 \\ \[PrinterExtensionID\]キーを指定するたびに、 \\ \[PrinterDriverId\]キー。 不完全なまたは正しくない形式のキーは削除されません。

この登録は、最初のインストールで必要だけです。 次の例では、プリンターの拡張機能を登録するために使用される適切なレジストリ キーの形式を示します。

> [!NOTE]
> **\[OfflineRoot\]**  HKEY の短縮形として使用される\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\印刷\\OfflinePrinterExtensions します。

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

次の一連のキーがでプリンターの拡張機能を登録するなど、{*PrinterExtensionIDGuid*} PrinterExtensionID と完全修飾パスを"c:\\Program Files\\Fabrikam\\pe.exe"の実行可能、{*PrinterDriverID1Guid*} と {*PrinterDriverID2Guid*} PrinterDriverIDs、プリンターの設定とプリンターの通知の理由を使用します。

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

同じプリンター拡張機能をアンインストールするには、次の一連のキーを指定してください。

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

プリンターの拡張機能は、ユーザーにリリースされたコンテキストと、イベント起動のコンテキストの両方で実行できる、ので、プリンターの拡張機能が動作するコンテキストを決定することができると便利です。 アプリを通知が起動された場合、すべてのキューの状態を列挙できませんや印刷設定など、このことができます。 (例: MSI や setup.exe の場合) と、ドライバーから個別にインストールされているプリンターの拡張機能がコマンド ライン スイッチ スタート メニューのショートカットのいずれかを使用することをお勧めしますまたは、中にレジストリの値が設定された AppPath エントリで。登録します。 DriverStore には、ドライバーを使用したインストールされているプリンターの拡張機能がインストールされている、ためこれらは起動できません外印刷の設定やプリンターの通知イベント。 そのためのコマンド ライン スイッチを指定はサポートされていませんここでします。

を現在 PrinterDriverID のプリンター拡張機能が登録する場合、PrinterDriverID を、AppPath、含める必要があります。 たとえば、名前のプリンター拡張アプリ*printerextension.exe*との PrinterDriverID 値 *{GUID}*、 \[PrinterExtensionAppPath\]ようになります次:

```console
"C:\program files\fabrikam\printerextension.exe {GUID}"
```

### <a name="enabling-events"></a>イベントを有効にします。

、実行時にプリンターの拡張機能は現在 PrinterDriverID のイベントをトリガーする有効にあります。 これは、引数を使用して、アプリに渡された PrinterDriverID\[ \]配列により、印刷システムの印刷設定やプリンターの通知などの理由を処理するための適切なイベントのコンテキストを提供します。

アプリケーションでは、現在 PrinterDriverID の新しい PrinterExtensionManager を作成する必要があります、OnDriverEvent イベントを処理し、PrinterDriverID して EnableEvents メソッドを呼び出すデリゲートを登録します。 次のコード スニペットは、この方法を示しています。

```csharp
PrinterExtensionManager mgr = new PrinterExtensionManager();
mgr.OnDriverEvent += OnDriverEvent;
mgr.EnableEvents(new Guid(PrinterDriverID1));
```

アプリが呼び出されません EnableEvents Windows でタイムアウトが発生し、標準的な UI を起動する、5 秒以内です。 これを防ぐためにはプリンターの拡張機能は、次を含む最新のパフォーマンス ベスト プラクティスに従う必要があります。

- 多くのアプリの初期化、できるだけまで遅らせる EnableEvents を呼び出した後。 その後、非同期メソッドを使用して初期化中に UI スレッドをブロックしていない UI の応答性を優先します。

- Ngen を使用すると、インストール時にネイティブ イメージを生成します。 詳細については、次を参照してください。[ネイティブ イメージ ジェネレーター](https://msdn.microsoft.com/library/6t9t5wcf.aspx)します。

- パフォーマンス測定ツールを使用すると、読み込みのパフォーマンスの問題を検索できます。 詳細については、次を参照してください。 [Windows パフォーマンス分析ツール](https://msdn.microsoft.com/performance/cc825801.aspx)します。

### <a name="driverevent-handler"></a>DriverEvent ハンドラー

OnDriverEvent、ハンドラーが登録されているし、イベントが有効になって印刷設定やプリンターの通知を処理するために、プリンターの拡張機能を起動した場合後、は、ハンドラーが呼び出されます。 上記のコード スニペットで OnDriverEvent という名前のメソッドは、イベント ハンドラーとして登録されました。 次のコード スニペットで、 *PrinterExtensionEventArgs*パラメーターは、構築するには、印刷設定とプリンターの通知シナリオを有効にするオブジェクト。 *PrinterExtensionEventArgs*用のラッパーです[ **IPrinterExtensionEventArgs**](https://msdn.microsoft.com/library/windows/hardware/hh973207)します。

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

関連付けられたクラッシュまたは低速の不正なユーザー エクスペリエンスを防ぐためには、プリンターの拡張機能、Windows は、EnableEvents がアプリの起動後に、時間の短い時間内で呼び出されない場合にタイムアウトを実装します。 デバッグを有効にするには、PrintNotify サービスにアタッチされたデバッガーがある場合は、このタイムアウトが無効です。

ほとんどの場合、ただし、すべて、アプリに関連するコード中、関心が実行中または OnDriverEvent コールバックの後にされます。 開発中は、いずれかを開始する前にメッセージ ボックスの印刷設定を表示する便利な場合もあります。 または OnDriverEvent コールバックからプリンターの通知が発生します。 メッセージ ボックスが表示されたら、Visual Studio に戻り、をクリックして**デバッグ** &gt; **プロセスにアタッチ**プロセスの名前を選択します。 最後に、メッセージ ボックスに戻るし、再開するには、[ok] をクリックします。 これは、例外を参照して、それ以降、ブレークポイントにヒットに保証されます。

新しい ReasonIds は今後サポート可能性があります。 その結果、プリンターの拡張機能は、ReasonID を明示的に確認する必要があり、最後の既知の ReasonID を検出するために、"else"ステートメントを使用する必要があります。 ReasonID に受信した不明な場合、アプリが正常に終了する必要があります。

### <a name="print-preferences"></a>印刷設定

印刷設定は、PrintSchemaEventArgs.Ticket オブジェクトによって決まります。 このオブジェクトは、機能とデバイスのオプションについて説明する、PrintTicket と PrintCapabilities ドキュメントをカプセル化します。 基になる XML が利用できることも、オブジェクト モデル簡単にこれらの形式を使用します。

各[ **IPrintSchemaTicket** ](https://msdn.microsoft.com/library/windows/hardware/hh451398)または[ **IPrintSchemaCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/hh451256)オブジェクトの機能があります ([ **IPrintSchemaFeature**](https://msdn.microsoft.com/library/windows/hardware/hh451284)) とオプション ([**IPrintSchemaOption**](https://msdn.microsoft.com/library/windows/hardware/hh451335))。 機能とオプションのためのインターフェイスでは、配信元に関係なく同じですが、基になる XML の結果として、動作が若干異なります。 たとえば、PrintCapabilities ドキュメントは、多くの機能、PrintTicket ドキュメントを指定だけ選択したときに (または既定値) ごとのオプション を指定します。 同様に、付きません PrintTicket ドキュメント PrintCapabilities ドキュメントは、ローカライズされた表示文字列を指定します。

[PrinterExtensionSample](https://go.microsoft.com/fwlink/p/?LinkId=617945)データ バインディングを使用して、プリンターの設定のコンボ ボックス コントロールを作成します。 により、コードの拡散を減らすことで維持するためにはるかに簡単にデータ バインディングを使用することをお勧めします。 WPF でのデータ バインディングの詳細については、次を参照してください。[データ バインディングの概要](https://msdn.microsoft.com/library/ms752347.aspx)します。

パフォーマンスを最大化するために、GetPrintCapabilities への呼び出しが PrintCapabilities ドキュメントを更新する必要がある場合のみ実行することをお勧めします。

ユーザーが選択を使用して、データにバインドされたコンボ ボックス コントロール、PrintTicket オブジェクトが自動的に更新されます。 最後に、ユーザーがクリックすると**OK**、非同期の検証と完了のチェーンが開始されます。 この非同期パターンは、実行時間の長いタスクの UI スレッドで発生している UI の基本設定が印刷または印刷しているアプリのいずれかでハングが発生しないようにするために広範に使用されます。 ユーザーがクリックした後、PrintTicket の変更を処理するために使用する手順の一覧を次に**OK**します。

1. PrintSchemaTicket が検証される asynchrously を使用して、 [ **IPrintSchemaTicket::ValidateAsync** ](https://msdn.microsoft.com/library/windows/hardware/hh451448)メソッド。

1. 非同期の検証が完了したら、共通言語ランタイム (CLR) は PrintTicketValidateCompleted メソッドを呼び出します。

    1. 検証が成功した場合は、CommitPrintTicketAsync メソッドを呼び出して CommitPrintTicketAsync 呼び出し、 [ **IPrintSchemaTicket::CommitAsync** ](https://msdn.microsoft.com/library/windows/hardware/hh451382)メソッド。 これが印刷設定が完了することを示す PrinterExtensionEventArgs.Request.Complete メソッドを呼び出して便利なメソッドを呼び出す、PrintTicketCommitCompleted メソッドを呼び出す PrintTicket の更新が正常に完了したらとそのアプリを閉じます。

    1. それ以外の場合、制約の状況に対処するユーザーに UI を表示します。

ユーザーがクリックした、キャンセルまたは直接印刷の基本設定ウィンドウを閉じ、プリンターの拡張機能は、エラー ログのメッセージ適切な HRESULT 値を含む IPrinterExtensionEventArgs.Request.Cancel を呼び出します。

プリンター拡張のプロセスが終了して前の段落で説明されているように、完了またはキャンセル メソッドを呼び出されませんが、し、印刷システムが自動的にフォールバック Microsoft 提供の UI を使用します。

デバイスの状態情報を取得するにはプリンターの拡張機能は、印刷デバイスを照会するのに Bidi を使用できます。 たとえば、インク状態またはその他のデバイスに関する状態を表示するのにプリンター拡張ことができます、IPrinterExtensionEventArgs.PrinterQueue.SendBidiQuery メソッドを使用デバイスに双方向のクエリを発行します。 OnBidiResponseReceived イベントのイベント ハンドラーを設定し、有効な Bidi クエリと SendBidiQuery メソッドを呼び出すことに関連する 2 段階のプロセスは、双方向の最新の状態を取得します。 次のコード スニペットでは、2 段階の手順を示します。

```csharp
PrinterQueue.OnBidiResponseReceived += new
EventHandler<PrinterQueueEventArgs>(OnBidiResponseReceived);
PrinterQueue.SendBidiQuery("\\Printer.consumables");
```

Bidi 応答が受信したときに、次のイベント ハンドラーが呼び出されます。 このイベント ハンドラーもにモックのインク状態実装では、デバイスが利用できない場合の開発に便利ですがありますに注意してください。 PrinterQueueEventArgs オブジェクトには、HRESULT と Bidi XML 応答の両方が含まれています。 Bidi XML 応答の詳細については、次を参照してください。[双方向の要求および応答スキーマ](https://msdn.microsoft.com/library/windows/desktop/dd183368.aspx)します。

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

### <a name="printer-notifications"></a>プリンターの通知

印刷設定と正確に同じ方法では、プリンターの通知が呼び出されます。 OnDriverEvent ハンドラーで IPrinterExtensionEventArgs では、ReasonID DriverEvents GUID と一致している場合、構築できますこのイベントを処理するために、エクスペリエンス。

[PrinterExtensionSample](https://go.microsoft.com/fwlink/p/?LinkId=617945)プロジェクトに、通知エクスペリエンスをプリンターの機能を示していませんが、次の変数は、この処理に最も役立ちます。

- PrinterExtensionEventArgs.BidiNotification – これは実行をトリガーするイベントの原因となった Bidi XML です。

- PrinterExtensionEventArgs.DetailedReasonId – eventID ドライバー イベントの xml ファイルからの GUID が含まれます。

通知の IPrinterExtensionEventArgs オブジェクトの最も重要な属性は、BidiNotification プロパティです。 これは実行をトリガーするイベントの原因となった Bidi XML です。 Bidi XML 応答の詳細については、次を参照してください。[双方向の要求および応答スキーマ](https://msdn.microsoft.com/library/windows/desktop/dd183368.aspx)します。

### <a name="managing-printers"></a>プリンターの管理

プリンター拡張のプリンターの管理/管理のハブとして使用できるアプリとしての役割をサポートするために、現在のプリンター拡張機能で登録された印刷キューを列挙し、各キューの状態を取得することができます。 これは、PrinterExtensionSample プロジェクトでは実践しませんが、イベント ハンドラーを登録する App.xaml.cs の Main メソッドに次のコード スニペットを追加する可能性があります。

```csharp
mgr.OnPrinterQueuesEnumerated += new EventHandler<PrinterQueuesEnumeratedEventArgs>(mgr_OnPrinterQueuesEnumerated);
```

キューが列挙されますとイベント ハンドラーが呼び出されますの状態の操作を実行することができます。 このイベントは、場合でも、ユーザーは、開かれた後、複数のキューがインストールに列挙された印刷キューの一覧が最新であることを確認するには、アプリの有効期間中に定期的に発生します。 その結果、これがイベント ハンドラーが実行されるたびに、これが次のコード スニペットで示すように、新しいウィンドウを作成できませんが重要です。

```csharp
static void mgr_OnPrinterQueuesEnumerated(object sender, PrinterQueuesEnumeratedEventArgs e)
{
    foreach (IPrinterExtensionContext pContext in e)
    {
        // show status
    }
}
```

プリンターの拡張機能を使用してメンテナンス タスクを実行するにはお勧めする WritePrinter API を使用して、次の擬似コードの説明に従って、従来します。

```Pseudocode
OpenPrinter
    StartDocPrinter
        StartPagePrinter
          WritePrinter
        EndPagePrinter
    EndDocPrinter
ClosePrinter
```

これらのレガシ Api を .NET にマーシャ リングする方法の詳細については、次を参照してください。 [Visual を使用して、プリンターに生データを送信する方法C#.NET](http://support.microsoft.com/?kbid=322091)または[Visual Basic .NET を使用して、プリンターに生データを送信する方法](http://support.microsoft.com/?kbid=322090)します。

## <a name="printer-extension-performance-best-practices"></a>プリンター拡張機能のパフォーマンスに関するベスト プラクティス

最適なユーザー エクスペリエンスを確保するためにロードをできるだけ高速にプリンターの拡張機能を設計する必要があります。 プリンター拡張機能のサンプル プロジェクトは、実行時にネイティブ プロセッサ アーキテクチャに適した形式にコンパイルする必要がありますを中間言語 (IL) に構築されたを取得するには、.NET アプリケーションです。 インストール中には、ネイティブ システム アーキテクチャ、アプリがコンパイルされていることを確認するベスト プラクティスに従って、プリンターの拡張機能がインストールされていることをお勧めします。 コードのコンパイルとインストールのベスト プラクティスの詳細については、次を参照してください。 [、デスクトップ アプリケーションの起動パフォーマンスの向上](http://blogs.msdn.com/b/dotnet/archive/2012/03/20/improving-launch-performance-for-your-desktop-applications.aspx)します。

Microsoft では、プリンターの拡張機能が、EnableEvents メソッドが呼び出された後までのリソースの読み込みなどの初期化タスクを延期することもお勧めします。 これには、プリンターの拡張機能の 5 秒のタイムアウトの前に EnableEvents を呼び出し、アプリが発生する可能性が最小限に抑えます。

OnDriverEvent の呼び出しの後のプリンター拡張は、UI を初期化し、応答性を確保できますが、非同期メソッドの使用を可能な限り迅速に描画する必要があります。 プリンターの拡張機能はないはずの依存関係ネットワーク呼び出しでまたは双方向のウィンドウの初期状態を作成するには印刷設定やプリンターの通知。

ユーザーが行ったよう PrintTicket、プリンターの拡張機能に影響を与える UI で行う必要がありますに画面を使用して選択が IPrintSchemaTicket::ValidateAsync メソッドのできるだけ早い段階で変更を検証するために使用します。 最後に、プリンターの拡張機能を使用する必要があります、 [ **IPrintSchemaTicket::CommitAsync** ](https://msdn.microsoft.com/library/windows/hardware/hh451382) PrintTicket の変更をコミットするためにメソッド。

プリンターの拡張機能は常に実行のプロセスからのプロセスでは、それらを起動します。 プリンターの拡張機能を開発しているときにに注意してください ウィンドウの動作を維持する必要があります。

- **WindowParent**プロパティから[ **IPrinterExtensionEventArgs** ](https://msdn.microsoft.com/library/windows/hardware/hh973207)アプリを起動するウィンドウ ハンドルを指定します。
- **WindowModal**プロパティから[ **IPrinterExtensionEventArgs** ](https://msdn.microsoft.com/library/windows/hardware/hh973207) (印刷設定モード) では、プリンターの拡張機能がモーダルで実行するかどうかを指定します。

プリンター拡張機能のサンプルでは、一般に、最上位ウィンドウとして起動される UI を作成する方法を示します。 ただし、場合によっては、UI は表示されません、別の整合性レベルで呼び出される UI を原因となったプロセスが実行されている場合や、異なるプロセッサ アーキテクチャのプロセスがコンパイルされたときなど、フォア グラウンドで。 この場合、プリンターの拡張機能では、タスク バーにアイコンが点滅して、フォア グラウンドにユーザーの許可を要求する FlashWindowEx を呼び出す必要があります。

## <a name="related-topics"></a>関連トピック

[双方向の要求および応答スキーマ](https://msdn.microsoft.com/library/windows/desktop/dd183368.aspx)

[データ バインディングの概要](https://msdn.microsoft.com/library/ms752347.aspx)

[Visual Basic .NET を使用して、プリンターに生データを送信する方法](http://support.microsoft.com/?kbid=322090)

[ビジュアルを使用してプリンターに生データを送信する方法C#.NET](http://support.microsoft.com/?kbid=322091)

[デスクトップ アプリケーションの起動時のパフォーマンスを向上](http://blogs.msdn.com/b/dotnet/archive/2012/03/20/improving-launch-performance-for-your-desktop-applications.aspx)

[ネイティブ イメージ ジェネレーター](https://msdn.microsoft.com/library/6t9t5wcf.aspx)

[印刷スキーマ インターフェイス](https://msdn.microsoft.com/library/windows/hardware/hh464019)

[プリンター拡張機能のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617945)

[Windows パフォーマンス分析ツール](https://msdn.microsoft.com/performance/cc825801.aspx)
