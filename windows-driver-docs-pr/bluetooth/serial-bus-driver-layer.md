---
title: シリアル バス ドライバーの層
description: シリアル バス ドライバーは現在が読み込まれて、ACPI によって作成された PDO に基づいてとクエリ、およびシグナリング コントロールを実行する GPIO、I2C コント ローラーなど、システム リソースにアクセスできます。
ms.assetid: E6A3E1CF-C25B-429B-946D-B300BAF3CF9B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4b7a842b8f49498a353ffe949fd36a6d8ea264
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531834"
---
# <a name="serial-bus-driver-layer"></a>シリアル バス ドライバーの層


シリアル バス ドライバーは現在が読み込まれて、ACPI によって作成された PDO に基づいてとクエリ、およびシグナリング コントロールを実行する GPIO、I2C コント ローラーなど、システム リソースにアクセスできます。

## <a name="span-idsamplemechanismforpowercontrolspanspan-idsamplemechanismforpowercontrolspanspan-idsamplemechanismforpowercontrolspansample-mechanism-for-power-control"></a><span id="Sample_Mechanism_for_Power_Control"></span><span id="sample_mechanism_for_power_control"></span><span id="SAMPLE_MECHANISM_FOR_POWER_CONTROL"></span>電源管理のためのサンプルのメカニズム


USB 経由で Bluetooth インバンドに (つまり USB のセレクティブ サスペンド) スリープをサポートし、復帰の通知メカニズムが組み込まれています ただし、SoC プラットフォームで電源管理をサポートするためのメカニズムできますより柔軟な (およびカスタマイズ可能な) は、さまざまなコント ローラーを使用します。

アイドル状態を確認し、シグナルをスリープ解除する実装のサンプルを次に示します

-   GPIO 割り込みホスト\_ウェイクの行とリモート デバイス (例: リモート接続) からの要求にサービス ホストをスリープ解除する必要があるときに、Bluetooth コント ローラーによって通知
-   GPIO 信号 BT\_線を有効にする - バス ドライバーによって設定され、オプションがアクティブなときにアサート (D0 で core スタック) または Bluetooth core スタックがアイドル (D2 に入力する) を検出されたときに、アサート解除されます。

システム リソースの形式でこれら 2 つの GPIO 行は、通常の割り込みと新しい GPIO 信号とドライバーの読み込み中に、シリアル バス ドライバーに報告されます。 その相互接続のプロパティは、システム インテグレーターと Bluetooth チップセット ベンダー (IHV) によって、ACPI テーブルで定義されます。 シリアル バス ドライバーでは、クエリを実行でき、これら依存コント ローラーの接続を開き、そのリソースにアクセスするために Id をキャッシュすることができます。

## <a name="span-idstartuptoenableidlespanspan-idstartuptoenableidlespanspan-idstartuptoenableidlespanstartup-to-enable-idle"></a><span id="Startup_to_Enable_Idle_"></span><span id="startup_to_enable_idle_"></span><span id="STARTUP_TO_ENABLE_IDLE_"></span>スタートアップをアイドル状態を有効にします。


S0 システム電源の状態でアイドル状態をサポートするために、次のタスクを実行するシリアル バス ドライバーが必要です。

1.  PnP レポートおよび電源管理機能。統合のデバイスとして、取り外し可能なフラグ、子の PDO する必要がありますに設定する WdfFalse。
2.  サポートしていること、関数のドライバー (Bluetooth core ドライバー) をアイドル状態を報告します。
3.  Arm を処理し、スリープを解除し、復帰の信号。
4.  デバイスの電源状態の通知を受信し、現在のデバイスの電源状態の I/O 完了を同期します。

**電源管理機能**

子バス ドライバーによって作成された PDO はアイドル状態のサポートを有効にする電源機能を設定しなどを示す設定を含む、電源マネージャーでを管理します。

