---
Description: このトピックでは、KMDF 関数ドライバー サポート USB のセレクティブを中断する方法について説明します。
title: USB KMDF 機能ドライバーにおけるセレクティブ サスペンド
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: bf0c54bb18bf38cd52966274b68e335b729c0199
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358341"
---
# <a name="selective-suspend-in-usb-kmdf-function-drivers"></a>USB KMDF 機能ドライバーにおけるセレクティブ サスペンド


**重要な API**

-   [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)
-   [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)
-   [**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)

このトピックでは、KMDF 関数ドライバー サポート USB のセレクティブを中断する方法について説明します。

機能またはユーザー モードでは使用できないリソースが、USB ドライバーが必要な場合は、KMDF 関数ドライバーを指定する必要があります。 選択的 KMDF ドライバーの実装は、KMDF 初期化構造体で関連する値を設定し、適切なコールバック関数を指定して中断します。 KMDF 中断およびデバイスを再開する下位のドライバーとの通信の詳細を処理します。

## <a name="guidelines-for-selective-suspend-in-kmdf-drivers"></a>ガイドラインの選択的 KMDF ドライバーで中断


選択的なサポートを中断 KMDF ドライバーは、次のガイドラインに従う必要があります。

-   KMDF ドライバー関数は、そのデバイス スタックの PPO である必要があります。 既定では、KMDF 関数ドライバーは、PPO が。
-   選択的なサポートを中断する KMDF 関数ドライバーには、電源管理の対象のキューまたは電源管理の対象でないキューを使用できます。 既定では、PPOs のキュー オブジェクトは、電源管理の対象をします。

**電源ポリシー所有権と KMDF の USB ドライバー**

既定では、USB デバイスの KMDF 関数ドライバーは、デバイス スタックの PPO が。 KMDF は選択的に管理中断し、このドライバーの代わりに再開します。

**KMDF ドライバーでの I/O キューの構成**

選択的なサポートを中断する KMDF 関数ドライバーには、電源管理の対象のキューまたは電源管理の対象でないキューを使用できます。 通常、ドライバーは、電源管理デバイス I/O 制御要求の受信にではなく、読み取り、書き込み、およびその他の電源に依存する要求を受信する 1 つまたは複数の電源管理キューを構成するキューを構成します。 電源管理対象のキューに到着すると、要求、KMDF により、デバイスは、ドライバーに要求を表示する前に D0 では。

デバイス スタックで PPO の上に配置する KMDF フィルター ドライバーを作成する場合は、電源管理対象のキューを使用する必要があります。 理由は、UMDF ドライバーの場合と同じです。 フレームワークではありません電源管理対象のキューからの要求、デバイスが中断されている間ため、このようなキューを使用停止デバイス スタックする可能性があります。

## <a name="selective-suspend-mechanism-for-kmdf-function-drivers"></a>セレクティブ サスペンド KMDF 関数ドライバーのメカニズム


KMDF ハンドルのほとんどの USB のセレクティブをサポートするために必要な作業を中断します。 I/O アクティビティの追跡、アイドル状態のタイマーを管理し、デバイス (Usbhub.sys またはで、Usbccgp.sys) 中断およびデバイスを再開する親ドライバーにより、I/O 制御の要求を送信します。

KMDF 関数のドライバー サポート オプションを選択する場合は、中断、KMDF は各デバイス オブジェクトを所有するすべての電源管理対象のキューの I/O アクティビティの追跡。 フレームワークでは、I/O の数がゼロに達するたびに、アイドル タイマが起動します。 既定のタイムアウト値は、5 秒です。

アイドル タイムアウト期間が切れる前に、デバイス オブジェクトに属している電源管理対象のキューに、I/O 要求が到着すると、フレームワークはアイドル タイマーをキャンセルし、デバイスを一時停止しません。

アイドル タイマーの期限が切れると、KMDF は中断状態に USB デバイスを配置するために必要な要求を発行します。 関数のドライバーでは、USB エンドポイントで継続的なリーダーを使用している場合、リーダーの繰り返されるポーリングは方向 KMDF アイドル タイマー アクティビティとしてはカウントされません。 ただしでは、 [ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)コールバック関数では、USB ドライバーを手動で停止、継続的なリーダーおよび電源管理のことを確認する対象でないキューによって供給される他の I/O ターゲット、ドライバーは、デバイスが稼働状態にないときに、I/O 要求を送信しません。 ターゲットをドライバーの呼び出しを停止する[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)指定と**WdfIoTargetWaitForSentIoToComplete**対象となるアクションとして。 応答では、フレームワークは、ターゲットの I/O キュー内にあるすべての I/O 要求が完了し、関連するすべてのコールバックが実行された I/O の完了後にのみに I/O ターゲットを停止します。

