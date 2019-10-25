---
title: シリアル バス ドライバー レイヤー
description: シリアルバスドライバーは、ACPI によって作成された PDO に基づいて読み込まれ、GPIO や I2C コントローラーなどのシステムリソースに対してクエリを実行し、アクセスしてシグナリングコントロールを実行することができます。
ms.assetid: E6A3E1CF-C25B-429B-946D-B300BAF3CF9B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4a6c57d54bb0fa55b1dc97a9f1a4cc210d40c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834538"
---
# <a name="serial-bus-driver-layer"></a>シリアル バス ドライバー レイヤー


シリアルバスドライバーは、ACPI によって作成された PDO に基づいて読み込まれ、GPIO や I2C コントローラーなどのシステムリソースに対してクエリを実行し、アクセスしてシグナリングコントロールを実行することができます。

## <a name="span-idsample_mechanism_for_power_controlspanspan-idsample_mechanism_for_power_controlspanspan-idsample_mechanism_for_power_controlspansample-mechanism-for-power-control"></a><span id="Sample_Mechanism_for_Power_Control"></span><span id="sample_mechanism_for_power_control"></span><span id="SAMPLE_MECHANISM_FOR_POWER_CONTROL"></span>電源管理のサンプルメカニズム


Bluetooth over USB には、スリープをサポートするためのインバンドシグナリング (つまり、USB の選択的な中断) とウェイクの機能が組み込まれています。 ただし、SoC プラットフォームでは、さまざまなコントローラーを使用して、電源管理をサポートするメカニズムをより柔軟に (およびカスタマイズ可能) できます。

アイドル状態とスリープ状態の通知を処理するための実装例を次に示します。

-   リモートデバイスからの要求を処理するためにホストのスリープを解除する必要がある場合 (たとえば、リモート接続)、GPIO 割り込みホスト\_、Bluetooth コントローラーによって通知されます。
-   GPIO signal line BT は、バスドライバーによって設定されたライン\_有効にします。これは、Bluetooth コアスタックがアイドル状態 (D2 に入っている) を検出したときにアサートされます。

この2つの GPIO 行は、システムリソースの形式で、通常の割り込みと新しい GPIO シグナルとしてドライバーを読み込んでいるときに、シリアルバスドライバーに報告されます。 相互接続プロパティは、システムインテグレーターと Bluetooth チップセットベンダー (IHV) によって ACPI テーブルで定義されます。 シリアルバスドライバーは、リソースを開いてアクセスするために、これらの依存するコントローラーの接続 Id を照会してキャッシュすることができます。

## <a name="span-idstartup_to_enable_idle_spanspan-idstartup_to_enable_idle_spanspan-idstartup_to_enable_idle_spanstartup-to-enable-idle"></a><span id="Startup_to_Enable_Idle_"></span><span id="startup_to_enable_idle_"></span><span id="STARTUP_TO_ENABLE_IDLE_"></span>起動してアイドル状態を有効にする


S0 システムの電源状態でのアイドルをサポートするために、次のタスクを実行するには、serial bus ドライバーが必要です。

1.  PnP および電源管理機能を報告します。統合デバイスとして、子 PDO のリムーバブルフラグを WdfFalse に設定する必要があります。
2.  関数ドライバー (Bluetooth コアドライバー) に対するアイドル状態がサポートされていることを報告します。
3.  Arm と disarm for wake、および wake signal を処理します。
4.  デバイスの電源状態通知を受信し、現在のデバイスの電源状態で i/o 完了を同期します。

**電源管理機能**

バスドライバーによって作成された子 PDO は、アイドル状態のサポートを有効にするための電源機能を設定し、次のような設定を含む電源マネージャーによって管理されます。

-   D2 デバイスの状態をサポートする機能。
-   アイドル状態にして D2 から復帰する機能。
-   システム状態からデバイスの状態へのマッピング、および Bluetooth コアドライバーとの同期。

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

子 PDO は、Bluetooth コアドライバーから IOCTL (i/o 制御) 要求を受信するための WDF キューを作成します。 このような要求は、デバイスが開始される前に、インターフェイスのバージョンと静的機能のクエリを実行します。このため、このキューを電源管理にすることはできません。

``` syntax
QueueConfig.PowerManaged = WdfFalse;

QueueConfig.EvtIoDeviceControl = PdoIoQuDeviceControl;

Status = WdfIoQueueCreate(ChildDevice, 
                          &QueueConfig, 
                          WDF_NO_OBJECT_ATTRIBUTES,
                          &Queue);
```

**Bluetooth トランスポート固有のアイドル機能のクエリ**

