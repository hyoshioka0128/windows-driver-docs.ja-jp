---
title: 新しい受信 SMS のバック グラウンド イベントを実行します。
description: 新しい受信 SMS のバック グラウンド イベントを実行します。
ms.assetid: 57534569-3678-4e2c-b55a-7dc6f057fb7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3196d69f70e3e044915a21d30c0bfa076e9e372
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530481"
---
# <a name="run-new-sms-received-background-events"></a>新しい受信 SMS のバック グラウンド イベントを実行します。


モバイル ブロード バンド SMS プラットフォームは、モバイル ネットワーク オペレーターまたは一般的な SMS メッセージからの管理用の SMS 通知がかどうかに応じて、受信した新しい SMS データを別のシステム イベントを提供します。 モバイル ネットワーク オペレーターから受信する新しい管理 SMS 通知をバック グラウンドのシステム イベントでは、モバイル ブロード バンド アプリからアクセスできるのみです。

アプリする必要がありますと、バック グラウンド タスクでの新しい受信 SMS メッセージの読み取りに SMS を使用するユーザーの同意が既に受信します。 アプリでは、バック グラウンド タスクから同意の要求をアプリは、システムの SMS デバイスをトリガーできませんので、最初に、SMS にアクセスしている場合は、バック グラウンド タスクからの新しい受信 SMS メッセージの内容を読み取ることができません。

次のコード例では、新しい SMS メッセージを受信したときに実行するように設計されたバック グラウンド タスクを示します。

**C#バック グラウンド タスクのコード**

``` syntax
namespace SmsBackgroundSample
{
  public sealed class SmsBackgroundTask : IBackgroundTask
  { 
    // The Run method is the entry point of a background task.

    public void Run(IBackgroundTaskInstance taskInstance)
    {
      // Associate a cancellation handler with the background task.

      taskInstance.Canceled += new BackgroundTaskCanceledEventHandler(OnCanceled);

      ManualResetEvent manualEventWaiter = new ManualResetEvent(false);
      manualEventWaiter.Reset();

      // Do the background task activity.

      DisplayToastAsync(taskInstance, manualEventWaiter);

      // Wait until the async operation is done. We need to do this else the background process will exit.
      manualEventWaiter.WaitOne(5000);

            Debug.Print("Background " + taskInstance.Task.Name + (" process ran"));

  }

  async void DisplayToastAsync(IBackgroundTaskInstance taskInstance, ManualResetEvent manualEventWaiter)
  {
    SmsReceivedEventDetails smsDetails = (SmsReceivedEventDetails)taskInstance.TriggerDetails;
    SmsBinaryMessage smsEncodedmsg = (SmsBinaryMessage) smsDetails.BinaryMessageMessage;
    SmsTextMessage smsTextMessage = Windows.Devices.Sms.SmsTextMessage.FromBinaryMessage(smsEncodedmsg);

    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(ToastTemplateType.ToastText02);
    XmlNodeList stringElements = toastXml.GetElementsByTagName("text");

    stringElements.Item(0).AppendChild(toastXml.CreateTextNode(smsTextMessage.From));
    stringElements.Item(1).AppendChild(toastXml.CreateTextNode(smsTextMessage.Body));

    ToastNotification notification = new ToastNotification(toastXml);
    ToastNotificationManager.CreateToastNotifier().Show(notification);

    manualEventWaiter.Set();
  }

}
```

**JavaScript アプリのコードをバック グラウンド タスクを登録するには**

``` syntax
var triggerAway = new Windows.ApplicationModel.Background.SystemTrigger(Windows.ApplicationModel.Background.SystemTriggerType.smsReceived, false);
var builderAway = new Windows.ApplicationModel.Background.BackgroundTaskBuilder();

builderAway.setTrigger(triggerAway);
builderAway.taskEntryPoint = "HelloWorldBackground.BackgroundTask1";
builderAway.name = "Sms";

var taskAway = builderAway.register();
taskAway.addEventListener("progress", new ProgressHandler(taskAway).onProgress);
taskAway.addEventListener("completed", new CompleteHandler(taskAway).onCompleted);
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SMS のアプリの開発](developing-sms-apps.md)

 

 






