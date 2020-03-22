# <a name="win32-services-interacting-with-devices"></a>デバイスと対話する Win32 サービス

## <a name="motivation"></a>動機

デバイスと対話する[INF AddService](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)を使用してインストールされた理想的な Win32 サービスは、*ドライバー*が*デバイス*と対話する場合と同様に動作します。  デバイスの存在に応じてドライバーが読み込まれ、アンロードされます。また、デバイスと対話する Win32 サービスは、デバイスの存在に応じて、**開始**と**停止**という同じパターンに従う必要があります。  

サービスが開始されるのは、関連付けられているデバイスが存在しないときに、デバイスインターフェイスが通信と停止した場合のみです。  この設計パターンでは、望ましくない動作と未定義の動作を最小化する堅牢なサービスが保証されます。  ここでは、このパターンに従ってサービスを設計する方法について説明します。

## <a name="service-install"></a>サービスのインストール

サービスをインストールするには、 [INF AddService](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ディレクティブを使用します。  これにより、サービスを作成して開始することができます。

サービスの需要開始を行うフラグを追加します。  これを実現するには、サービストリガーを開始するための**Starttype = 0x3**を設定します。

このセクションの最後の手順では、 **addtrigger**ディレクティブを使用して、デバイスインターフェイスが到着したときにサービスを開始します ( **addtrigger**に関する詳細については、「 [addtrigger](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive) 」を参照してください)。  AddTrigger を使用する方法の例を次に示します。

```
[UserSvc_AddTrigger]
TriggerType = 1                                   ; SERVICE_TRIGGER_TYPE_DEVICE_INTERFACE_ARRIVAL
Action      = 1                                   ; SERVICE_TRIGGER_ACTION_SERVICE_START
SubType     = %GUID_DEVINTERFACE_OSRFX2%          ; Interface class GUID
DataItem    = 2, "USB\VID_0547&PID_1002"          ; SERVICE_TRIGGER_DATA_TYPE_STRING

[UserSvc_Install]
ServiceType   = 0x10 ; SERVICE_WIN32_OWN_PROCESS
StartType     = 3   ; SERVICE_DEMAND_START
ErrorControl  = 0   ; SERVICE_ERROR_IGNORE
ServiceBinary = %13%\oemsvc.exe
AddTrigger    = UserSvc_AddTrigger

```
DataItem で指定された HardwareId は省略可能であり、通常は、ジェネリッククラスインターフェイスを使用してトリガーのスコープをより特定のデバイスに限定する場合にのみ必要です。  

## <a name="service-runtime"></a>サービス ランタイム
    
ランタイムの観点からは、サービスの最初のステップはデバイスインターフェイス通知に登録する必要があります。  これを実現するための規範的なガイダンスについては、このページの「[デバイスインターフェイスへの到着とデバイスの削除に関する通知の登録](https://docs.microsoft.com/windows-hardware/drivers/install/registering-for-notification-of-device-interface-arrival-and-device-removal)」を参照してください。

具体的には、 **CM_Register_Notification**を**CM_NOTIFY_FILTERY_TYPE_DEVICEINTERFACE**フラグと共に使用して、デバイスインターフェイス通知の適切な登録を行う必要があります。

>[!NOTE]
>サービスが開始されると、到着通知が既に渡されている可能性があるため、デバイスインターフェイスの通知を受け取るという事実に依存することはできません。 代わりに、インターフェイスが既に存在するかどうかを確認するために、デバイスインターフェイスの一覧を取得する必要があります。

通知を登録すると、次の2つの手順で目的のデバイスインターフェイスを見つけることができます。

1. 通知コールバックからのインターフェイスの検出
2. 既存のデバイスインターフェイスの一覧を照会し、を使用して目的のインターフェイスを検索し**CM_Get_Device_Interface_List**

>[!NOTE] 
>通知の登録と目的のデバイスインターフェイスの検索の間にインターフェイスが到着する可能性があることに注意してください。  その場合は、通知コールバックとインターフェイスの一覧の両方にインターフェイスが表示されます。

目的のデバイスインターフェイスが見つかったら、 [CreateFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を使用してインターフェイスへのハンドルを開きます。  

次の手順では、デバイスを操作および管理するために、2番目のインターフェイスごとの通知を登録します。 これを行うには、 **CM_Register_Notification**を**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**フラグと共に使用します。  これにより、デバイスが離れるときに、それに応じてハンドルが解放されるようになります。

デバイスインターフェイスの到着と削除を追跡して、最後のデバイスインターフェイスが削除されるようにして、サービスを停止できるようにする必要があります。  最後のインターフェイスが削除されたら、サービスを停止します (詳細については、この[ページ](https://docs.microsoft.com/windows/desktop/Services/service-servicemain-function)を参照してください)。 これを行うには、次の手順を実行します。

1. サービスが停止していることを示すために SCM に**SERVICE_STOP_PENDING**状態を通知する
2. サービスが使用していたすべてのものを Unitialize/クリーンアップする
3. 停止操作を完了するために**SERVICE_STOP**状態を SCM に Post

サービスが停止されている場合は、既存のすべての開いているハンドルをデバイスインターフェイスに対して確認してから、クリーンアップするようにします (存在しない場合もあります)。 
  
デバイスのインターフェイスは、デバイスのインストール中、デバイスの有効化/無効化、デバイスの再列挙、システムの再起動、または一覧表示されていない他のシナリオで発生します。  デバイスインターフェイスが復帰すると、トリガーの開始登録に基づいてサービスが開始されます。

このフローにより、デバイスインターフェイスの到着時にサービスが開始され、最後のデバイスインターフェイスが存在しなくなった時点で停止します。

## <a name="code-sample--related-links"></a>コードサンプル & 関連リンク

GitHub には、このようなイベントのフローをサービスがどのように活用できるかを示すサンプルがあります。  このサンプルについては、「 [Win32 サービスのサンプル](https://github.com/microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_usersvc)」を参照してください。

Addtrigger に関する有用なドキュメントは**AddTrigger** 、 [addtrigger](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ページでも参照できます。
