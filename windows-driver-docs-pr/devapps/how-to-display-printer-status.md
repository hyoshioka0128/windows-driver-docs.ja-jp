---
title: UWP アプリのデバイスのプリンターのステータスを表示する方法
description: このトピックでは、C#プリンターの状態を照会し、表示する方法を示すには、印刷の設定と印刷通知のサンプルのバージョン。
ms.assetid: 91AD1B3B-0D0B-4FB6-8A0F-4943143D8FCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8770e6e44f9433c009bcac80e5b26c2e13d1b76
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350351"
---
# <a name="how-to-display-printer-status-in-a-uwp-device-app"></a>UWP アプリのデバイスのプリンターのステータスを表示する方法


Windows 8.1 では、ユーザーは、UWP デバイス アプリの最新の UI から、プリンターの状態を確認できます。 このトピックでは、C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)プリンターの状態を照会し、表示する方法を示すサンプル。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)使用して、 **InkLevel.xaml**ページ (この例では、インク レベル) ではプリンターの状態を取得し、それを表示する方法を示します。 印刷のヘルパー クラスは、デバイス コンテキスト (IPrinterExtensionContext) を作成し、デバイス クエリの実行に使用されます。 **PrinterHelperClass.cs**ファイルは、 **DeviceAppForPrintersLibrary**プロジェクトで定義されている Api を使用して、 **PrinterExtensionLibrary**プロジェクト。 プリンターの拡張機能ライブラリでは、v4 印刷ドライバーのプリンター拡張機能のインターフェイスにアクセスする便利な手段を提供します。 詳細については、次を参照してください。、[プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)します。

**注**  このトピックで示すコード例に基づいています、C#のバージョン、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル。 このサンプルも JavaScript および C++ で使用できます。 C++ は COM を直接アクセスできるため、C++ のバージョン サンプルにはが含まれていないことコード ライブラリ プロジェクトに注意してください。 コードの最新バージョンを参照するサンプルをダウンロードします。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


開始する前に。

1.  V4 印刷ドライバーを使用して、プリンターをインストールすることを確認します。 詳細については、次を参照してください。[開発 v4 印刷ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=314231)します。
2.  開発用 PC の設定を取得します。 参照してください[Getting started](getting-started.md)については、ツールをダウンロードして開発者アカウントを作成します。
3.  アプリをストアに関連付けます。 このトピックの「[手順 1:UWP デバイスのアプリ作成](step-1--create-a-uwp-device-app.md)についてです。
4.  アプリに関連付けているプリンター用のデバイス メタデータを作成します。 参照してください[手順 2。デバイス メタデータを作成する](step-2--create-device-metadata.md)の詳細についてはします。
5.  使用してアプリを作成している記述しているかどうかはC#または JavaScript を追加、 **PrinterExtensionLibrary**と**DeviceAppForPrintersLibrary** UWP デバイスのアプリ ソリューションにプロジェクト。 これらのプロジェクト内の各を見つけることができます、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプル。
    **注**  のための C++ COM に直接アクセスできる、C アプリの場合は、COM ベースのプリンター デバイス コンテキストを使用する別のライブラリを必要としません。

     

## <a name="span-idstep1findtheprinterspanspan-idstep1findtheprinterspanspan-idstep1findtheprinterspanstep-1-find-the-printer"></a><span id="Step_1__Find_the_printer"></span><span id="step_1__find_the_printer"></span><span id="STEP_1__FIND_THE_PRINTER"></span>手順 1: プリンターを検出します。


デバイス コンテキストを作成する前に、アプリは、プリンターのデバイス ID を特定する必要があります。 これを行うには、サンプルを使用して、 `EnumerateAssociatedPrinters` PC に接続されているすべてのプリンターを検索します。 各プリンターのコンテナーをチェックし、各コンテナーの PackageFamilyName プロパティを比較することによって、アソシエーションを探します。

**注**  下で、アプリに関連付けられているデバイスの場合、System.Devices.AppPackageFamilyName が見つかりません、**パッケージ**Microsoft Visual Studio でのマニフェスト デザイナーのタブ。

 