既定では、KMDF は D0 からデバイスがアイドル状態の設定で、ドライバーが指定されているデバイスの電源状態に遷移します。 移行の一環として、KMDF が別の電源切断シーケンスの場合と同様に、ドライバーの電源のコールバック関数を呼び出します。

デバイスが中断された後に、フレームワークで、次のイベントのいずれかが発生した場合、デバイスが自動的に再開します。

-   ドライバーの電源管理対象のキューのいずれかの I/O 要求が到着します。
-   ユーザーが USB のセレクティブを無効にしますが、デバイス マネージャーを使用して中断します。
-   ドライバー呼び出し[ **WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)」の説明に従って、[デバイス中断の防止](#preventsusp)します。

デバイスを再開するには、KMDF はデバイス スタックの電源投入要求を送信し、別の電源投入シーケンスの場合と同様に、ドライバーのコールバック関数を呼び出します。

電源オフ、電源投入シーケンスに関連するコールバックの詳細については、次を参照してください。、[プラグ アンド プレイと WDF ドライバーでの電源管理](http://download.microsoft.com/download/5/d/6/5d6eaf2b-7ddf-476b-93dc-7cf0072878e6/WDF-pnpPower.docx)ホワイト ペーパー。

## <a name="supporting-usb-selective-suspend-in-a-kmdf-function-driver"></a>KMDF ドライバーで関数を中断 USB のセレクティブをサポートしています。


実装するには、関数 KMDF ドライバーで USB のセレクティブが中断します。

-   アイドル状態などのアイドル タイムアウトに関連する電源ポリシー設定を初期化します。
-   必要に応じて一時的に中断を防ぐため、または、ドライバーは、デバイスが開いているハンドルまたはデバイスの I/O キューに関連付けられていないその他の理由により中断されていない必要がありますが判断した場合、操作を再開するためのロジックが含まれます。
-   USB ドライバーの選択的にサポートしていること、INF でヒューマン インターフェイス デバイス (HID) を示しますが中断します。

**KMDF ドライバーでは関数の電源ポリシー設定を初期化しています**

USB のセレクティブ サスペンドのサポートを構成する KMDF ドライバーを使用して、 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体。 ドライバーは、まず、構造体を初期化する必要があり、ドライバーとそのデバイスの機能の詳細を提供するフィールドを設定できます。 この構造体でのドライバーが通常は、その*EvtDriverDeviceAdd*または*EvtDevicePrepareHardware*関数。

**WDF を初期化するために\_デバイス\_POWER\_ポリシー\_IDLE\_設定の構造体**

ドライバーを使用して、ドライバーでは、デバイス オブジェクトが作成された後、 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)関数、構造体を初期化します。 この関数は、2 つの引数を受け取ります。

-   ポインター、 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造体を初期化します。
-   サポートを示す列挙値を選択的な中断します。 ドライバーを指定する必要があります**IdleUsbSelectiveSuspend**します。

ドライバーが指定されている場合**IdleUsbSelectiveSuspend**関数は次のように、構造体のメンバーを初期化します。

-   **IdleTimeout**に設定されている**IdleTimeoutDefaultValue** (現在 5000 ミリ秒または 5 秒)。
-   **UserControlOfIdleSettings**に設定されている**IdleAllowUserControl**します。
-   **有効になっている**に設定されている**WdfUseDefaul**t で、その選択的に示すの中断が有効になってがユーザーと無効にできますが、 **UserControlOfIdleSettings**メンバーが許可されています。
-   **DxState**に設定されている**PowerDeviceMaximum**デバイスの報告される電源機能を使用して、アイドル状態のデバイスに移行するときの状態を確認します。

**USB のセレクティブの中断を構成するには**

ドライバーが初期化された後、 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造、ドライバーを設定できます他のフィールドの構造と、呼び出しに**WdfDeviceAssignS0IdleSettings**フレームワークにこれらの設定を渡す。 次のフィールドは、USB ドライバーが関数に適用されます。

-   IdleTimeout: 間隔 (ミリ秒) フレームワークでは、アイドル状態のデバイスが考慮する前に、I/O 要求を受け取らずに経過する必要があります。 ドライバーは ULONG 値を指定できますか、既定値を確認できます。
-   UserControlOfIdleSettings-ユーザーがデバイスのアイドル状態の設定を変更するかどうか。 使用可能な値には、IdleDoNotAllowUserControl および IdleAllowUserControl です。
-   DxState-デバイスの電源状態をフレームワークには、デバイスが中断します。 指定できる値は、PowerDeviceD1、PowerDeviceD2、および PowerDeviceD3 は。

    USB ドライバーでは、この値の初期設定は変更しないでください。 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)関数では、この値を設定するにはPowerDeviceMaximum により、フレームワークがデバイスの機能に基づく適切な値を選択します。

次のコード スニペットでは、Osrusbfx2 サンプル ドライバーの Device.c ファイルからです。

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

