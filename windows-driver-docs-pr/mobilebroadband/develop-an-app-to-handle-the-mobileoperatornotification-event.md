---
title: MobileOperatorNotification イベントを処理するアプリを開発する
description: MobileOperatorNotification イベントを処理するアプリを開発する
ms.assetid: 3c483888-8ec4-4270-af3e-ef1efc995171
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e778c54a6077bb306f1b0b2ec6dfe29b93296a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380286"
---
# <a name="develop-an-app-to-handle-the-mobileoperatornotification-event"></a>MobileOperatorNotification イベントを処理するアプリを開発する


このトピックでは、処理するモバイル ブロード バンド アプリを開発する方法を説明します、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント。

-   [ベスト プラクティス](#bp)

-   [手順 1: バック グラウンド タスク コントラクトの宣言](#stepone)

-   [手順 2:バック グラウンド タスク ハンドラー](#steptwo)

-   [手順 3:アクティブ化イベントを処理します。](#stepthree)

-   [手順 4:バック グラウンド タスクの完了ハンドラーを処理します。](#stepfour)

-   [トラブルシューティング](#ts)

-   [Backgroundtask.js ファイルのサンプル](#samp)

## <a name="span-idbpspanspan-idbpspanbest-practices"></a><span id="bp"></span><span id="BP"></span>ベスト プラクティス


バック グラウンド イベントの処理のためには、次のベスト プラクティスを使用してください。

-   アクションを実行することはできません、バック グラウンド イベントを登録しないでください。 これらのイベントを処理と、アプリのクォータを不必要に消費されます。

-   バック グラウンド イベントの受信時に、大量の処理を実行しません。

-   [次へ] の時刻に、アプリの処理を遅延させることが起動されることを検討してください。

-   トースト通知の表示、バック グラウンド イベントへの応答でのタイルを更新してください。 モバイル ブロード バンド アプリでは、バック グラウンド イベントのペイロードを処理できます。

バック グラウンド タスクの詳細については、次を参照してください。[バック グラウンド タスクの概要](https://go.microsoft.com/fwlink/p/?linkid=313924)します。

## <a name="span-idsteponespanspan-idsteponespanstep-1-background-task-contract-declaration"></a><span id="stepone"></span><span id="STEPONE"></span>手順 1:バック グラウンド タスク コントラクトの宣言


Windows モバイル ブロード バンド アプリによって提供されるバック グラウンド タスクのエクスペリエンスを認識するのシステムの機能の拡張機能が提供しているアプリを宣言しなければなりません。

Visual Studio プロジェクトの package.appxmanifest ファイルで宣言するには、次の手順に従います。

**バック グラウンド タスク コントラクトを宣言するには**

1.  **ソリューション エクスプ ローラー**プロジェクトの package.appxmanifest ファイルをダブルクリックします。

2.  **宣言** タブから**使用可能な宣言**を選択します**バック グラウンド タスク**順にクリックします**追加**します。

3.  で、**プロパティ**見出しで、次のアプリ情報を入力してください。

    -   **スタート ページ**ボックス**アプリ設定**、JavaScript と HTML を使用するモバイル ブロード バンド アプリ、アプリでバック グラウンド タスクを処理するファイル名を入力します (たとえば、 **backgroundtask.js**)。

    -   下、**タスクの種類がサポートされている**見出しで、をクリックして、**システム イベント**チェック ボックスをオンします。

これが正しく行われる、package.appxmanifest ファイルで、次のような拡張要素が必要です。

``` syntax
<Extension Category="windows.backgroundTasks" StartPage="backgroundtask.js">
  <BackgroundTasks>
    <Task Type="systemEvent" />
  </BackgroundTasks>
</Extension>
```

## <a name="span-idsteptwospanspan-idsteptwospanstep-2-background-task-handler"></a><span id="steptwo"></span><span id="STEPTWO"></span>手順 2:バック グラウンド タスク ハンドラー


アプリが通知を携帯電話会社に提供する場合、宣言、バック グラウンド タスクのアクティブ化のハンドラーを指定する必要があります。 ハンドラーが携帯電話会社ネットワーク アカウント ID とイベント データを取得[ **Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails**](https://msdn.microsoft.com/library/windows/apps/br207377)します。

バック グラウンド タスクでサポートされている唯一の UI である**トースト**、バック グラウンドのタスク ハンドラーがトーストを表示または保存[ **NetworkOperatorNotificationEventDetails** ](https://msdn.microsoft.com/library/windows/apps/br207377)にローカル ストレージ。

次のコード例では、新しい管理 SMS 通知を受信したときに実行するように設計されたバック グラウンド タスクを示します。

**C#**

``` syntax
using Windows.Networking.NetworkOperators;

namespace MNOMessageBackground
{
    public sealed class MNOBackgroundTask : IBackgroundTask
    {
       public void Run(Windows.ApplicationModel.Background.IBackgroundTaskInstance taskInstance)
       {
         NetworkOperatorNotificationEventDetails notifyData = (NetworkOperatorNotificationEventDetails)taskInstance.TriggerDetails;

         //The network account ID is stored in notifyData.NetworkAccountId

            switch (notifyData.NotificationType)
            {
                case NetworkOperatorEventMessageType.Gsm: // 0
                    break;
                case NetworkOperatorEventMessageType.Cdma: // 1
                    break;
                case NetworkOperatorEventMessageType.Ussd: // 2
                    break;
                case NetworkOperatorEventMessageType.DataPlanThresholdReached: // 3
                    break;
                case NetworkOperatorEventMessageType.DataPlanReset: //4 
                    break;
                case NetworkOperatorEventMessageType.DataPlanDeleted: //5
                    break;
                case NetworkOperatorEventMessageType.ProfileConnected: //6
                    break;
                case NetworkOperatorEventMessageType.ProfileDisconnected: //7
                    break;
                case NetworkOperatorEventMessageType.RegisteredRoaming: //8
                    break;
                case NetworkOperatorEventMessageType.RegisteredHome: ///9
                    break;
                case NetworkOperatorEventMessageType.TetheringEntitlementCheck: //10
                    break;

                default:
                    break;
             }

            // Add code to save the message to app local storage, and optionally show toast notification and tile updates.
        }
    }
}
```

**JavaScript**

``` syntax
(function () {
    "use strict";

    //
    // The background task instance's activation parameters are available via
    // Windows.UI.WebUI.WebUIBackgroundTaskInstance.current.
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current,
        networkOperatorEventType = Windows.Networking.NetworkOperators.NetworkOperatorEventMessageType,
        key = null,
        settings = Windows.Storage.ApplicationData.current.localSettings;

    try {

        
        var details = backgroundTaskInstance.triggerDetails;

// The network account ID is stored in details.networkAccountId.

        switch (details.notificationType) {
            case networkOperatorEventType.gsm:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.cdma:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.ussd:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.dataPlanThresholdReached:
                showToast("Mobile Broadband message", "Data plan threshold reached");
                break;
            case networkOperatorEventType.dataPlanReset:
                showToast("Mobile Broadband message", "Data plan reset");
                break;
            case networkOperatorEventType.dataPlanDeleted:
                showToast("Mobile Broadband message", "Data plan deleted");
                break;
            case networkOperatorEventType.profileConnected:
                showToast("Mobile Broadband message", "Profile connected");
                break;
            case networkOperatorEventType.profileDisconnected:
                showToast("Mobile Broadband message", "Profile disconnected");
                break;
            case networkOperatorEventType.registeredRoaming:
                showToast("Mobile Broadband message", "Registered roaming");
                break;
            case networkOperatorEventType.registeredHome:
                showToast("Mobile Broadband message", "Registered home");
                break;
            case networkOperatorEventType.tetheringEntitlementCheck:
                showToast("Mobile Broadband message", "Entitlement check completed");
                break;
            default:
                showToast("Mobile Broadband message", "Unknown message");
                break;
        }

        //
        // A JavaScript background task must call close when it is done.
        //
 close();
    }
    catch (exception) {
// Display error message.
close();
    }
```

### <a name="span-idshowtileandtoastnotificationsspanspan-idshowtileandtoastnotificationsspanspan-idshowtileandtoastnotificationsspanshow-tile-and-toast-notifications"></a><span id="Show_tile_and_toast_notifications"></span><span id="show_tile_and_toast_notifications"></span><span id="SHOW_TILE_AND_TOAST_NOTIFICATIONS"></span>タイルとトースト通知を表示します。

トーストの両方を表示し、ユーザーが一時的な性質のトースト通知を見逃すために、モバイル ブロード バンド アプリでタイル通知することをお勧めします。 トースト通知とタイルの更新プログラムのエクスペリエンスのデザイン ガイドラインを参照してください[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)します。

**トースト通知を有効にするには**

1.  **ソリューション エクスプ ローラー**プロジェクトの package.appxmanifest ファイルをダブルクリックします。

2.  **アプリケーション UI** ] タブの [、**通知**見出しで、設定**トースト対応**に**はい**します。

これが正しく行われる、package.appxmanifest ファイルで、次のような拡張要素が必要です。

``` syntax
<VisualElements … ToastCapable="true"… />
```

次のコードは、バック グラウンド タスクを識別するハンドルでトースト通知を表示する方法を示しています。

**JavaScript**

``` syntax
function showToast(title, body) {
        var notifications = Windows.UI.Notifications;
        var toastNotificationManager = Windows.UI.Notifications.ToastNotificationManager;
        var toastXml = toastNotificationManager.getTemplateContent(notifications.ToastTemplateType.toastText02);

        var temp = "the parameter will pass to app when app activated from tap Toast ";
        toastXml.selectSingleNode("/toast").setAttribute("launch", temp);

        var textNodes = toastXml.getElementsByTagName("text");
        textNodes[0].appendChild(toastXml.createTextNode(title));
        textNodes[1].appendChild(toastXml.createTextNode(body));

        var toast = new notifications.ToastNotification(toastXml);
        toastNotificationManager.createToastNotifier().show(toast);
    }
```

### <a name="span-idgetsmstextmessagespanspan-idgetsmstextmessagespanspan-idgetsmstextmessagespanget-sms-text-message"></a><span id="Get_SMS_text_message"></span><span id="get_sms_text_message"></span><span id="GET_SMS_TEXT_MESSAGE"></span>SMS テキスト メッセージを取得します。

バック グラウンド タスクは受信 SMS メッセージによってトリガーされました、バック グラウンド タスクの詳細は、ペイロードで SMS オブジェクトを実行します。

**JavaScript**

``` syntax
(function () {
    "use strict";

    //
    // The background task instance's activation parameters are available via
    // Windows.UI.WebUI.WebUIBackgroundTaskInstance.current.
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current,

    try {
        
        var details = backgroundTaskInstance.triggerDetails;
        if (details.notificationType === networkOperatorEventType.gsm
        || details.notificationType === networkOperatorEventType.cdma)
        {
     var textMessage = new Windows.Devices.Sms.SmsTextMessage.fromBinaryMessage(details.smsMessage);
            
         // textMessage can be used to get other SmsMessage properties    
         // like sender number, timestamp, message part count etc.
         showToast("From: " + textMessage.from + "; TimeStamp: " + textMessage.timestamp, details.message);
        }
```

### <a name="span-iduselocalstoragespanspan-iduselocalstoragespanspan-iduselocalstoragespanuse-local-storage"></a><span id="Use_local_storage"></span><span id="use_local_storage"></span><span id="USE_LOCAL_STORAGE"></span>ローカル ストレージを使用します。

バック グラウンド タスクは、ローカル ストレージを使用して、アプリは、後でその情報を使用できるように、バック グラウンド イベントから取得したメッセージを保存します。

**JavaScript**

``` syntax
    //
    // Save the message 
    //
    var settings = Windows.Storage.ApplicationData.current.localSettings;
    var keyMessage = "BA5857FA-DE2C-4A4A-BEF2-49D8B4130A39";


    //
    // The background task instance's activation parameters are available via
    // Windows.UI.WebUI.WebUIBackgroundTaskInstance.current
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current;

    var details = backgroundTaskInstance.triggerDetails;
    settings.values[keyMessage] = details.message;
```

次のコードでは、アプリでバック グラウンド タスク ハンドラーによって格納されたメッセージを取得する方法を示します。

**JavaScript**

``` syntax
var settings = Windows.Storage.ApplicationData.current.localSettings;
    var keyMessage = "BA5857FA-DE2C-4A4A-BEF2-49D8B4130A39";
    var operatorMessage = settings.values[keyMessage];
```

## <a name="span-idstepthreespanspan-idstepthreespanstep-3-handle-the-activation-event"></a><span id="stepthree"></span><span id="STEPTHREE"></span>手順 3:アクティブ化イベントを処理します。


使用してアプリに渡される場合は、トーストでは、パラメーターを設定、 **detail.arguments**します。

JavaScript でまたはC#、処理する、 [ **WinJS.Application.onactivated** ](https://msdn.microsoft.com/library/windows/apps/br212679)イベント、し、イベント ハンドラーに渡されるイベント引数を確認します。 トーストからのアクティブ化は、型のイベント引数を渡し[ **Windows.UI.WebUI.WebUILaunchActivatedEventArgs**](https://msdn.microsoft.com/library/windows/apps/hh701841)します。 場合、イベント引数の**detail.kind**プロパティは[ **Windows.ApplicationModel.Activation.ctivationKind**](https://msdn.microsoft.com/library/windows/apps/br224693).**起動**、アプリ提供開始エクスペリエンスまたは通知を受け取ったかどうかに応じて、イベント引数の**detail.argument**プロパティに設定されて**null**.

**JavaScript**

``` syntax
WinJS.Application.addEventListener("activated", activated; false);

function activated(eventArgs)
{
  if (eventArgs.detail.kind == Windows.ApplicationModel.Activation.ActivationKind.launch)
  {
    if (!eventArgs.detail.arguments)
    {
      // Initialize logic for the Start experience here.
    }
    else
    {
      // Initialize logic for the Notification experience here.
    }
  }
}
```

## <a name="span-idstepfourspanspan-idstepfourspanstep-4-handle-background-task-completion-handlers"></a><span id="stepfour"></span><span id="STEPFOUR"></span>手順 4:バック グラウンド タスクの完了ハンドラーを処理します。


フォア グラウンド アプリでは、バック グラウンド タスクが完了したときに通知する完了ハンドラーも登録できます。 完了状態またはで発生した例外はすべて、**実行**バック グラウンド タスクのメソッドは、フォア グラウンド アプリの完了ハンドラーに渡されます。 タスクが完了したときに、アプリが中断されていた場合は、次回アプリを再開したときに完了の通知を受け取ります。 アプリ内の場合、 **Terminated**状態では、完了の通知を受信しません。 戻るとき、アプリが読み取ることができるファイルなどの状態マネージャーまたは別の手段を使用して情報を保持する必要がありますをバック グラウンド タスクが正常に実行された情報を保持する必要がある場合、**を実行している**状態。

**重要な**  アプリが引き続きバック グラウンドの完了または進行状況のハンドラーを登録するには少なくとも 1 つの時間を実行する必要が、通信事業者のバック グラウンド イベントがシステムによって、アプリに自動的に登録します。

 

**C#**

``` syntax
foreach (var cur in BackgroundTaskRegistration.AllTasks)
{
   if(cur.Value.Name == “MobileOperatorNotificationHandler”)
   {
       cur.Value.Progress += new BackgroundTaskProgressEventHandler(OnProgress);
       cur.Value.Completed += new BackgroundTaskCompletedEventHandler(OnCompleted);
   }
}

//
// Handle background task completion.
private void OnCompleted(IBackgroundTaskRegistration sender, BackgroundTaskCompletedEventArgs e)
{
   var taskCompletion = task as IBackgroundTaskRegistration;
   var completionArgs = args.Context as BackgroundTaskCompletedEventArgs;
   
  //
  // If the background task threw an exception, display the exception in the error text box.
  if (completionArgs.Status != null)
  {
    throw completionArgs.Status;
  }
}

// Handle background task progress.
private void OnProgress(IBackgroundTaskRegistration sender, BackgroundTaskProgressEventArgs e)
{
  var taskRegistration = task as IBackgroundTaskRegistration;
  var progressArgs = args.Context as BackgroundTaskProgressEventArgs;
  // progressArgs.Progress has the progress percentage
}
```

**JavaScript**

``` syntax
var iter = Windows.ApplicationModel.Background.BackgroundTaskRegistration.allTasks.first();
var hascur = iter.hasCurrent;
while (hascur) {
    var cur = iter.current.value;
    if (cur.name === “MobileOperatorNotificationHandler”) {
        cur.addEventListener("progress", new ProgressHandler(cur).onProgress);
        cur.addEventListener("completed", new CompleteHandler(cur).onCompleted);
    }
    hascur = iter.moveNext();
}

//
// Handle background task progress.
//
function ProgressHandler(task) {
    this.onProgress = function (args) {
       try {
           var progress = "Progress: " + args.progress + "%";
       } catch (ex) {
           displayError(ex);
       }
   };
}

//
// Handle background task completion.
//
function CompleteHandler(task) {
    this.onCompleted = function (args) {
        try {
            var key = task.taskId;
        } catch (ex) {
            displayError(ex);
        }
    };
}
```

## <a name="span-idtsspanspan-idtsspantroubleshooting"></a><span id="ts"></span><span id="TS"></span>トラブルシューティング


出てくる可能性のある問題をトラブルシューティングするのにには、これらのセクションを使用します。

### <a name="span-idtriggermetadataparsingtoregisterbackgroundtasksspanspan-idtriggermetadataparsingtoregisterbackgroundtasksspanspan-idtriggermetadataparsingtoregisterbackgroundtasksspantrigger-metadata-parsing-to-register-background-tasks"></a><span id="Trigger_metadata_parsing_to_register_background_tasks"></span><span id="trigger_metadata_parsing_to_register_background_tasks"></span><span id="TRIGGER_METADATA_PARSING_TO_REGISTER_BACKGROUND_TASKS"></span>バック グラウンド タスクを登録する解析トリガー メタデータ

ユーザーは、モバイル ブロード バンド デバイスが接続されているときに Windows 8、Windows 8.1、および Windows 10 自動的にインストール、モバイル ブロード バンドのアプリと関連付けられているサービスのメタデータとレジスタ バック グラウンド タスク、サービス メタデータで定義されています。 ただし、Windows 8.1 で、アプリが自動的にピン留めされていないスタート画面にします。

開発者は、手動でサービス メタデータを解析し、キーを押して、バック グラウンド タスクを登録するには、Windows 8、Windows 8.1、および Windows 10 をトリガーできる、 **F5**キー (または右クリックし、選択**更新**)、で**デバイスとプリンター**デスクトップ上のウィンドウ。 サービス メタデータの解析をバック グラウンド タスクの登録は、アプリが展開されている場合にのみ成功します。

### <a name="span-idverifythatbackgroundtasksarecorrectlyregisteredspanspan-idverifythatbackgroundtasksarecorrectlyregisteredspanspan-idverifythatbackgroundtasksarecorrectlyregisteredspanverify-that-background-tasks-are-correctly-registered"></a><span id="Verify_that_background_tasks_are_correctly_registered_"></span><span id="verify_that_background_tasks_are_correctly_registered_"></span><span id="VERIFY_THAT_BACKGROUND_TASKS_ARE_CORRECTLY_REGISTERED_"></span>バック グラウンド タスクが正しく登録されていることを確認します。

開発者は、デバイス セットアップ マネージャー (DSM) が正しく解析サービス メタデータ、イベント ログを表示することによって確認できます**アプリケーションとサービス ログ\\Microsoft\\Windows\\DeviceSetupManager**します。

1.  イベント ビューアーを開きます。

2.  **メニュー** ] タブで [**ビュー**、] をクリックし、 **[分析およびデバッグ ログ**。

3.  参照する**Applications and Services Logs\\Microsoft\\Windows\\DeviceSetupManager**します。

関心のあるイベントは、DSM でのバック グラウンド タスクが正常に登録されたことを示すイベント ID が 220、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント、およびメタデータ内にあるすべてのエラーを示すイベント ID 7900パッケージです。

### <a name="span-idverifythatprovisioningmetadataissuccessfullyappliedspanspan-idverifythatprovisioningmetadataissuccessfullyappliedspanspan-idverifythatprovisioningmetadataissuccessfullyappliedspanverify-that-provisioning-metadata-is-successfully-applied"></a><span id="Verify_that_provisioning_metadata_is_successfully_applied"></span><span id="verify_that_provisioning_metadata_is_successfully_applied"></span><span id="VERIFY_THAT_PROVISIONING_METADATA_IS_SUCCESSFULLY_APPLIED"></span>プロビジョニングのメタデータが正しく適用されていることを確認します。

ときに適用する、メタデータをプロビジョニングすることを確認します[ **ProvisionFromXmlDocumentResults.AllElementsProvisioned** ](https://msdn.microsoft.com/library/windows/apps/br212047)は true。 それ以外の場合は、エラーの詳細については ProvisionResultsXml を確認してください。 モバイル ブロード バンドの一般的なエラーを以下に示します。

-   PC で SIM とプロビジョニング ファイルの不一致 (プロファイルがエラーで失敗\_いない\_が見つかりました)。

-   プロビジョニング ファイルで CarrierId とエクスペリエンスのメタデータでサービスの数が一致しません。

### <a name="span-idverifythatbackgroundtasksarebeingrunbythesystemeventbrokerspanspan-idverifythatbackgroundtasksarebeingrunbythesystemeventbrokerspanspan-idverifythatbackgroundtasksarebeingrunbythesystemeventbrokerspanverify-that-background-tasks-are-being-run-by-the-system-event-broker"></a><span id="Verify_that_background_tasks_are_being_run_by_the_System_Event_Broker"></span><span id="verify_that_background_tasks_are_being_run_by_the_system_event_broker"></span><span id="VERIFY_THAT_BACKGROUND_TASKS_ARE_BEING_RUN_BY_THE_SYSTEM_EVENT_BROKER"></span>バック グラウンド タスクをシステム イベント ブローカーによって実行されていることを確認します。

Windows が生成することを確認することができます、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベントとイベント ビューアーのチェックして、アプリのバック グラウンド タスクがイベント ブローカーによって実行されていること。 これらのイベントのログ記録は既定で無効と、次の手順を実行することによって有効にすることができます。

1.  イベント ビューアーを開きます。

2.  **メニュー** ] タブで [**ビュー**、] をクリックし、 **[分析およびデバッグ ログ**。

3.  参照する**Applications and Services Logs\\Microsoft\\Windows\\BackgroundTaskInfrastructure**します。

4.  右クリック**診断ログ**選択**ログの有効化**します。

バック グラウンド タスクが正常に実行結果のイベント ログを有効にすると、**イベント ID = 1**を持つ次の説明。"エントリ ポイントでバック グラウンド タスクのインスタンス&lt;バック グラウンド\_タスク\_名前空間\_名前&gt;.&lt;バック グラウンド\_タスク\_クラス\_名前&gt;、名 MobileOperatorNotificationHandler はセッション 1 で作成されておりの ID が与え{11111111-1111-1111-1111-111111111111}"。

バック グラウンド タスクが実行されていない場合は、まず、サービス メタデータで指定されているバック グラウンド タスクの名前に、パッケージの AppXManifest.xml ファイルの名前が一致する確認します。 アプリをデプロイした後、サービス メタデータを解析がトリガーされ、モバイル ブロード バンド デバイスを挿入することを確認します。

### <a name="span-idverifythatwindowsreceivessmsandussdnotificationsspanspan-idverifythatwindowsreceivessmsandussdnotificationsspanspan-idverifythatwindowsreceivessmsandussdnotificationsspanverify-that-windows-receives-sms-and-ussd-notifications"></a><span id="Verify_that_Windows_receives_SMS_and_USSD_notifications"></span><span id="verify_that_windows_receives_sms_and_ussd_notifications"></span><span id="VERIFY_THAT_WINDOWS_RECEIVES_SMS_AND_USSD_NOTIFICATIONS"></span>Windows が SMS、USSD の通知を受信することを確認します。

Windows がイベント ビューアーで SmsRouter イベントをチェックして SMS、USSD の通知を受信しているを確認することができます。

イベント ビューアーで、**アプリケーションとサービス ログ\\Microsoft\\Windows\\モバイル ブロード バンド エクスペリエンス SmsRouter\\Microsoft-Windows-SMSRouter**エントリには「受信した SMS オペレーターへの通知メッセージを SMSRouter」や「、SMSRouter では、テキスト メッセージを受信した」など **アプリケーションとサービス ログ\\Microsoft\\Windows\\モバイル ブロード バンド エクスペリエンス SmsApi\\SMSApi**などのエントリを"アプリ。Microsoft.SDKSamples.SmsSendReceive モバイル ブロード バンド デバイスで SMS テキスト メッセージを送信する: {11111111-1111-1111-1111-111111111111}"。

### <a name="span-idreceivedsmsmessagesarenotdetectedasoperatornotificationsspanspan-idreceivedsmsmessagesarenotdetectedasoperatornotificationsspanspan-idreceivedsmsmessagesarenotdetectedasoperatornotificationsspanreceived-sms-messages-are-not-detected-as-operator-notifications"></a><span id="Received_SMS_messages_are_not_detected_as_operator_notifications"></span><span id="received_sms_messages_are_not_detected_as_operator_notifications"></span><span id="RECEIVED_SMS_MESSAGES_ARE_NOT_DETECTED_AS_OPERATOR_NOTIFICATIONS"></span>オペレーターへの通知として受信した SMS メッセージが検出されません。

オペレーターへの通知として受信した SMS が検出されない場合、アカウントのプロビジョニングのメタデータの管理用の SMS 通知のカスタム フィルター規則を確認します。 プロビジョニングのメタデータに関する詳細については、次を参照してください。[アカウント プロビジョニング](account-provisioning.md)します。

具体的には、アカウント プロビジョニングのメタデータは、送信者の電話番号を指定する場合は、数値の書式指定と一致することを受信したメッセージで SMS Api を使用して確認します。 これが正しく一致することを確認するためにパターンを一時的に変更**\[ ^ \] \\*** この送信者からのすべてのメッセージを照合します。

## <a name="span-idsampspanspan-idsampspansample-backgroundtaskjs-file"></a><span id="samp"></span><span id="SAMP"></span>Backgroundtask.js ファイルのサンプル


``` syntax
//
// A JavaScript background task runs a specified JavaScript file.
//
(function () {
    "use strict";

    //
    // The background task instance's activation parameters are available via Windows.UI.WebUI.WebUIBackgroundTaskInstance.current.
    //
    var backgroundTaskInstance = Windows.UI.WebUI.WebUIBackgroundTaskInstance.current,
        networkOperatorEventType = Windows.Networking.NetworkOperators.NetworkOperatorEventMessageType,
        key = null,
        settings = Windows.Storage.ApplicationData.current.localSettings;

    try {       
        var details = backgroundTaskInstance.triggerDetails;

        switch (details.notificationType) {
            case networkOperatorEventType.gsm:
                var textMessage = new Windows.Devices.Sms.SmsTextMessage.fromBinaryMessage(details.smsMessage);
                showToast("Gsm Msg From: " + textMessage.from + "; TimeStamp: " + textMessage.timestamp, details.message);
                
                break;
            case networkOperatorEventType.cdma:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.ussd:
                showToast("Mobile Broadband message", details.message);
                break;
            case networkOperatorEventType.dataPlanThresholdReached:
                showToast("Mobile Broadband message", "Data plan threshold reached");
                break;
            case networkOperatorEventType.dataPlanReset:
                showToast("Mobile Broadband message", "Data plan reset");
                break;
            case networkOperatorEventType.dataPlanDeleted:
                showToast("Mobile Broadband message", "Data plan deleted");
                break;
            case networkOperatorEventType.profileConnected:
                showToast("Mobile Broadband message", "Profile connected");
                break;
            case networkOperatorEventType.profileDisconnected:
                showToast("Mobile Broadband message", "Profile disconnected");
                break;
            case networkOperatorEventType.registeredRoaming:
                showToast("Mobile Broadband message", "Registered roaming");
                break;
            case networkOperatorEventType.registeredHome:
                showToast("Mobile Broadband message", "Registered home");
                break;
            case networkOperatorEventType.tetheringEntitlementCheck:
                showToast("Mobile Broadband message", "Entitlement check completed");
                break;
            default:
                showToast("Mobile Broadband message", "Unknown message");
                break;
        }
        taskSucceeded();
    }
    catch (exception) {
        taskFailed();
    }

    function showToast(title, body) {

        var notifications = Windows.UI.Notifications;
        var toastNotificationManager = Windows.UI.Notifications.ToastNotificationManager;
        var toastXml = toastNotificationManager.getTemplateContent(notifications.ToastTemplateType.toastText02);

        //
        // Pass to app through eventArguments.arguments.
        //
        var temp = "\"Title\"" + ":" + "\"" + title + "\"" + "," + "\"Message\"" + ":" + "\"" + body + "\"";
        if (temp.length > 251) {
            temp = temp.substring(0, 251);
        }
        toastXml.selectSingleNode("/toast").setAttribute("launch", "'{" + temp + "}'");

        var textNodes = toastXml.getElementsByTagName("text");
        textNodes[0].appendChild(toastXml.createTextNode(title));
        textNodes[1].appendChild(toastXml.createTextNode(body));

        var toast = new notifications.ToastNotification(toastXml);
        toastNotificationManager.createToastNotifier().show(toast);        
    }

    //
    // This function is called when the background task is completed successfully.
    //
    function taskSucceeded() {
        //
        // Use the succeeded property to indicate that this background task completed successfully.
        //
        backgroundTaskInstance.succeeded = true;
        backgroundTask.taskInstance.progress = 100;
        console.log("Background " + backgroundTask.taskInstance.task.name + " Completed");

        //
        // Write to localSettings to indicate that this background task completed.
        //
        key = backgroundTaskInstance.task.taskId.toString();
        settings.values[key] = "Completed";

        //
        // A JavaScript background task must call close when it is done.
        //
        close();
    }

    //
    // If the task was canceled or failed, stop the background task.
    //
    function taskFailed() {
        console.log("Background " + backgroundTask.taskInstance.task.name + " Failed");
        backgroundTaskInstance.succeeded = false;

        key = backgroundTaskInstance.task.taskId.toString();
        settings.values[key] = "Failed";

        close();
    }
})();
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Mobile operator notifications とシステム イベントを有効にします。](enabling-mobile-operator-notifications-and-system-events.md)

[作成とインターネットの共有エクスペリエンスの構成](creating-and-configuring-internet-sharing-experiences.md)

 

 