この例では、`EnumerateAssociatedPrinters`からメソッド、 **InkLevel.xaml.cs**ファイル。

```CSharp
async void EnumerateAssociatedPrinters(object sender, RoutedEventArgs e)
{
    // Reset output text and associated printer array.
    AssociatedPrinters.Items.Clear();
    BidiOutput.Text = "";

    // GUID string for printers.
    string printerInterfaceClass = "{0ecef634-6ef0-472a-8085-5ad023ecbccd}";
    string selector = "System.Devices.InterfaceClassGuid:=\"" + printerInterfaceClass + "\"";

    // By default, FindAllAsync does not return the containerId for the device it queries.
    // We have to add it as an additonal property to retrieve. 
    string containerIdField = "System.Devices.ContainerId";
    string[] propertiesToRetrieve = new string[] { containerIdField };

    // Asynchronously find all printer devices.
    DeviceInformationCollection deviceInfoCollection = await DeviceInformation.FindAllAsync(selector, propertiesToRetrieve);

    // For each printer device returned, check if it is associated with the current app.
    for (int i = 0; i < deviceInfoCollection.Count; i++)
    {
        DeviceInformation deviceInfo = deviceInfoCollection[i];
        FindAssociation(deviceInfo, deviceInfo.Properties[containerIdField].ToString());
    }
}
```

`FindAssociation`によって呼び出されたメソッド`EnumerateAssociatedPrinters`プリンターの現在のアプリケーションに関連付けられたを確認します。 つまり、このメソッドは、アプリの UWP デバイスのアプリを確認します。 アプリとプリンターがローカル コンピューター上のデバイスのメタデータで定義されている場合、この関連付けが存在します。

この例では、`FindAssociation`からメソッド、 **InkLevel.xaml.cs**ファイル。

```CSharp
async void FindAssociation(DeviceInformation deviceInfo, string containerId)
{

    // Specifically telling CreateFromIdAsync to retrieve the AppPackageFamilyName. 
    string packageFamilyName = "System.Devices.AppPackageFamilyName";
    string[] containerPropertiesToGet = new string[] { packageFamilyName };

    // CreateFromIdAsync needs braces on the containerId string.
    string containerIdwithBraces = "{" + containerId + "}";

    // Asynchoronously getting the container information of the printer.
    PnpObject containerInfo = await PnpObject.CreateFromIdAsync(PnpObjectType.DeviceContainer, containerIdwithBraces, containerPropertiesToGet);

    // Printers could be associated with other device apps, only the ones with package family name
    // matching this app's is associated with this app. The packageFamilyName for this app will be found in this app's packagemanifest
    string appPackageFamilyName = "Microsoft.SDKSamples.DeviceAppForPrinters.CS_8wekyb3d8bbwe";
    var prop = containerInfo.Properties;

    // If the packageFamilyName of the printer container matches the one for this app, the printer is associated with this app.
    string[] packageFamilyNameList = (string[])prop[packageFamilyName];
    if (packageFamilyNameList != null)
    {
        for (int j = 0; j < packageFamilyNameList.Length; j++)
        {
            if (packageFamilyNameList[j].Equals(appPackageFamilyName))
            {
                AddToList(deviceInfo);
            }
        }
    }
}
```

アソシエーションが見つかった場合、`FindAssociation`メソッドは、`AddToList`メソッドの一覧にデバイス ID を追加するには、デバイス Id が関連付けられています。 という名前のコンボ ボックスでこれらの Id が格納されている`AssociatedPrinters`します。

この例では、`AddToList`からメソッド、 **InkLevel.xaml.cs**ファイル。

```CSharp
void AddToList(DeviceInformation deviceInfo)
{
    // Creating a new display item so the user sees the friendly name instead of the interfaceId.
    ComboBoxItem item = new ComboBoxItem();
    item.Content = deviceInfo.Properties["System.ItemNameDisplay"] as string;
    item.DataContext = deviceInfo.Id;
    AssociatedPrinters.Items.Add(item);

    // If this is the first printer to be added to the combo box, select it.
    if (AssociatedPrinters.Items.Count == 1)
    {
        AssociatedPrinters.SelectedIndex = 0;
    }
}
```