例では、ドライバーが呼び出す[ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdf_device_power_policy_idle_settings_init)、指定する**IdleUsbSelectiveSuspend**します。 ドライバー セット**IdleTimeout** 10,000 ミリ秒 (10 秒) に、フレームワークの既定値を受け入れる**DxState**と**UserControlOfIdleSettings**します。 その結果がアイドル状態に管理者特権を持つユーザーを有効にするか、デバイスのアイドル状態のサポートを無効にできるようにする、デバイス マネージャーのプロパティ ページが作成されると、フレームワークは D3 の状態にデバイスを移行します。 ドライバーを呼び出して[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)をアイドル状態のサポートを有効にし、これらの設定をフレームワークに登録します。

ドライバーを呼び出すことができます[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)のどの時点後、デバイス オブジェクトを作成します。 ほとんどのドライバーから最初にこのメソッドの呼び出しは、 *EvtDriverDeviceAdd*コールバック、これが必ずしも不可能または不適切もします。 ドライバーは、複数のデバイスまたはデバイスのバージョンをサポートする場合、ドライバー知らないことがありますすべてのデバイス機能、ハードウェアのクエリを実行するまでです。 呼び出し元を延期できるは、このようなドライバー **WdfDeviceAssignS0IdleSettings**まで、 *EvtDevicePrepareHardware*コールバック。

呼び出し後、最初に、いつでも[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)ドライバーは、アイドル タイムアウト値と、デバイスがアイドル状態、デバイスの状態を変更できます。 1 つまたは複数の設定を変更するドライバーだけを初期化します別[ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)前述のように構造と呼び出し**WdfDeviceAssignS0IdleSettings**もう一度です。

### <a href="" id="preventsusp"></a>USB デバイスの中断の防止

場合によっては、USB デバイスがないの電源を切断 I/O 要求がタイムアウト期間内に存在しない場合でも、通常ときにハンドルが開いて、デバイスにかデバイスが充電中です。 USB ドライバーがから呼び出すことによって、このような状況でアイドル状態のデバイスを中断するフレームワークを防ぐため[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)を呼び出すと[ **WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)もう一度もかまわない場合、デバイスが中断されます。

[**WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)アイドル タイマーを停止します。 場合、 **IdleTimeout**期間の有効期限が切れていない、デバイスが中断されていないと、フレームワークは、アイドル タイマーをキャンセルし、デバイスを一時停止しません。 デバイスがまだ中断されている場合、フレームワークは稼働状態にデバイスを返します。 **WdfDeviceStopIdle**Sx スリープ状態にシステムが変更されたときに、デバイスを中断してから、フレームワークができません。 その唯一の影響は、システムの S0 作業状態のときに、デバイスの中断を防ぐためには。 [**WdfDeviceResumeIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)アイドル タイマーを再起動します。 これら 2 つのメソッド、デバイス上の参照カウントを管理するため、ドライバーは呼び出しが**WdfDeviceStopIdle**を複数回フレームワークを一時停止しません、デバイス ドライバーが呼び出されるまで**WdfDeviceResumeIdle**同じ回数。 ドライバーを呼び出してはならない**WdfDeviceResumeIdle**最初に呼び出さず**WdfDeviceStopIdle**します。

### <a name="including-a-registry-key-hid-drivers-only"></a>レジストリ キー (HID ドライバーのみ) を含む

KMDF 上部のフィルター ドライバーのサポート オプションを選択している、INF で示す必要があります USB HID デバイスを中断できるように、Microsoft 提供の HIDClass.sys ポート ドライバーが選択的に有効にできますが、HID スタックの中断します。 INF は、SelectiveSuspendEnabled キーを追加する AddReg ディレクティブを含めるし、文字列を次に示すように 1、その値を設定する必要があります。

```cpp
HKR,,"SelectiveSuspendEnabled",0x00000001,0x1
```

例については、Hidusbfx2.inx WinDDK % に wdk を参照してください。\\BuildNumber\\Src\\Hid\\ Hidusbfx2\\sys です。

## <a name="remote-wake-support-for-kmdf-drivers"></a>KMDF ドライバー リモート ウェイクのサポート


選択的に次のように suspend、KMDF は、USB デバイスは、デバイスがアイドル状態であり、システムが動作状態 (S0) または状態 (S1 ~ S4) ウェイク信号をトリガーできるようにスリープ解除時サポートを組み込みます。 KMDF 言うと、これら 2 つの機能と呼ばれます「S0 からのスリープ解除」と「Sx, からの復帰」それぞれします。

USB デバイスの場合、デバイス自体が低電力状態から作業状態への移行を開始できることをウェイク アップはだけで示します。 そのための USB 用語で S0 からのスリープ解除 Sx からの復帰、同じとは「リモート ウェイク アップ」と呼ばれます

