---
title: Windows 8.1 でデバイスのバック グラウンド タスクの作成
description: このトピックでは、DeviceUseTrigger または DeviceServicingTrigger を使用してデバイスのバック グラウンド タスクを作成する方法について説明します。
ms.assetid: 34263DB8-BB42-480B-AF7F-CC45772E6E84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f47e173582c5007bb8ac90310926fd19ff49a2d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330668"
---
# <a name="creating-a-device-background-task-in-windows-81-uwp-device-apps"></a>Windows 8.1 (UWP デバイス アプリ) でのデバイスのバック グラウンド タスクの作成


Windows 8.1 では、UWP アプリは、周辺機器のデバイス上のデータを同期できます。 アプリがデバイスのメタデータに関連付けられている場合は、その uwp デバイス ファームウェアの更新プログラムなど、デバイスの更新プログラムも実行できます。 このトピックでは、使用するデバイスのバック グラウンド タスクを作成する方法を説明します、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)または[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)します。 これらのトリガーを使用するデバイスのバック グラウンド エージェントは、同期され更新されているユーザーの同意を確認し、デバイスは、バッテリの寿命を保てるようにするポリシーが適用されます。 デバイスのバック グラウンド タスクの詳細については、次を参照してください。[デバイスとの同期と UWP デバイス アプリ用の更新プログラム](device-sync-and-update-for-uwp-device-apps.md)します。

**注**に対応するこのトピックで、[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )します。 カスタム USB デバイスのサンプルでは、デバイス、DeviceUseTrigger との同期を実行するバック グラウンド タスクを示します。 DeviceServicingTrigger、ファームウェアの更新プログラムを実行するバック グラウンド タスクの例を表示するには、ダウンロード、[ファームウェア更新の USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=309186)します。



デバイスのバック グラウンド タスクでは、[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )DeviceUseTrigger には、このトピックで説明したすべての機能は、DeviceServicingTrigger を使用して、デバイスのバック グラウンド タスクにも適用できます。 2 つのトリガーを使用しての唯一の違いは、Windows によって行われたポリシーのチェックです。

## <a name="span-idtheappmanifestspanspan-idtheappmanifestspanspan-idtheappmanifestspanthe-app-manifest"></a><span id="The_app_manifest"></span><span id="the_app_manifest"></span><span id="THE_APP_MANIFEST"></span>アプリ マニフェスト


デバイスのバック グラウンド タスクを使用するには、アプリはフォア グラウンド アプリのアプリ マニフェスト ファイルで宣言する必要がありますなどがシステムによってトリガーされるバック グラウンド タスクを完了します。 詳細については、次を参照してください。[デバイスとの同期と UWP デバイス アプリ用の更新プログラム](device-sync-and-update-for-uwp-device-apps.md)します。

アプリ パッケージ マニフェスト ファイルからこの例では**DeviceLibrary.SyncContent**はフォア グラウンド アプリから、エントリ ポイントです。 **DeviceLibrary.SyncContent**バック グラウンド タスクを使用するためのエントリ ポイントは、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)します。

```XML
<Extensions>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.SyncContent">
    <BackgroundTasks>
      <m2:Task Type="deviceUse" /> 
    </BackgroundTasks>
  </Extension>
</Extensions>
```

## <a name="span-idthedevicebackgroundtaskspanspan-idthedevicebackgroundtaskspanspan-idthedevicebackgroundtaskspanthe-device-background-task"></a><span id="The_device_background_task"></span><span id="the_device_background_task"></span><span id="THE_DEVICE_BACKGROUND_TASK"></span>デバイスのバック グラウンド タスク


デバイスのバック グラウンド タスク クラス実装、`IBackgroundTask`インターフェイスし、実際のコードいずれかの同期を作成または更新を周辺機器にはが含まれています。 バック グラウンド タスクのクラスは、バック グラウンド タスクがトリガーされたときと、アプリのアプリケーション マニフェストで指定されたエントリ ポイントから実行されます。