-   D2 デバイスの状態をサポートする機能がそのです。
-   入力するためには、その機能は、アイドル状態し、D2 からの復帰にします。
-   デバイスにシステム状態のマッピングは、状態し、Bluetooth core ドライバーと同期します。

``` syntax
WDF_DEVICE_POWER_CAPABILITIES_INIT(&PowerCaps);
…
PowerCaps.DeviceD1 = WdfFalse;
PowerCaps.DeviceD2 = WdfTrue;
…
PowerCaps.DeviceWake = PowerDeviceD2;

PowerCaps.DeviceState[PowerSystemWorking]   = PowerDeviceD0;
PowerCaps.DeviceState[PowerSystemSleeping1] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemSleeping2] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemSleeping3] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemHibernate] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemShutdown]  = PowerDeviceD3;
..
WdfDeviceSetPowerCapabilities(ChildDevice, &PowerCaps);
```

PDO の子では、WDF を Bluetooth core ドライバーから IOCTL (入出力制御) 要求を受信するキューを作成します。 このような要求が、インターフェイスのバージョンと前; 開始されているデバイスに静的機能に対してクエリを実行するにはそのため、このキューは、電源管理をすることはできません。

``` syntax
QueueConfig.PowerManaged = WdfFalse;

QueueConfig.EvtIoDeviceControl = PdoIoQuDeviceControl;

Status = WdfIoQueueCreate(ChildDevice, 
                          &QueueConfig, 
                          WDF_NO_OBJECT_ATTRIBUTES,
                          &Queue);
```

**アイドル状態の機能の特定のクエリを Bluetooth トランスポート**

(前のセクションで強調表示されている) として電源管理機能をレポートするには、だけでなく子 PDO もアイドル状態にその機能の Bluetooth core ドライバーのクエリに応答します。 サポートするために、S0 でアイドル状態このフラグが設定します。

``` syntax
FdoExtension->BthXCaps.IsDeviceIdleCapable = TRUE;
```

**Arm し、ウェイク アップの解除**

アイドル状態のサポートの要件は、Bluetooth デバイスをリモートからスリープ解除要求を受信する機能です。 このようなスリープ解除要求のセットアップでは、ウェイク アップに装備されている必要があります。 Arm のオン/操作を実行するコールバックを受信する Bluetooth 関数の PDO を登録できます。

``` syntax
WDF_PDO_EVENT_CALLBACKS_INIT(&Callbacks);

// Receive this callback to arming the device for wake
Callbacks.EvtDeviceEnableWakeAtBus  = PdoDevEnableWakeAtBus;

// Receive this callback to disarming the device for wake
Callbacks.EvtDeviceDisableWakeAtBus = PdoDevDisableWakeAtBus;

WdfPdoInitSetEventCallbacks(DeviceInit, &Callbacks);
```

上記の機構をサポート、Bluetooth core ドライバー アイドル状態を有効にするし、サポートをスリープ解除します。

**デバイスの電源状態の通知**

入力し、デバイスの電源の状態遷移の通知を受け取るため D0 を終了するコールバックを受信する子の PDO を登録します。 現在のデバイスの電源状態を使用して IO の完了を同期 – つまり通常の IO 完了 D0 で完了するだけです。

``` syntax
    //
    // Register to receive device power state change notification
    //
    WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&PnpPowerCallbacks);  

    PnpPowerCallbacks.EvtDeviceD0Entry = PdoDevD0Entry;
    PnpPowerCallbacks.EvtDeviceD0Exit  = PdoDevD0Exit; 

    
    WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, 
                                           &PnpPowerCallbacks);
```

## <a name="span-idarmforwakespanspan-idarmforwakespanspan-idarmforwakespanarm-for-wake"></a><span id="Arm_for_Wake"></span><span id="arm_for_wake"></span><span id="ARM_FOR_WAKE"></span>ウェイク アップの arm