KMDF の USB 機能ドライバーでは、KMDF が機構を中断する、選択的の一部として、この機能を提供するために S0 からのスリープ解除をサポートするためのコードは必要ありません。 ただし、システムが Sx ときをリモート ウェイク アップをサポートする関数のドライバーが必要です。

-   呼び出すことによって、デバイスがリモート ウェイク アップをサポートしているかどうか確認[ **WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)します。
-   ウェイク アップの設定の初期化と呼び出し元によってリモート ウェイクを有効にする[ **WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)します。

KMDF ドライバーでの USB のセレクティブ サスペンドのサポートを構成すると同時にスリープ解除のサポートを構成する通常の*EvtDriverDeviceAdd*または*EvtDevicePrepareHardware*関数。

### <a name="checking-device-capabilities"></a>デバイスの機能のチェック

KMDF の USB 機能ドライバーを初期化します、電源ポリシーの設定のアイドル状態しスリープ解除、デバイスがリモート ウェイク アップをサポートしていることを確認する必要があります。 デバイスのハードウェア機能に関する情報を取得するには、ドライバーを初期化します、 [ **WDF\_USB\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_device_information)構造と呼び出し[ **WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)では通常、その*EvtDriverDeviceAdd*または*EvtDevicePrepareHardware*コールバック。

呼び出しで[ **WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)、ドライバーがデバイス オブジェクトを初期化されたへのポインター、ハンドルを渡します[ **WDF\_USB\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_device_information)構造体。 関数の成功時に、構造体の特徴のフィールドは、デバイスが自己供給型かどうかを示すフラグが含まれています、高速、およびサポートするリモート ウェイクで動作できます。

Osrusbfx2 KMDF サンプルから次の例では、デバイスがリモート ウェイク アップをサポートするかどうかを確認するには、このメソッドを呼び出す方法を示します。 これらの行のコードを実行すると、waitWakeEnable 変数には、デバイスをサポートしない場合はリモート ウェイクと FALSE の場合に、TRUE が含まれています。

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

### <a name="enabling-remote-wakeup"></a>リモート ウェイク アップを有効にします。

リモート ウェイク アップの USB 用語では、USB デバイスが有効なときにそのデバイス\_リモート\_ウェイク アップ機能が設定されます。 USB 仕様では、ホスト ソフトウェアは、「のみだけ前」に、デバイスを配置することをスリープ状態のデバイスにリモート ウェイク アップ機能を設定する必要があります。 ウェイク アップの設定を初期化するためにのみ、KMDF 関数ドライバーが必要です。 KMDF と Microsoft 提供の USB バス ドライバー、I/O 要求を発行したり、リモート ウェイク アップを有効にするために必要なハードウェアの操作を処理します。

**ウェイク アップの設定を初期化するには**

1.  呼び出す[ **WDF\_デバイス\_POWER\_ポリシー\_WAKE\_設定\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdf_device_power_policy_wake_settings_init)初期化するために、 [**WDF\_デバイス\_POWER\_ポリシー\_WAKE\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)構造体。 この関数の設定、構造体の**有効**メンバー **WdfUseDefault**、設定、 **DxState**メンバー **PowerDeviceMaximum**と設定、 **UserControlOfWakeSettings**メンバー **WakeAllowUserControl**します。
2.  呼び出す[ **WdfDeviceAssignSxWakeSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)初期化された構造体。 その結果、D3 状態からスリープ解除するデバイスが有効になっていると、ユーザーが有効にするまたはデバイス マネージャーでのデバイス プロパティ ページからウェイク信号を無効にできます。

サンプルは、初期化する方法を示します Osrusbfx2 から次のコード スニペットは、既定値に設定をスリープ解除します。

```cpp
WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS wakeSettings;

WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS_INIT(&wakeSettings);
status = WdfDeviceAssignSxWakeSettings(Device, &wakeSettings);
if (!NT_SUCCESS(status)) {
    return status;
}
```

選択的なサポートを中断する USB デバイスの場合は、基になるバス ドライバーは、スリープ解除するデバイスのハードウェアを準備します。 USB 機能ドライバーがほとんど必要とその結果、 *EvtDeviceArmWakeFromS0*コールバック。 フレームワークは、アイドル タイムアウトの期限が切れると、USB バス ドライバーにセレクティブ サスペンドの要求を送信します。

同じ理由で、USB 機能ドライバーがほとんど必要とする*EvtDeviceWakeFromS0Triggered*または*EvtDeviceWakeFromSxTriggered*コールバック。 代わりに、フレームワークと基になるバス ドライバーは、デバイスを動作状態に戻すのすべての要件を処理します。

## <a name="related-topics"></a>関連トピック
[USB drivers (WDF) でのセレクティブ サスペンドします。](selective-suspend-in-usb-drivers-wdf.md)  