デバイスのバック グラウンド クラスで、[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )を使用して USB デバイスに同期を実行するコードを含む、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)バック グラウンド タスク。 詳細については、サンプルをダウンロードします。 実装の詳細については`IBackgroundTask`Windows のバック グラウンド タスクのインフラストラクチャを参照してくださいと[バック グラウンド タスクを使用してアプリをサポートしている](https://go.microsoft.com/fwlink/p/?LinkID=254337)します。

デバイスのバック グラウンド タスクの一部をキー[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )が含まれます。

1.  `IoSyncBackgroundTask`クラスが実装する、 `IBackgroundTask` Windows のバック グラウンド タスクのインフラストラクチャで必要なインターフェイスです。

2.  `IoSyncBackgroundTask`クラスを取得、`DeviceUseDetails`インスタンス内のクラスに渡されます、`IoSyncBackgroundTask`クラスの Run メソッドと進行状況を報告するには、このインスタンスのバックアップ キャンセル イベントを登録して、Microsoft Store アプリを使用します。

3.  `IoSyncBackgroundTask`クラスの Run メソッドは、プライベートも呼び出して`OpenDevice`と`WriteToDeviceAsync`をバック グラウンドのデバイスを実装するメソッドがコードを同期します。

## <a name="span-idtheforegroundappspanspan-idtheforegroundappspanspan-idtheforegroundappspanthe-foreground-app"></a><span id="The_foreground_app"></span><span id="the_foreground_app"></span><span id="THE_FOREGROUND_APP"></span>フォア グラウンド アプリ


フォア グラウンド アプリ、[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )を登録し、使用するデバイスのバック グラウンド タスクをトリガー [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)します。 このセクションでは、フォア グラウンド アプリはトリガーを登録して、デバイスのバック グラウンド タスクの進行状況を処理するための手順の概要を示します。

フォア グラウンド アプリ、[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )デバイスのバック グラウンド タスクを使用して、次の手順を実行します。

1.  新しい[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)と`BackgroundTaskRegistration`オブジェクト。

2.  バック グラウンド タスクがこのアプリが既に登録済みの参照をチェックし、呼び出すことによってキャンセルされ、 [BackgroundTaskRegistration.Unregister](https://go.microsoft.com/fwlink/p/?LinkId=309315)タスクのメソッド。

3.  プライベート`SetupBackgroundTask`メソッドは、デバイスと同期するバック グラウンド タスクを登録します。 `SetupBackgroundTask`メソッドの呼び出し元、`SyncWithDeviceAsync`メソッドで、次の手順。

    1.  初期化します、`DeviceUseTrigger`後で使用し保存します。
    2.  新たに作成`BackgroundTaskBuilder`オブジェクトと、使用してその`Name`、`TaskEntryPoint`と`SetTrigger`プロパティとメソッドをアプリの登録`DeviceUseTrigger`オブジェクトとバック グラウンドのタスク名。 `BackgroundTaskBuilder`オブジェクトの`TaskEntryPoint`プロパティがバック グラウンド タスクがトリガーされたときに実行されるバック グラウンド タスク クラスの完全名に設定します。
    3.  入力候補およびフォア グラウンド アプリがユーザーに入力候補および進行状況の更新を提供できるように、バック グラウンド タスクから進行状況イベントを登録します。

4.  プライベート`SyncWithDeviceAsync`メソッドは、デバイスと同期して、バック グラウンド同期を開始するバック グラウンド タスクを登録します。

    1.  呼び出し、`SetupBackgroundTask`メソッドは、前の手順と、デバイスを同期するバック グラウンド タスクを登録します。
    2.  秘密を呼び出す`StartSyncBackgroundTaskAsync`バック グラウンド タスクを開始するメソッド。 メソッドがバック グラウンド タスクを確実にデバイスにアプリのハンドルを閉じることは、開始時にデバイスを開くことができません。

        **重要な**バック グラウンド タスクをフォア グラウンド アプリが呼び出す前に、デバイスへの接続を閉じる必要がありますので、更新プログラムを実行するデバイスを開く必要があります`RequestAsync`します。




    次に、`StartSyncBackgroundTaskAsync`メソッドの呼び出し、`DeviceUseTrigger`オブジェクトの`RequestAsync`を起動するメソッドがバック グラウンド タスクをトリガーし、返します、`DeviceTriggerResults`オブジェクトから`RequestAsync`バック グラウンド タスクが正常に開始するかどうかを判断するために使用します。

    **重要な**Windows をチェックして、すべての必要なタスクの開始に使用ポリシーは、完了したことを確認します。 すべてのポリシーのチェックが完了した場合、操作が進行中に安全に中断するアプリを許可する、フォア グラウンド アプリの外部でバック グラウンド タスクとして、更新操作が実行されているようになりました。 Windows はまた、ランタイムの要件を強制し、それらの要件が満たされた不要になった場合は、バック グラウンド タスクをキャンセルします。



3.  最後に、`SyncWithDeviceAsync`メソッドは、`DeviceTriggerResults`から返されるオブジェクト`StartSyncBackgroundTaskAsync`をバック グラウンド タスクが正常に開始するかどうかを判断します。 Switch ステートメントを使用して検査の結果 `DeviceTriggerResults`


5.  フォア グラウンド アプリの実装をプライベート`OnSyncWithDeviceProgress`イベント ハンドラー デバイスのバック グラウンド タスクからの進行状況でアプリの UI を更新します。

6.  フォア グラウンド アプリの実装をプライベート`OnSyncWithDeviceCompleted`バック グラウンド タスクが完了したときに、バック グラウンド タスクからフォア グラウンド アプリへの移行を処理するイベント ハンドラー。

    1.  使用して、`CheckResults`のメソッド、`BackgroundTaskCompletedEventArgs`バック グラウンド タスクによって例外がスローされたかどうかを決定するオブジェクト。
    2.  これで、バック グラウンド タスクが完了し、ユーザーに通知する UI が更新されるフォア グラウンド アプリはアプリによって使用するためのデバイスを再度開かれます。

7.  フォア グラウンド アプリ実装のプライベート ボタンのクリックしてイベント ハンドラーを起動し、バック グラウンド タスクの取り消し、UI から。

    1.  プライベート`Sync_Click`イベント ハンドラーの呼び出し、`SyncWithDeviceAsync`メソッドは、前の手順で説明します。
    2.  プライベート`CancelSync_Click`イベント ハンドラーの呼び出し、プライベート`CancelSyncWithDevice`バック グラウンド タスクをキャンセルするメソッド。

8.  プライベート`CancelSyncWithDevice`メソッドは、登録を解除しを使用して、デバイスを再度開くことができますので、任意のアクティブなデバイスの同期をキャンセル、 [BackgroundTaskRegistration.Unregister](https://go.microsoft.com/fwlink/p/?LinkId=309315)メソッド。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カスタム USB デバイスのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )

[ファームウェア更新の USB デバイスのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=309186)

[UWP デバイス アプリによるデバイスの同期と更新](device-sync-and-update-for-uwp-device-apps.md)

[起動する、再開、およびマルチタス キング](https://go.microsoft.com/fwlink/p/?LinkId=309316)

[バック グラウンド タスクを使用してアプリをサポートしています。](https://go.microsoft.com/fwlink/p/?LinkID=254337)










