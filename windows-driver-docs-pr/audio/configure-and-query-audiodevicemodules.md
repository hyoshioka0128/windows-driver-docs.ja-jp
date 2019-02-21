---
Description: This article shows how to send commands and receive change notifications from audio device modules. from a Universal Windows Platform (UWP) app.
ms.assetid: AA053196-F331-4CBE-B032-4E9CBEAC699C
title: オーディオ デバイス モジュールのクエリを構成し、
label: Configure and query audio device modules
template: ''
ms.author: drewbat
ms.date: 06/28/2017
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 608926ac8c1eab801eecb31027c9261e4041134a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528763"
---
# <a name="configure-and-query-audio-device-modules"></a>オーディオ デバイス モジュールのクエリを構成し、 

この記事では、コマンドを送信し、UWP アプリからのオーディオ デバイス モジュールからの変更通知を受信する方法を示します。 オーディオ デバイス モジュール処理単位または他のオーディオ設定モジュール、オーディオ ドライバーで定義されたハードウェア効果があります。 この機能は、モジュール プロバイダーのユーザーを制御できるようにして、DSP で実行されているオーディオ処理モジュールからステータス情報を取得する UWP アプリを作成できるようにするために設計されました。 オーディオ デバイス モジュールのこの記事に示すように Api を使用するには、制限する必要があります指定*audioDeviceConfiguration*アプリケーション パッケージ マニフェストで機能します。