子 PDO は、(前のセクションで強調表示されているように) 電源管理機能を報告するだけでなく、Bluetooth コアドライバーのクエリにも応答して、アイドル状態に入る機能を提供します。 S0 でのアイドルをサポートするために、このフラグは次のように設定されています。

``` syntax
FdoExtension->BthXCaps.IsDeviceIdleCapable = TRUE;
```

**Arm と Disarm for Wake**

アイドルサポートの要件は、リモート Bluetooth デバイスからウェイクアップ要求を受信できることです。 このようなウェイクアップ要求のセットアップには、ウェイクが必要です。 Bluetooth 関数の PDO は、arm/disarm アクションを実行するためのコールバックを受信するように登録できます。

``` syntax
WDF_PDO_EVENT_CALLBACKS_INIT(&Callbacks);

// Receive this callback to arming the device for wake
Callbacks.EvtDeviceEnableWakeAtBus  = PdoDevEnableWakeAtBus;

// Receive this callback to disarming the device for wake
Callbacks.EvtDeviceDisableWakeAtBus = PdoDevDisableWakeAtBus;

WdfPdoInitSetEventCallbacks(DeviceInit, &Callbacks);
```

上記のメカニズムがサポートされているため、Bluetooth コアドライバーはアイドルとウェイクのサポートを有効にすることができます。

**デバイスの電源状態の通知**

子 PDO は、デバイスの電源状態の遷移を通知するために、D0 を入力および終了するコールバックを受信するように登録します。 現在のデバイスの電源状態は、IO の完了を同期するために使用されます。つまり、通常の IO の完了は、D0 でのみ完了する必要があります。

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

## <a name="span-idarm_for_wakespanspan-idarm_for_wakespanspan-idarm_for_wakespanarm-for-wake"></a><span id="Arm_for_Wake"></span><span id="arm_for_wake"></span><span id="ARM_FOR_WAKE"></span>ウェイクの Arm


アイドル状態に入る前に、シリアルバスドライバーは、 [**EvtDeviceEnableWakeAtBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)に対して arm 用のコールバックを受信します。

Wake のためのメカニズムは、SoC プラットフォームに固有のベンダーであるため、このセクションの範囲外です。 ただし、Windows では、バスドライバーがウェイクアップ信号を受信できるように準備されており、そのようなシグナルを処理するコールバック関数 (ISR など) があることを前提としています。

## <a name="span-identer_idlespanspan-identer_idlespanspan-identer_idlespanenter-idle"></a><span id="Enter_Idle"></span><span id="enter_idle"></span><span id="ENTER_IDLE"></span>アイドル状態の入力


Bluetooth コアドライバーにより、時間ベースのアイドル検出メカニズムが有効になります。 アイドル状態の要件を満たしている場合、コアドライバーはスタックの開始を開始してアイドル状態になります。 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、入力候補関数と共に D2 に入るようにパワーを設定します。 バスドライバーが IRP を完了すると、この完了関数が呼び出されます。 現時点では、D2 への切り替えが完了しています。

Bluetooth コアドライバーは、アイドル状態に移行している間、保留中のすべての読み取り要求を取り消し、アクティブに復帰するときに再起動します。 シリアルバスドライバー自体がアイドル状態に入るためには、空の電源管理キューが必要です。

Bluetooth コアドライバーは、アイドル状態のタイムアウトに加えて、次のように、アイドル状態に入る前にさまざまな状況を考慮します。

-   直前に発行した HCI コマンドが完了するまで待ちます。 注: Bluetooth コアドライバーは、完了するまでアイドル状態になりません。
-   接続されているすべてのデバイスは、スニフモードです。

このアイドル状態の場合、多機能コントローラーは、Bluetooth 機能によって機能を調整するオプションを備えていますが、揮発性の設定と構成を維持するために電力を供給し続ける必要があります。 その後、そのスリープ解除メカニズムを使用して、スタックをアクティブ (D0) 状態に戻してから、i/o 通信を再開できます。

## <a name="span-idwake_from_sleepspanspan-idwake_from_sleepspanspan-idwake_from_sleepspanwake-from-sleep"></a><span id="Wake_from_Sleep"></span><span id="wake_from_sleep"></span><span id="WAKE_FROM_SLEEP"></span>スリープ状態からの復帰


Bluetooth 機能が1つ以上のデバイスとペアリングされていて、スリープ状態にある間、そのラジオは、ペアリングされたデバイスからの要求を定期的にスキャンしています。 ペアリングされたデバイスが要求を開始し、Bluetooth ラジオによって受信されると、アクティブ状態に再開するプロセスが開始されます。 デバイススタックがアクティブ (D0) に再開されると、ドライバーはこのリモート要求の処理を開始できます。