## <a name="span-idstep2displaythestatusspanspan-idstep2displaythestatusspanspan-idstep2displaythestatusspanstep-2-display-the-status"></a><span id="Step_2__Display_the_status"></span><span id="step_2__display_the_status"></span><span id="STEP_2__DISPLAY_THE_STATUS"></span>手順 2: 状態を表示します。


`GetInkStatus`メソッドは、非同期イベント ベースのパターンで情報を要求するプリンターからを使用します。 このメソッドでは、関連するデバイス ID を使用して、デバイスの状態を取得するために使用するデバイス コンテキストを取得します。 呼び出し、`printHelper.SendInkLevelQuery()`メソッドは、デバイスのクエリを開始します。 応答を返す場合、`OnInkLevelReceived`メソッドが呼び出され、UI が更新されます。

**注**  このC#ため、例が JavaScript のサンプルよりもさまざまなパターンに従いますC#、PrintHelperClass を UI スレッドに戻すには、イベント メッセージを投稿できるように、ディスパッチャーを送信することができます。

 

この例では、`GetInkStatus`と`OnInkLevelReceived`からメソッド、 **InkLevel.xaml.cs**ファイル。

```CSharp
void GetInkStatus(object sender, RoutedEventArgs e)
{
    if (AssociatedPrinters.Items.Count > 0)
    {
        // Get the printer that the user has selected to query.
        ComboBoxItem selectedItem = AssociatedPrinters.SelectedItem as ComboBoxItem;

        // The interfaceId is retrieved from the detail field.
        string interfaceId = selectedItem.DataContext as string;

        try
        {
            // Unsubscribe existing ink level event handler, if any.
            if (printHelper != null)
            {
                printHelper.OnInkLevelReceived -= OnInkLevelReceived;
                printHelper = null;
            }

            object context = Windows.Devices.Printers.Extensions.PrintExtensionContext.FromDeviceId(interfaceId);printHelper.SendInkLevelQuery()

            // Use the PrinterHelperClass to retrieve the bidi data and display it.
            printHelper = new PrintHelperClass(context);
            try
            {
                printHelper.OnInkLevelReceived += OnInkLevelReceived;
                printHelper.SendInkLevelQuery();

                rootPage.NotifyUser("Ink level query successful", NotifyType.StatusMessage);
            }
            catch (Exception)
            {
                rootPage.NotifyUser("Ink level query unsuccessful", NotifyType.ErrorMessage);
            }
        }
        catch (Exception)
        {
            rootPage.NotifyUser("Error retrieving PrinterExtensionContext from InterfaceId", NotifyType.ErrorMessage);
        }
    }
}

private void OnInkLevelReceived(object sender, string response)
{
    BidiOutput.Text = response;
}
```

印刷のヘルパー クラスが Bidi クエリをデバイスに送信して、応答の受信処理します。

この例では、`SendInkLevelQuery`メソッド、およびその他のユーザーから、 **PrintHelperClass.cs**ファイル。 印刷のヘルパー クラスのメソッドの一部のみがここに表示されるに注意してください。 ダウンロード、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルを完全なコードを参照してください。

```CSharp
public void SendInkLevelQuery()
{
    printerQueue.OnBidiResponseReceived += OnBidiResponseReceived;

    // Send the query.
    string queryString = "\\Printer.Consumables";
    printerQueue.SendBidiQuery(queryString);
}

private void OnBidiResponseReceived(object sender, PrinterQueueEventArgs responseArguments)
{
    // Invoke the ink level event with appropriate data.
    dispatcher.RunAsync(
        Windows.UI.Core.CoreDispatcherPriority.Normal,
        () =>
        {
            OnInkLevelReceived(sender, ParseResponse(responseArguments));
        });
}

private string ParseResponse(PrinterQueueEventArgs responseArguments)
{
    if (responseArguments.StatusHResult == (int)HRESULT.S_OK)
        return responseArguments.Response;
    else
        return InvalidHResult(responseArguments.StatusHResult);
}

private string InvalidHResult(int result)
{
    switch (result)
    {
        case unchecked((int)HRESULT.E_INVALIDARG):
            return "Invalid Arguments";
        case unchecked((int)HRESULT.E_OUTOFMEMORY):
            return "Out of Memory";
        case unchecked((int)HRESULT.ERROR_NOT_FOUND):
            return "Not found";
        case (int)HRESULT.S_FALSE:
            return "False";
        case (int)HRESULT.S_PT_NO_CONFLICT:
            return "PT No Conflict";
        default:
            return "Undefined status: 0x" + result.ToString("X");
    }
}
```

