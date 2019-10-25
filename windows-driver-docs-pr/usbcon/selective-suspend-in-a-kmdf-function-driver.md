---
Description: このトピックでは、KMDF 関数ドライバーが USB のセレクティブサスペンドをサポートする方法について説明します。
title: USB KMDF 機能ドライバーにおけるセレクティブ サスペンド
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: e1e85f54bdcc8b14a70e23e156da9e6b9617f347
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824165"
---
# <a name="selective-suspend-in-usb-kmdf-function-drivers"></a>USB KMDF 機能ドライバーにおけるセレクティブ サスペンド


**重要な API**

-   [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)
-   [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)
-   [**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)

このトピックでは、KMDF 関数ドライバーが USB のセレクティブサスペンドをサポートする方法について説明します。

USB ドライバーにユーザーモードでは利用できない機能またはリソースが必要な場合は、KMDF 関数ドライバーを指定する必要があります。 KMDF ドライバーは、KMDF 初期化構造に関連する値を設定し、適切なコールバック関数を提供することにより、選択的中断を実装します。 KMDF は、デバイスを中断および再開するために、下位のドライバーとの通信の詳細を処理します。

## <a name="guidelines-for-selective-suspend-in-kmdf-drivers"></a>KMDF ドライバーのセレクティブサスペンドのガイドライン


セレクティブサスペンドをサポートする KMDF ドライバーは、次のガイドラインに従う必要があります。

-   KMDF 関数ドライバーは、そのデバイススタックの PPO である必要があります。 既定では、KMDF 関数ドライバーは PPO です。
-   セレクティブサスペンドをサポートする KMDF 関数ドライバーでは、電源管理されているキュー、または電源管理されていないキューを使用できます。 既定では、PPOs のキューオブジェクトは電源管理されています。

**電源ポリシーの所有権と KMDF USB ドライバー**

既定では、USB デバイス用の KMDF 関数ドライバーは、デバイススタックの PPO です。 KMDF は、このドライバーの代わりにセレクティブサスペンドと再開を管理します。

**KMDF ドライバーの i/o キューの構成**

セレクティブサスペンドをサポートする KMDF 関数ドライバーでは、電源管理されているキュー、または電源管理されていないキューを使用できます。 通常、ドライバーは、着信デバイスの i/o 制御要求を受信するために、電源管理されていないキューを構成し、読み取り、書き込み、およびその他の電源に依存する要求を受信するように1つ以上の電源管理キューを構成します。 要求が電源管理キューに到着すると、KMDF は、ドライバーに要求を提示する前に、デバイスが D0 にあることを確認します。

デバイススタックの PPO の上にある KMDF フィルタードライバーを作成する場合は、電源管理キューを使用しないようにする必要があります。 この理由は、UMDF ドライバーの場合と同じです。 フレームワークは、デバイスが中断されている間に、電源管理キューからの要求を提示しないため、このようなキューを使用すると、デバイススタックが停止する可能性があります。

## <a name="selective-suspend-mechanism-for-kmdf-function-drivers"></a>KMDF 関数ドライバーの選択的中断メカニズム


KMDF は、USB のセレクティブサスペンドをサポートするために必要なほとんどの作業を処理します。 これは、i/o アクティビティを追跡し、アイドルタイマーを管理し、親ドライバー (Usbhub または Usbccgp) がデバイスを中断および再開する原因となるデバイス i/o 制御要求を送信します。

KMDF 関数ドライバーがセレクティブサスペンドをサポートしている場合、KMDF は、各デバイスオブジェクトが所有するすべての電源管理キューの i/o アクティビティを追跡します。 I/o カウントが0に達すると、フレームワークはアイドルタイマーを開始します。 既定のタイムアウト値は5秒です。

アイドルタイムアウト期間が経過する前に、デバイスオブジェクトに属する電源管理キューに i/o 要求が到着すると、フレームワークはアイドルタイマーをキャンセルし、デバイスを中断しません。