このリモート要求は、前のセクションで説明したように、バスドライバーの wake シグナル処理関数によって処理されます。 このウェイクアップシグナル処理関数は、PDO のデバイスの状態が実際に D2 状態であることを確認し、 [**WdfDeviceIndicateWakeStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus) (PDO、success status) を呼び出して、W/w (Wait WAKE) IRP を完了するように kmdf に通知します。 この時点で、この W/W IRP の完了関数が呼び出され、その開始側 (Bluetooth コアドライバーと電源ポリシー所有者) によって処理されるようになります。

W/W IRP が完了すると、Bluetooth コアドライバーがトリガーされ、D0 への移行が開始されます。 このメソッドは、デバイスの電源状態を D0 に設定するために、 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)に完了関数を要求します。

シリアルバスドライバーは、アクティブな D0 状態に再開する前に、wake を無効にするための notification [**EvtDeviceDisableWakeAtBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)を受信する場合があります。これにより、前に[**EvtDeviceEnableWakeAtBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)た処理を元に戻すプロセスが完了します。

Bluetooth ドライバースタックが D0 に再開された後、シリアルバスドライバーはリモートデバイス要求を完了できます。

一部のイベントは、次のようなシリアルバスドライバーで同期する必要があります。

-   D2 を入力するときは、保留中の W/W Irp が既に存在している必要があります。 これは、W/W Irp を受信するときではなく、ウェイクシグナルを受信するための取り組まが発生したときです。 ウェイクシグナルは、D2 状態の場合にのみ実行可能です。
-   D2 の入力中に (パケットを送信するために) データが到着していて、保留中の読み取り要求がキューに存在しない場合、バスドライバーは受信データをキャッシュして D2 に入ることができます。 次に、W/W Irp (success) を完了してシステムを D0 に復帰させ、読み取り要求を再度保留し、完了します。
-   Bthport は、保留中のすべての読み取り要求を取り消し、D2 に入る前に完了を待機します。 同時に、シリアルバスドライバーは、完全な HCI パケットを受信し、この HCI パケットを返す読み取り要求をキューから解除している可能性があります。 シリアルバスドライバーはこの要求を完了する必要があり、その後、D2 に入るように開始されます。

ホスト側で Bluetooth アプリケーションによって開始されたアクションは、スタックをアイドル状態から復帰させることもできます。 この場合、デバイスの電源状態の移行のみが必要であり、この操作は Bluetooth コアドライバーによって開始されます。

電力のアップ時間を短縮するために、シリアルバスドライバーのコールバック関数 (EnterD0 や wake など) を、ページング可能としてマークすることはできません。

## <a name="span-ida_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitionsspanspan-ida_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitionsspanspan-ida_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitionsspana-flowchart-to-express-the-idlewake-armdisarm-and-device-power-state-transitions"></a><span id="A_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="a_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="A_FLOWCHART_TO_EXPRESS_THE__IDLE_WAKE__ARM_DISARM__AND_DEVICE_POWER_STATE_TRANSITIONS"></span>アイドル/ウェイク、arm/disarm、およびデバイスの電源状態遷移を表現するフローチャート


次に示すのは、アイドルとウェイクのサポートのための一般的なシーケンスとロジックを示す、簡略化されたフローチャートです。 このロジックは多くのドライバーとスレッドにまたがり、例外と、表現されていないコーナーケース (ホスト側のアプリケーションは、アイドル状態からスタックを復帰させることもできます) があります。

![bluetooth デバイスの電源状態遷移のフローチャート](images/bthdevicepwrstatetransitionsflowchart.png)

## <a name="span-idbus_driver_s_own_power_managementspanspan-idbus_driver_s_own_power_managementspanspan-idbus_driver_s_own_power_managementspanbus-drivers-own-power-management"></a><span id="Bus_Driver_s_own_Power_Management"></span><span id="bus_driver_s_own_power_management"></span><span id="BUS_DRIVER_S_OWN_POWER_MANAGEMENT"></span>バスドライバーの独自の電源管理


シリアルバスドライバーは、関数ドライバー (FD) とそのレイヤーの電源ポリシー所有者 (PPO) です。 そのため、独自の電源管理を処理する必要があります。 すべての子がデバイスの電源状態を下げると、より低い電力状態になる可能性があります。 この低電力状態を入力する準備ができたら、UART コントローラードライバーに対する保留中の i/o 要求を取り消すことができます。これにより、UART ドライバーも低電力状態にすることができます。 ただし、UART ドライバーは、その電源状態が後でアクティブに戻ったときに、デバイス設定 (ボーレートを含む) を保持して復元する必要があります。

 

 





