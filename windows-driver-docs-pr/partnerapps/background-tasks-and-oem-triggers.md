---
title: バックグラウンド タスクとカスタム トリガー
description: バックグラウンド タスクとカスタム トリガー
ms.assetid: 672d3501-da84-495b-b70e-f07de32aff53
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a34d6920032d824cd151bd55114f9eb1db89ea4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571640"
---
# <a name="background-tasks-and-custom-triggers"></a>バックグラウンド タスクとカスタム トリガー


バック グラウンド タスクは、Windows 10 でコードをバック グラウンドで実行するための 1 つのメソッドです。 標準的なアプリケーション プラットフォームの一部である、基本的に、アプリをシステム イベント (トリガー)、およびコードの定義済みのブロックをバック グラウンドで実行イベントの発生時に登録する機能を提供します。 システムのトリガーには、ネットワーク接続の変更などのイベントまたはシステムのタイム ゾーンが含まれます。

状況によっては、指定されたシステムのトリガーはパートナーのシナリオに対処するのに十分な。 **Windows 10 バージョン 1803 以降**にパートナーの柔軟性を提供して、パートナーは作成し、カスタムのトリガーをバック グラウンド タスクの詳細のような状況での使用を許可して、アプリ登録できます。 カスタムのトリガーでは、デバイス ドライバーに定義されているし、したいハードウェアの状態のイベントを発生させることができます。 カスタムのトリガーが発生したときに、アプリは、標準的なアプリ モデルとまったく同じ方法でバック グラウンド タスクを実行できます。

## <a name="span-idimplementingacustomtriggerspanspan-idimplementingacustomtriggerspanspan-idimplementingacustomtriggerspanimplementing-a-custom-trigger"></a><span id="Implementing_a_custom_trigger"></span><span id="implementing_a_custom_trigger"></span><span id="IMPLEMENTING_A_CUSTOM_TRIGGER"></span>カスタムのトリガーを実装します。


カスタムのトリガーを実装するための 2 つの手順があります。 具体的には、トリガーの定義し、デバイスのドライバーまたはシステムのサービス内で発生する必要があり、バック グラウンド タスクを使用してアプリを作成する必要があります。

### <a name="span-idcreatingthecustomtriggerspanspan-idcreatingthecustomtriggerspanspan-idcreatingthecustomtriggerspancreating-the-custom-trigger"></a><span id="Creating_the_custom_trigger"></span><span id="creating_the_custom_trigger"></span><span id="CREATING_THE_CUSTOM_TRIGGER"></span>カスタムのトリガーを作成します。

カスタムのトリガーが定義され、ネイティブのサービスまたはデバイス ドライバーを通じて内で発生した、 **RtlRaiseCustomSystemEventTrigger**関数。 ユニバーサル アプリからの登録でき、システム定義のトリガーと同じ方法では比較的でバック グラウンド タスクを開始するために使用します。

次のコードの抜粋は、カスタムのトリガーを発生させる方法を示しています。

``` syntax
#define GUID_MY_CUSTOMSYSTEMEVENTTRIGGERID L"{9118718B-FF80-4AFE-BAF1-D88A4525F3AB}"

CUSTOM_SYSTEM_EVENT_TRIGGER_CONFIG triggerConfig;
CUSTOM_SYSTEM_EVENT_TRIGGER_INIT(&triggerConfig,
                                 GUID_MY_CUSTOMSYSTEMEVENTTRIGGERID);

NTSTATUS status = RtlRaiseCustomSystemEventTrigger(&triggerConfig);
```

上記のコード サンプル内で、GUID をパラメーターとして渡す、 **RtlRaiseCustomSystemEventTrigger**関数は、バック グラウンド タスクを作成するときのアプリを登録するトリガーの識別子を定義します。 この識別子は一意である必要があります。

### <a name="span-idcreatingabackgroundtaskspanspan-idcreatingabackgroundtaskspanspan-idcreatingabackgroundtaskspancreating-a-background-task"></a><span id="Creating_a_background_task"></span><span id="creating_a_background_task"></span><span id="CREATING_A_BACKGROUND_TASK"></span>バック グラウンド タスクを作成します。

バック グラウンド タスクを作成して、カスタムのトリガーの登録を行うには、標準のシステムのトリガーを使用するバック グラウンド タスクを使用するプロセスによく似ています。

1.  まず、UWP アプリを作成します。

2.  次の例に示すように、アプリ マニフェスト ファイルでバック グラウンド タスクを定義します。 なお、**型**の属性、**タスク**に設定されている要素 `“systemEvent”`

    ``` syntax
    <Applications>
      <Application Id="MyBackgroundTaskSample.App" Executable="$targetnametoken$.exe" EntryPoint=" MyBackgroundTaskSample.App">
        <Extensions>
          <Extension Category="windows.backgroundTasks" EntryPoint="MyBackgroundTask.SampleBackgroundTask">
            <BackgroundTasks>
              <Task Type="systemEvent" />
            </BackgroundTasks>
          </Extension>
        </Extensions>
      </Application>
    </Applications>
    ```

3.  次のコード例で示すように作成したカスタムのトリガーをリッスンするようにアプリを登録します。 文字列がインスタンス化するときに使用することに注意してください、 **CustomSystemEventTrigger**する必要があります一致を使用するときに、GUID を作成する、トリガー、ネイティブのサービスまたはデバイス ドライバー。

    ``` syntax
    public void InitBackgroundTask()
    {
       // Create a new background task builder.
       BackgroundTaskBuilder taskBuilder = new BackgroundTaskBuilder();

       // Create a new CustomSystemEvent trigger.
       var myTrigger = new CustomSystemEventTrigger(
                            "{9118718B-FF80-4AFE-BAF1-D88A4525F3AB}", //Trigger Identifier
                            CustomSystemEventTriggerRecurrence.Once); //OneShot 

       // Associate the CustomSystemEvent trigger with the background task builder.
       taskBuilder.SetTrigger(myTrigger);

       // Specify the background task to run when the trigger fires.
       taskBuilder.TaskEntryPoint = MyBackgroundTask.SampleBackgroundTask;

       // Name the background task.
       taskBuilder.Name = “fabrikam.audio-jack.connected Task”;

       // Register the background task.
       BackgroundTaskRegistration taskRegistration = taskBuilder.Register();

       // Associate completed event handler with the new background task.
       taskRegistration.Completed += new BackgroundTaskCompletedEventHandler(OnCompleted); 
    }
    ```

4.  次のコード例で示すように、バック グラウンド タスクを作成します。

    ``` syntax
    namespace MyBackgroundTask
    {
       public sealed class SampleBackgroundTask : IBackgroundTask
       {
          // Called by the system when it's time to run our task
          public void Run(IBackgroundTaskInstance instance)
          {
             DoWork();
          }
       }
    }
    ```

詳細なガイダンスについて、作成、構成、およびバック グラウンド タスクとトリガーを使用するを参照してください[クイック スタート。作成し、バック グラウンド タスクを登録](https://msdn.microsoft.com/library/windows/apps/hh977055.aspx)します。

 

 