アイドル状態を入力する前に、シリアル バス ドライバーのコールバックの受信は[ **EvtDeviceEnableWakeAtBus** ](https://msdn.microsoft.com/library/windows/hardware/ff540866) wake の arm にします。

ウェイク アップの arm へのメカニズムでは、ベンダー固有の SoC プラットフォームと、このセクションの範囲外のためです。 ただし、Windows には、このようなシグナルを処理するコールバック関数 (例: ISR) があります、バス ドライバーは、ウェイク信号を受信する準備が期待しています。

## <a name="span-identeridlespanspan-identeridlespanspan-identeridlespanenter-idle"></a><span id="Enter_Idle"></span><span id="enter_idle"></span><span id="ENTER_IDLE"></span>アイドル状態を入力します


Bluetooth core ドライバーにより、アイドル状態検出の時間ベースのメカニズムです。 アイドル状態の要件を満たす、時にアイドル状態にスタックを開始するコア ドライバーを開始します。 呼び出す[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)完了関数 D2 に付随する電力を設定します。 バス ドライバーは IRP を完了したら、この完了関数が呼び出されます。 この時点では、D2 への移行の完了を取得します。

アイドル状態への移行、中に Bluetooth core ドライバーは保留中のすべての読み取り要求をキャンセルし、アクティブに再開するときに、それらを再起動します。 空の電源管理対象のキューは、シリアル バス ドライバー自体のアイドル状態を入力するために必要です。

アイドル タイムアウトは、だけでなく、Bluetooth core ドライバーを考慮に入れますさまざまな状況など、アイドル状態に入る前に。

-   発行しただけ HCI コマンドの完了を待ちます。 注: Bluetooth core ドライバーは入力アイドル状態の完了まで。
-   接続されているすべてのデバイスはスニッフィング モードです。

このアイドル状態で、多機能のコント ローラー、Bluetooth 関数によってその能力を制限するオプションがありますが、引き続き、揮発性の設定と構成を維持するために電力を供給する必要があります。 I/O の通信を再開できますが後に作業中の (D0) 状態に戻すスタックをスリープ解除するには、そのウェイク メカニズムに依存することできます。

## <a name="span-idwakefromsleepspanspan-idwakefromsleepspanspan-idwakefromsleepspanwake-from-sleep"></a><span id="Wake_from_Sleep"></span><span id="wake_from_sleep"></span><span id="WAKE_FROM_SLEEP"></span>スリープ状態から復帰します。


Bluetooth 関数は、1 つまたは複数のデバイスとペアリングされているが、スリープ状態では、そのラジオは定期的に、ペアリングされたデバイスからの要求をスキャンします。 ペアになっているデバイスでは、要求を開始するし、Bluetooth 無線が受信した取得、アクティブな状態を再開するプロセスを開始します。 アクティブ (D0) には、デバイス スタックを再開しました、ドライバーは、このリモート要求のサービス開始できます。

このリモート要求は、最後のセクションで説明したように、バス ドライバー ウェイク信号処理関数によって処理されます。 このウェイク信号処理関数がいることを確認 PDO のデバイスの状態 D2 の状態が実際を呼び出して[ **WdfDeviceIndicateWakeStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff546025) (PDO、成功の状態) を完了する KMDF に通知する、IRP の W/W (待機ウェイク)。 この W/W IRP の完了関数が呼び出すことができ、Bluetooth core ドライバーと電源ポリシー所有者 - のイニシエーターによって処理され、この時点では。

W/W IRP の完了には、D0 への移行を開始する Bluetooth core ドライバーがトリガーされます。 要求を[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734) D0 にデバイスの電源状態を設定する入力候補の関数を使用します。

シリアル バス ドライバー active d0 へを再開する前に通知を受け取ることがあります[ **EvtDeviceDisableWakeAtBus** ](https://msdn.microsoft.com/library/windows/hardware/ff540858)ウェイク – を無効にするものを反転させるプロセスを完了[ **EvtDeviceEnableWakeAtBus** ](https://msdn.microsoft.com/library/windows/hardware/ff540866)前でした。

Bluetooth ドライバー スタックの D0 を再開した後、シリアル バス ドライバーをリモート デバイス要求完了できます。

一部のイベントは、シリアル バス ドライバーなど、同期する必要があります。

-   D2 を入力するときに既にある保留中の W/W Irp。 これは、場合、ウェイク信号を受信するウェイク アップの取り組まを実行するのではなく W/W Irp を受信する場合です。 ウェイク信号は D2 状態のみ中にアクションにつながるです。
-   D2 を入力するときにデータの到着 (パケットを形成する) をキューに保留中の読み取り要求がない場合は、バス ドライバーは受信データをキャッシュし、D2 を入力します。 Re 保留 D0 にシステムを起動し、読み取り要求を完了すること (成功) で W/W Irp を完了できます。
-   Bthport は保留中のすべての読み取り要求をキャンセルし、D2 に入る前に、完了するまで待機します。 同時に、シリアル バス ドライバーは完全な HCI パケットを受け取ることがおよびを返すこの HCI パケット読み取りの要求をキューに登録解除します。 シリアル バス ドライバーは、この要求を完了する必要があり、D2 を入力し、開始されます。

ホスト側の Bluetooth アプリケーションによって開始されたアクションは、アイドル状態からスタックをスリープ解除もできます。 ここでは、デバイスの電源状態遷移のみが必要と Bluetooth core ドライバーによってこのアクションが開始されます。

電源稼働時間を軽減するためにシリアル バス ドライバーのコールバック関数 (例: EnterD0 とスリープ解除) する必要がありますがマークされていないページング可能です。

## <a name="span-idaflowcharttoexpresstheidlewakearmdisarmanddevicepowerstatetransitionsspanspan-idaflowcharttoexpresstheidlewakearmdisarmanddevicepowerstatetransitionsspanspan-idaflowcharttoexpresstheidlewakearmdisarmanddevicepowerstatetransitionsspana-flowchart-to-express-the-idlewake-armdisarm-and-device-power-state-transitions"></a><span id="A_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="a_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="A_FLOWCHART_TO_EXPRESS_THE__IDLE_WAKE__ARM_DISARM__AND_DEVICE_POWER_STATE_TRANSITIONS"></span>アイドル状態またはスリープ解除、arm/解除、およびデバイスの電源の状態遷移を表現するフローチャート


次に一般的なシーケンスを説明するために簡略化されたフローチャートとのロジックがアイドル状態し復帰のサポート。 このロジックは、多くのドライバーと、スレッドにまたがるし、例外と表されないのコーナー ケースがある (例: ホスト側のアプリケーションも復帰がアイドル状態から stack)。

![bluetooth デバイスの電源の状態遷移のフローチャート](images/bthdevicepwrstatetransitionsflowchart.png)

## <a name="span-idbusdriversownpowermanagementspanspan-idbusdriversownpowermanagementspanspan-idbusdriversownpowermanagementspanbus-drivers-own-power-management"></a><span id="Bus_Driver_s_own_Power_Management"></span><span id="bus_driver_s_own_power_management"></span><span id="BUS_DRIVER_S_OWN_POWER_MANAGEMENT"></span>バス ドライバーの電源管理


シリアル バス ドライバーは、関数ドライバー (FD) とそのレイヤーの電源ポリシー所有者 (PPO) です。 したがって、独自の電源管理を処理するために必要です。 すべての子入力デバイスの電力の少ない状態、自体低電力状態にそれを入力できます。 この低電力状態に入る準備が保留中の I/O 要求 UART コント ローラーのドライバーには取り消せます – これにより、低電力状態にも入力する UART ドライバー。 ただし、UART ドライバーを保存および (ボー レートを含む) のデバイス設定を復元する必要がありますの電源状態がアクティブに後で再開される場合。

 

 