アイドルタイマーの期限が切れると、KMDF は、USB デバイスを中断状態にするために必要な要求を発行します。 関数ドライバーが USB エンドポイントで連続リーダーを使用している場合、リーダーの繰り返しポーリングは KMDF アイドルタイマーに対するアクティビティとしてカウントされません。 ただし、 [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数では、USB ドライバーは、デバイスが i/o 要求を送信しないときにドライバーが i/o 要求を送信しないようにするために、電源管理されていないキューによって送られる連続リーダーとその他の i/o ターゲットを手動で停止する必要があります。動作中の状態。 ターゲットを停止するために、ドライバーは[**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出し、ターゲットアクションとして**WdfIoTargetWaitForSentIoToComplete**を指定します。 応答として、フレームワークは、ターゲットの i/o キューにあるすべての i/o 要求が完了し、関連付けられている i/o 完了コールバックが実行された後にのみ、i/o ターゲットを停止します。

既定では、KMDF はデバイスを D0 からに移行し、ドライバーがアイドル設定で指定したデバイスの電源状態に遷移します。 移行の一環として、KMDF はドライバーの電源コールバック関数を他の電源ダウンシーケンスと同じ方法で呼び出します。

デバイスが中断された後、次のいずれかのイベントが発生すると、フレームワークはデバイスを自動的に再開します。

-   I/o 要求は、ドライバーの電源管理キューのいずれかに到着します。
-   ユーザーはデバイスマネージャーを使用して、USB のセレクティブサスペンドを無効にします。
-   ドライバーは、「[デバイスの中断の防止](#preventsusp)」で説明されているように、 [**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)を呼び出します。

デバイスを再開するために、KMDF はデバイススタックを使用して電源要求を送信し、他の電源シーケンスと同じ方法で、ドライバーのコールバック関数を呼び出します。

電源と電源のシーケンスに関係するコールバックの詳細については、 [WDF Drivers の「プラグアンドプレイと電源管理](http://download.microsoft.com/download/5/d/6/5d6eaf2b-7ddf-476b-93dc-7cf0072878e6/WDF-pnpPower.docx)」ホワイトペーパーを参照してください。

## <a name="supporting-usb-selective-suspend-in-a-kmdf-function-driver"></a>KMDF 関数ドライバーでの USB 選択的中断のサポート


KMDF 関数ドライバーで USB セレクティブサスペンドを実装するには、次のようにします。

-   アイドルタイムアウトなど、アイドルに関連する電源ポリシー設定を初期化します。
-   開いているハンドル、またはデバイスの i/o キューに関連付けられていないその他の理由によってデバイスが中断されないと判断した場合に、一時的に中断を回避したり操作を再開したりするロジックを含めることもできます。
-   ヒューマンインターフェイスデバイス (HID) 用の USB ドライバーで、選択的中断がサポートされていることを INF で指定します。

**KMDF 関数ドライバーの電源ポリシー設定を初期化しています**

USB セレクティブサスペンドのサポートを構成するために、KMDF ドライバーは、[**電源\_ポリシー\_アイドル\_設定の構造\_WDF\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)を使用します。 ドライバーはまず構造体を初期化し、次にドライバーとそのデバイスの機能に関する詳細情報を提供するフィールドを設定します。 通常、この構造体は、 *Evtdriverdeviceadd*または*Evtdeviceのハードウェア*関数に格納されます。

**WDF\_デバイスを初期化するには\_電源\_ポリシー\_アイドル\_設定の構造**

ドライバーは、デバイスオブジェクトを作成した後、 [**WDF\_デバイス\_電源\_ポリシー\_アイドル\_設定\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)関数を使用して構造体を初期化します。 この関数は、次の2つの引数を受け取ります。

-   [**WDF\_デバイスへのポインター\_電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)の構造体を初期化します。
-   選択的中断のサポートを示す列挙値。 ドライバーは**IdleUsbSelectiveSuspend**を指定する必要があります。

ドライバーで**IdleUsbSelectiveSuspend**が指定されている場合、関数は次のように構造体のメンバーを初期化します。

-   **IdleTimeout**は**IdleTimeoutDefaultValue** (現在は5000ミリ秒または5秒) に設定されています。
-   **UserControlOfIdleSettings**は**IdleAllowUserControl**に設定されています。
-   **Enabled**は**WdfUseDefaul**t に設定されています。これは、選択的中断が有効になっているが、 **UserControlOfIdleSettings**メンバーが許可した場合にユーザーが無効にできることを示します。
-   **Dxstate**は**PowerDeviceMaximum**に設定されています。これは、デバイスの報告された電源機能を使用して、アイドル状態のデバイスの遷移先の状態を判断します。

**USB のセレクティブサスペンドを構成するには**

ドライバーは、[**電源\_ポリシー\_アイドル\_設定の構造\_WDF\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)を初期化した後、その構造内の他のフィールドを設定してから、 **WdfDeviceAssignS0IdleSettings**を呼び出してこれらの値を渡すことができます。フレームワークへの設定。 次のフィールドは、USB 関数ドライバーに適用されます。

-   IdleTimeout: フレームワークがデバイスのアイドル状態を考慮する前に、i/o 要求を受信せずに経過する必要がある間隔 (ミリ秒単位)。 ドライバーは、ULONG 値を指定することも、既定値を受け入れることもできます。
-   UserControlOfIdleSettings —ユーザーがデバイスのアイドル設定を変更できるかどうかを指定します。 指定できる値は、IdIdleAllowUserControl Onotallowusercontrol とです。
-   DxState —フレームワークがデバイスを中断するデバイスの電源状態。 指定できる値は、PowerDeviceD1、PowerDeviceD2、および PowerDeviceD3 です。

    USB ドライバーでは、この値の初期設定を変更しないでください。 [**WDF\_デバイス\_電源\_ポリシー\_アイドル\_設定\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)関数は、この値を PowerDeviceMaximum に設定します。これにより、フレームワークはデバイスの機能に基づいて適切な値を選択します。

次のコードスニペットは、Osrusbfx2 サンプルドライバーの Device. c ファイルから抜粋したものです。

```cpp
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS idleSettings;
NTSTATUS    status = STATUS_SUCCESS;
//
// Initialize the idle policy structure.
//
WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS_INIT(&idleSettings, 
     IdleUsbSelectiveSuspend);
idleSettings.IdleTimeout = 10000; // 10 sec

status = WdfDeviceAssignS0IdleSettings(Device, &idleSettings);
if ( !NT_SUCCESS(status)) {
     TraceEvents(TRACE_LEVEL_ERROR, DBG_PNP,
                 "WdfDeviceSetPowerPolicyS0IdlePolicy failed %x\n", 
                 status);
    return status;
}
```

この例では、ドライバーは、 **IdleUsbSelectiveSuspend**を指定して[ **\_デバイス\_電源\_ポリシー\_アイドル\_設定\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)に呼び出します。 ドライバーは**IdleTimeout**を1万ミリ秒 (10 秒) に設定し、 **Dxstate**と**UserControlOfIdleSettings**のフレームワークの既定値を受け入れます。 その結果、フレームワークは、アイドル状態のときにデバイスを D3 状態に遷移し、管理者特権を持つユーザーがデバイスのアイドルサポートを有効または無効にするためのデバイスマネージャープロパティページを作成します。 次に、ドライバーは[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出してアイドルサポートを有効にし、これらの設定をフレームワークに登録します。

ドライバーは、デバイスオブジェクトを作成した後、いつでも[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出すことができます。 ほとんどのドライバーは、最初に*Evtdriverdeviceadd*コールバックからこのメソッドを呼び出しますが、これは常に可能であるか、望ましくない可能性があります。 ドライバーが複数のデバイスまたはデバイスのバージョンをサポートしている場合、ドライバーは、ハードウェアに対してクエリを行うまで、デバイスのすべての機能を認識しない可能性があります。 このようなドライバーは、 *EvtdeviceWdfDeviceAssignS0IdleSettings ハードウェア*コールバックまで、の呼び出しを延期できます。

[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を最初に呼び出した後、いつでも、ドライバーは、デバイスがアイドル状態するアイドルタイムアウト値とデバイスの状態を変更できます。 1つまたは複数の設定を変更するには、ドライバーは、前に説明したように、別の[**WDF\_デバイス\_電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)の構造体を初期化し、もう一度**WdfDeviceAssignS0IdleSettings**を呼び出します。

### <a href="" id="preventsusp"></a>USB デバイスの中断を防止する

場合によっては、タイムアウト期間内に i/o 要求が存在しない場合でも、USB デバイスの電源をオフにしないことがあります。通常、ハンドルがデバイスに対して開かれている場合や、デバイスが充電されている場合などです。 USB ドライバーを使用すると、 [**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)を呼び出し、デバイスの中断が許容される場合に[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)を呼び出すことによって、フレームワークがアイドル状態のデバイスを中断するのを防ぐことができます。

[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)は、アイドルタイマーを停止します。 **IdleTimeout**期間が終了しておらず、デバイスがまだ中断されていない場合、フレームワークはアイドルタイマーをキャンセルし、デバイスを中断しません。 デバイスが既に中断されている場合、フレームワークはデバイスを動作中の状態に戻します。 **Wdfdevicestopidle**では、システムが Sx スリープ状態に変更されたときに、フレームワークがデバイスを中断するのを防ぐことはできません。 その唯一の効果は、システムが S0 の動作状態にある間、デバイスが中断されないようにすることです。 [**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)は、アイドルタイマーを再起動します。 この2つの方法では、デバイスの参照カウントを管理します。したがって、ドライバーが**Wdfdevicestopidle**を複数回呼び出す場合、 **WdfDeviceResumeIdle**が同じ回数だけ呼び出されるまで、フレームワークはデバイスを中断しません。 最初に**Wdfdevicestopidle**を呼び出さないと、ドライバーは**WdfDeviceResumeIdle**を呼び出すことができません。

### <a name="including-a-registry-key-hid-drivers-only"></a>レジストリキーを含める (HID ドライバーのみ)

USB HID デバイス用の KMDF 上位フィルタードライバーは、HID スタックに対して、Microsoft が提供する HIDClass ポートドライバーが選択的中断を有効にできるように、選択的中断をサポートすることを INF で示す必要があります。 INF には、次の文字列に示すように、SelectiveSuspendEnabled キーを追加し、その値を1に設定する AddReg ディレクティブが含まれている必要があります。

```cpp
HKR,,"SelectiveSuspendEnabled",0x00000001,0x1
```

例については、WDK の inx にある% WinDDK%\\の\\Src\\Hid\\ Hidusbfx2\\sys の Hidusbfx2 を参照してください。

## <a name="remote-wake-support-for-kmdf-drivers"></a>KMDF ドライバーのリモートウェイクサポート


セレクティブサスペンドと同様に、KMDF ではウェイクアップのサポートが組み込まれているので、デバイスがアイドル状態で、システムが動作中 (S0) またはスリープ状態 (S1 ~ S4) にあるときに、USB デバイスがウェイクアップ信号をトリガーすることができます。 KMDF の用語では、これらの2つの機能はそれぞれ "S0 からの復帰" と "wake from Sx" と呼ばれます。

USB デバイスの場合、ウェイクアップは、デバイス自体が低電力状態から動作状態への移行を開始できることを示しているだけです。 したがって、USB 用語では、S0 からの復帰と Sx からのウェイクは同じであり、"リモートスリープ" と呼ばれます。

KMDF USB 関数ドライバーは、S0 からの復帰をサポートするコードを必要としません。 KMDF は、選択的中断メカニズムの一部としてこの機能を提供するためです。 ただし、システムが Sx にあるときにリモートスリープをサポートするには、関数ドライバーが次のことを行う必要があります。

-   [**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)を呼び出して、デバイスがリモートウェイクをサポートしているかどうかを確認します。
-   Wake 設定を初期化して[**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)を呼び出すことによって、リモートスリープを有効にします。

KMDF ドライバーでは、通常、 *Evtdriverdeviceadd*または*Evtdeviceのハードウェア*機能で USB セレクティブサスペンドのサポートを構成するときに、同時にウェイクアップサポートを構成します。

### <a name="checking-device-capabilities"></a>デバイスの機能を確認する

KMDF USB 関数ドライバーは、アイドル状態と復帰用に電源ポリシー設定を初期化する前に、デバイスがリモートスリープをサポートしていることを確認する必要があります。 デバイスのハードウェア機能に関する情報を取得するために、ドライバーは[**WDF\_USB\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_information)構造を初期化し、通常は Evtdriverdeviceadd で[**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)を呼び出します。または、*ハードウェア*コールバック。

[**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)を呼び出すと、ドライバーはデバイスオブジェクトへのハンドルと、初期化された[**WDF\_USB\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_information)構造体へのポインターを渡します。 関数から正常に返された場合、構造体の特徴フィールドには、デバイスの電源が入っているかどうかを示すフラグ、高速で動作すること、およびリモートスリープをサポートするフラグが含まれます。

Osrusbfx2 KMDF サンプルの次の例では、このメソッドを呼び出して、デバイスがリモートウェイクアップをサポートしているかどうかを確認する方法を示しています。 これらのコード行が実行された後、waitWakeEnable 変数には、デバイスがリモートウェイクアップをサポートしている場合は TRUE、それ以外の場合は FALSE が含まれます。

```cpp
    WDF_USB_DEVICE_INFORMATION          deviceInfo;
// Retrieve USBD version information, port driver capabilities and device
// capabilites such as speed, power, etc.
//

WDF_USB_DEVICE_INFORMATION_INIT(&deviceInfo);

status = WdfUsbTargetDeviceRetrieveInformation(
                            pDeviceContext->UsbDevice,
                            &deviceInfo);
waitWakeEnable = deviceInfo.Traits & WDF_USB_DEVICE_TRAIT_REMOTE_WAKE_CAPABLE;
```

### <a name="enabling-remote-wakeup"></a>リモートウェイクアップの有効化

USB 用語では、デバイス\_リモート\_ウェイクアップ機能が設定されている場合に、リモートウェイクアップに対して USB デバイスが有効になります。 USB 仕様によれば、ホストソフトウェアでは、デバイスをスリープ状態にするために、デバイスのリモートウェイクアップ機能を "直前" に設定する必要があります。 KMDF 関数ドライバーは、ウェイク設定を初期化するためにのみ必要です。 KMDF および Microsoft が提供する USB バスドライバーは、i/o 要求を発行し、リモートウェイクアップを有効にするために必要なハードウェア操作を処理します。

**ウェイク設定を初期化するには**

1.  [**WDF\_デバイス\_電源\_ポリシー\_wake\_settings\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_device_power_policy_wake_settings_init)を呼び出して、[**電源\_ポリシー\_wake\_settings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)構造体を初期化します。 この関数は、構造体の**有効な**メンバーを**Wdfusedefault**に設定し、 **dxstate**メンバーを**PowerDeviceMaximum**に設定し、 **UserControlOfWakeSettings**メンバーを**WakeAllowUserControl**に設定します。
2.  初期化された構造体を使用して[**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)を呼び出します。 その結果、デバイスは D3 状態から復帰できるようになり、ユーザーはデバイスマネージャーのデバイスプロパティページからウェイクアップ信号を有効または無効にすることができます。

Osrusbfx2 サンプルの次のコードスニペットは、ウェイク設定を既定値に初期化する方法を示しています。

```cpp
WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS wakeSettings;

WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS_INIT(&wakeSettings);
status = WdfDeviceAssignSxWakeSettings(Device, &wakeSettings);
if (!NT_SUCCESS(status)) {
    return status;
}
```

セレクティブサスペンドをサポートする USB デバイスの場合は、基になるバスドライバーによってデバイスハードウェアのスリープ状態が準備されます。 その結果、USB 関数ドライバーは、ほとんどの場合、 *EvtDeviceArmWakeFromS0*コールバックを必要としません。 フレームワークは、アイドルタイムアウトが経過したときに、セレクティブサスペンド要求を USB バスドライバーに送信します。

同じ理由から、USB 関数ドライバーは、 *EvtDeviceWakeFromS0Triggered*または*EvtDeviceWakeFromSxTriggered*コールバックを必要とすることはほとんどありません。 代わりに、フレームワークと基になるバスドライバーは、デバイスを動作状態に戻すためのすべての要件を処理します。

## <a name="related-topics"></a>関連トピック
[USB ドライバーでの選択的な中断 (WDF)](selective-suspend-in-usb-drivers-wdf.md)  