## <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>テスト


UWP デバイス アプリをテストする前に、デバイス メタデータを使用して、プリンターにリンクする必要があります。

-   デバイスのアプリ情報を追加するプリンターのデバイス メタデータ パッケージのコピーする必要があります。 使用してビルドできるデバイス メタデータを持っていない場合、**デバイス メタデータの作成ウィザード**、トピックの説明に従って[手順 2。デバイス メタデータ、UWP デバイス アプリを作成](https://go.microsoft.com/fwlink/p/?LinkId=313644)です。

    **注**  を使用する、**デバイス メタデータの作成ウィザード**、Microsoft Visual Studio Professional、Microsoft、Visual Studio Ultimate をインストールする必要がありますまたは[スタンドアロン Windows 8.1 の SDK](https://go.microsoft.com/fwlink/p/?linkid=309209)、このトピックの手順を完了する前にします。 Microsoft Visual Studio Express for Windows をインストールすると、ウィザードが含まれていない SDK のバージョンがインストールされます。

     

次の手順では、アプリをビルドし、デバイスのメタデータをインストールします。

1.  テスト署名を有効にします。
    1.  開始、**デバイス メタデータの作成ウィザード**から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\をダブルクリックして、x86**DeviceMetadataWizard.exe**
    2.  **ツール**メニューの **テスト署名を有効にする**します。

2.  コンピューターを再起動します
3.  ソリューション (.sln) ファイルを開くには、ソリューションをビルドします。 F7 キーを押すか**ビルド -&gt;ソリューションのビルド**サンプルが読み込まれた後は、上部のメニューから。

4.  接続を切断し、プリンターをアンインストールします。 Windows が次に、デバイスが検出されたときに更新済みのデバイス メタデータの読み取りができるように、この手順が必要です。
5.  編集し、デバイスのメタデータを保存します。 デバイス アプリをデバイスにリンクするには、デバイスでデバイス アプリを関連付ける必要があります。
    **注**  デバイスのメタデータをまだ作成していない場合は、次を参照してください。[手順 2。デバイス メタデータ、UWP デバイス アプリを作成](https://go.microsoft.com/fwlink/p/?LinkId=313644)です。

     

    1.  場合、**デバイス メタデータの作成ウィザード**が開くまだ、開始から *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\x86 により、ダブルクリック**DeviceMetadataWizard.exe**します。
    2.  クリックして**デバイス メタデータの編集**します。 これからは、既存のデバイス メタデータ パッケージを編集できます。
    3.  **オープン** ダイアログ ボックスで、UWP デバイス アプリに関連付けられている、デバイス メタデータ パッケージを見つけます。 (これが、 **devicemetadata ms**ファイル拡張子)。
    4.  **指定 UWP デバイスのアプリ情報** ページで、Microsoft Store アプリの情報を入力、 **UWP デバイス アプリ**ボックス。 をクリックして**インポート UWP アプリのマニフェスト ファイル**自動的に入力する、**パッケージ名**、**パブリッシャー名**と**UWP アプリの ID**します。
    5.  場合は、アプリは、プリンターの通知の登録は、入力、**通知ハンドラー**ボックス。 **イベント ID**、印刷イベント ハンドラーの名前を入力します。 **イベント資産**、そのコードが存在するファイルの名前を入力します。

    6.  完了したら、クリックして **[次へ]** に到達するまで、**完了**ページ。
    7.  **デバイス メタデータ パッケージの確認** ページで、すべての設定が正しいことと選択するかどうかを確認、**デバイス メタデータ パッケージをローカル コンピューター上のメタデータ ストアにコピー**チェック ボックスをオンします。 クリックして**保存**します。

6.  デバイスが接続されている場合、その Windows が更新されたデバイスのメタデータを読み取り、プリンターに再接続します。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>トラブルシューティング


### <a name="span-idissuecantfindprinterwhenenumeratingdevicesassociatedwiththeappspanspan-idissuecantfindprinterwhenenumeratingdevicesassociatedwiththeappspanspan-idissuecantfindprinterwhenenumeratingdevicesassociatedwiththeappspanissue-cant-find-printer-when-enumerating-devices-associated-with-the-app"></a><span id="Issue__Can_t_find_printer_when_enumerating_devices_associated_with_the_app"></span><span id="issue__can_t_find_printer_when_enumerating_devices_associated_with_the_app"></span><span id="ISSUE__CAN_T_FIND_PRINTER_WHEN_ENUMERATING_DEVICES_ASSOCIATED_WITH_THE_APP"></span>問題:アプリに関連付けられているデバイスを列挙するときに、プリンターを見つけることができません。

関連付けられているプリンターを列挙するときに、プリンターが見つからない場合は.

-   **考えられる原因:** テスト署名が有効になっていません。 有効にする方法については、このトピックでは、"デバッグ"を参照してください。

-   **考えられる原因:** アプリには、右側のパッケージ ファミリ名のクエリいないいます。 コード内のパッケージ ファミリ名を確認します。 開いて**package.appxmanifest**で Microsoft Visual Studio を確認する、パッケージ ファミリ名のクエリには構造と一致する、**パッケージ** タブのパッケージ ファミリ名のフィールド。

-   **考えられる原因:** デバイス メタデータは、パッケージ ファミリ名に関連付けられています。 使用して、**デバイス メタデータの作成ウィザード**をデバイスのメタデータを開き、パッケージ ファミリ名を確認します。 ウィザードを開始します *%programfiles (x86) %*\\Windows キット\\8.1\\bin\\をダブルクリックして、x86 **DeviceMetadataWizard.exe**します。

### <a name="span-idissuefoundprinterassociatedwiththeappbutcantquerybidiinfospanspan-idissuefoundprinterassociatedwiththeappbutcantquerybidiinfospanspan-idissuefoundprinterassociatedwiththeappbutcantquerybidiinfospanissue-found-printer-associated-with-the-app-but-cant-query-bidi-info"></a><span id="Issue__Found_printer_associated_with_the_app__but_can_t_query_Bidi_info"></span><span id="issue__found_printer_associated_with_the_app__but_can_t_query_bidi_info"></span><span id="ISSUE__FOUND_PRINTER_ASSOCIATED_WITH_THE_APP__BUT_CAN_T_QUERY_BIDI_INFO"></span>問題:見つかったプリンターは、アプリに関連付けられたが、Bidi 情報をクエリすることはできません。

プリンターが見つかった場合はエラーを返します、関連付けられているプリンターが Bidi クエリを列挙するときにしています.

-   **考えられる原因:** 正しくないパッケージ ファミリ名。 コード内のパッケージ ファミリ名を確認します。 開いて**package.appxmanifest**で Visual Studio を確認する、パッケージ ファミリ名のクエリには構造と一致する、**パッケージ** タブのパッケージ ファミリ名のフィールド。

-   **考えられる原因:** V4 プリンターではなく、v3 プリンターを使用してプリンターがインストールされました。 インストールされているバージョンを表示するには、PowerShell を開き、次のコマンドを入力します。

    ```PowerShell
    get-printer | Select Name, {(get-printerdriver -Name $_.DriverName).MajorVersion}
    ```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[プリンター拡張機能インターフェイス (v4 印刷ドライバー)](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[アプリを作成する UWP デバイス (ステップ バイ ステップ ガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスのアプリ (ステップ バイ ステップ ガイド) のデバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 