## <a name="get-an-instance-of-the-audiodevicemodulesmanager-class"></a>AudioDeviceModulesManager クラスのインスタンスを取得します。
この記事に示すように、すべてのオーディオ デバイス モジュールの操作の開始のインスタンスを取得することによって、  **[AudioDeviceModulesManager](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager)** します。 これを最初に、静的なを呼び出すことによって行います**[GetDefaultAudioRenderId](https://docs.microsoft.com/uwp/api/windows.media.devices.mediadevice.getdefaultaudiorenderid)** のメソッド、 **[MediaDevice](https://docs.microsoft.com/uwp/api/windows.media.devices.mediadevice)** クラス。 コンス トラクターには、既定のオーディオのレンダリングのデバイスの ID を返しますこれ**AudioDeviceModulesManager**オーディオ デバイスに関連付けられているクラスのインスタンスを作成します。

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
```

## <a name="query-for-installed-audio-device-modules"></a>オーディオ デバイスがインストールされているモジュールのクエリ

オーディオ デバイス モジュールを呼び出すことによってインストールされたすべてのクエリ、 **[FindAll](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager.findall)** の**[AudioDeviceModulesManager](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager)** クラス。 オーディオ デバイスのモジュールを呼び出して一連の特定のクエリ**[FindAllById](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager.findallbyid)** 要求されたモジュールの ID を渡すとします。 次の例は、一連のモジュール、呼び出しのために、ID を定義**FindAllById**の一覧を取得する**[AudioDeviceModule](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule)** オブジェクトし、それぞれの詳細を出力します。デバッグ出力するモジュール。

C#
```csharp
public const string Contoso_AudioDeviceModuleId = "F72E09C3-FEBA-4C50-93BE-2CA56123AF09";
``` 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
var modules = audioModuleManager.FindAllById(Contoso_AudioDeviceModuleId);

foreach (var module in modules)
{
    var classId = module.ClassId;
    var name = module.DisplayName;
    var minorVersion = module.MinorVersion;
    var majorVersion = module.MajorVersion;
    var instanceId = module.InstanceId;

        Debug.WriteLine($"{classId} : {name} : {minorVersion} : {majorVersion} : {instanceId}");
}
``` 
## <a name="send-a-command-to-an-audio-device-module-and-receive-result-data"></a>オーディオ デバイス、モジュールにコマンドを送信し、結果データを受信
コマンドを呼び出すことによって、オーディオ デバイス モジュールに送信**[SendCommandAsync](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule.sendcommandasync)** 上、 **[AudioDeviceModule](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule)** オブジェクト。 **SendCommandAsync**メソッドは引数としてバイト配列を受け取ります。 通常このバイト配列には、コマンド識別子後に、コマンドに関連付けられたデータにはが含まれますが、コマンドの形式と値はまったくのベンダー定義し、システムによって透過的に処理されます。

**SendCommandAsync**メソッドが完了すると、取得する非同期操作を返します、 **[ModuleCommandResult](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule.sendcommandasync)** の結果を表すオブジェクト、コマンド。 **[状態](https://docs.microsoft.com/uwp/api/windows.media.devices.modulecommandresult.status)** プロパティには、システムが、コマンドを実行できるかどうかを示す列挙値が含まれています。 これは必ずしもオーディオ デバイス モジュールがコマンドが正常に実行できること。 **[結果](https://docs.microsoft.com/uwp/api/windows.media.devices.modulecommandresult.result)** プロパティには、コマンドの状態を示すために、オーディオ デバイス モジュールによって返されるバイト配列が含まれています。 通常、成功または失敗の後に、コマンドのデータの結果を示す値になります。 モジュールのコマンドと同様の応答形式のモジュールと値はベンダ定義です。

次の例では**FindAllAsync**オーディオ デバイスのモジュールのセットを取得します。 A  **[datawriter の各](https://docs.microsoft.com/uwp/api/windows.storage.streams.datawriter)** コマンドの例とデータを含むバイト配列を作成するために使用します。 **SendCommandAsync**コマンド バッファーを送信するために呼び出されると、非同期操作の完了後、 **ModuleCommandResult**が返されます。 コマンドの実行が成功した場合、 **[DataReader](https://docs.microsoft.com/uwp/api/windows.storage.streams.datareader)** 最初、モジュールから返される整数の状態値の読み取りに使用します。 この値は、ベンダー定義の成功値は、残りの結果データが読み取られ、UI を更新するなど、アプリによって使用します。


C#
```csharp
public const byte Contoso_ReverbLevel_Command = 30; 
public const byte Contoso_SendCommand_Success = 99;
``` 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
var modules = audioModuleManager.FindAllById(Contoso_AudioDeviceModuleId);

foreach (var module in modules)
{
    var writer = new Windows.Storage.Streams.DataWriter();
    writer.WriteByte(Contoso_ReverbLevel_Command);
    writer.WriteByte(100);

    var command = writer.DetachBuffer();

    var result = await module.SendCommandAsync(command);

    if (result.Status == SendCommandStatus.Success)
    {
        using (DataReader reader = DataReader.FromBuffer(result.Result))
        {
            int bufferStatus = reader.ReadInt32();
            if (bufferStatus == Contoso_SendCommand_Success)
            {
                byte[] data = { 0, 0 };
                reader.ReadBytes(data);
                // Do something with returned data, such as update UI
            }
        }
    }
}
```

## <a name="receive-notifications-when-audio-device-modules-are-modified"></a>オーディオ デバイス モジュールが変更されたときに通知を受け取る
登録することで、オーディオ デバイス モジュールが更新されたときにアプリが通知を受信できる、 **[ModuleNotificationReceived](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager.modulenotificationreceived)** イベント。 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);

audioModuleManager.ModuleNotificationReceived += AudioModuleManager_ModuleNotificationReceived;
``` 

**ModuleNotificationReceived**現在のオーディオ デバイスに関連付けられているすべてのオーディオ デバイス モジュールが変更されたときに発生します。 インスタンスを取得、イベントは、特定のモジュールに関連付けられているかどうかを判断する**AudioDeviceModule**にアクセスして、 **[モジュール](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs.module)** のプロパティ、 **[AudioDeviceModuleNoticiationEventArgs](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs)** イベント ハンドラー、および次のチェックに渡された、 **[ClassId](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule.classid)** プロパティをモジュールを識別します。 バイト配列に格納されているイベントに関連付けられているデータが渡される、 **[NotificationData](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs.notificationdata)** イベント引数のプロパティ。 コマンドと結果と同様、返されるバイト配列の形式は、ベンダー定義です。 次の例で、通知のデータの最初のバイトには、モジュールのリバーブのレベルの設定の値の例が含まれている場合、データの読み取りおよび UI を更新するために使用します。

C#
```csharp
public const byte Contoso_ReverbLevel_Data = 25;
```

C#
```csharp
private void AudioModuleManager_ModuleNotificationReceived(AudioDeviceModulesManager sender, AudioDeviceModuleNotificationEventArgs args)
{
    if (args.Module.ClassId == Contoso_AudioDeviceModuleId)
    {
        // Get the coefficient data from the reverb module.
        using (DataReader reader = DataReader.FromBuffer(args.NotificationData))
        {
            // read notification data.
            byte item = reader.ReadByte();

            // if reverb coefficient data are changed.
            if (item == Contoso_ReverbLevel_Data)
            {
                // read the new value
                byte[] data = { 0 };
                reader.ReadBytes(data);
                ReverbLevelSlider.Value = data[0];
            }
        }
    }
}
```
