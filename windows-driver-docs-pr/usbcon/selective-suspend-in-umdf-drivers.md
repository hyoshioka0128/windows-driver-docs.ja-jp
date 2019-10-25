---
Description: このトピックでは、UMDF 関数ドライバーが USB のセレクティブサスペンドをサポートするしくみについて説明します。
title: USB UMDF ドライバーでのセレクティブサスペンド
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 20d2e19907a706c980e3bce316b16f4c48ed3299
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824159"
---
# <a name="selective-suspend-in-usb-umdf-drivers"></a>USB UMDF ドライバーでのセレクティブサスペンド


**重要な API**

-   [**IWDFUsbTargetDevice:: SetPowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy)
-   [**IWDFDevice2::AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)
-   [**IWDFDevice2::AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)

このトピックでは、UMDF 関数ドライバーが USB のセレクティブサスペンドをサポートするしくみについて説明します。

UMDF 関数ドライバーでは、次の2つの方法のいずれかで、USB のセレクティブサスペンドをサポートできます。

-   電源ポリシーの所有権を要求し、デバイスのアイドル電力を処理し、再開します。
-   Microsoft が提供する WinUSB .sys ドライバーを使用して、選択的中断を処理します。 WinUSB .sys は、UMDF USB ドライバーのインストール中に、カーネルモードのデバイススタックの一部としてインストールされます。 WinUSB は、USB デバイス操作を中断および再開するための基盤となるメカニズムを実装します。

どちらの方法でも、少量のコードしか必要ありません。 WDK に用意されている IdleWake サンプルは、UMDF USB ドライバーでのセレクティブサスペンドをサポートする方法を示しています。 このサンプルは、% WinDDK%\\の\\Src\\Usb\\OsrUsbFx2\\ UMDF\\Fx2\_Driver\\IdleWake にあります。 このフォルダーには、サンプルの PPO と non PPO の両方のバージョンが含まれています。

セレクティブサスペンドをサポートする UMDF ドライバーは、次のガイドラインに従う必要があります。

-   UMDF ドライバーは、デバイススタックの電源ポリシーの所有権を要求できますが、そのためには必要ありません。 既定では、基になる WinUSB .sys ドライバーが電源ポリシーを所有しています。
-   選択的中断をサポートする UMDF ドライバー。 PPO では、電源管理キューまたは電源管理されていないキューを使用できます。 選択的中断をサポートするが、PPO ではない UMDF ドライバーは、電源管理キューを使用しないようにする必要があります。

## <a name="power-policy-ownership-in-umdf-usb-drivers"></a>UMDF USB ドライバーの電源ポリシーの所有権


既定では、WinUSB .sys は、UMDF USB ドライバーを含むデバイススタックの PPO です。 WDF 1.9 以降では、UMDF ベースの USB ドライバーが電源ポリシーの所有権を要求することができます。 PPO にできるドライバーはデバイススタックごとに1つだけなので、PPO である UMDF USB ドライバーでは、WinUSB. sys の電源ポリシーの所有権を明示的に無効にする必要があります。

**UMDF USB ドライバーで電源ポリシーの所有権を要求するには**

1.  **Iwdfdeviceinitialize:: SetPowerPolicyOwnership**を呼び出し、通常は、ドライバーコールバックオブジェクトの**Idriverentry:: ondeviceadd**メソッドから**TRUE**を渡します。 次に、例を示します。

    ``` syntax
    FxDeviceInit->SetPowerPolicyOwnership(TRUE);
    ```

2.  WinUSB で電源ポリシーの所有権を無効にします。 ドライバーの INF ファイルに、レジストリの**WinUsbPowerPolicyOwnershipDisabled**値を0以外の値に設定する**AddReg**ディレクティブを含めます。 **AddReg**ディレクティブは、DDINSTALL. HW セクションに記述する必要があります。 次に、例を示します。

    ``` syntax
    [MyDriver_Install.NT.hw]
    AddReg=MyDriver_AddReg

    [MyDriver_AddReg]
    HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
    ```

セレクティブサスペンドをサポートし、1.9 より前の WDF バージョンでビルドされた UMDF USB ドライバーは、電源ポリシーの所有権を要求しません。 これらの以前のバージョンの WDF では、USB の選択的中断は、WinUSB .sys が PPO の場合にのみ適切に機能します。

## <a name="io-queues-in-umdf-usb-drivers"></a>UMDF USB ドライバーの i/o キュー


選択的中断をサポートする UMDF ドライバーの場合、そのデバイスの電源ポリシーが UMDF ドライバーによって所有されているかどうかによって、使用できる i/o キューの種類が決まります。 選択的中断および PPOs をサポートする UMDF ドライバーでは、電源管理されているキューか、電源管理されていないキューを使用できます。 選択的中断をサポートするが、PPO ではない UMDF USB ドライバーは、電源管理の i/o キューを使用しないようにする必要があります。

デバイスが中断されている間に、電源管理キューに i/o 要求が到着した場合、ドライバーが PPO でない限り、フレームワークは要求を提示しません。これは、 [USB ドライバーのセレクティブサスペンド](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)のイメージに示されています。 UMDF ドライバーがデバイスの PPO でない場合、フレームワークはデバイスの代わりにデバイスの電源をオンにすることはできません。 その結果、要求は、電源管理キューでスタックされたままになります。 要求が WinUSB に到達しないため、WinUSB はデバイスの電源をオンにできません。 その結果、デバイススタックが停止する可能性があります。

キューが電源管理されていない場合、デバイスの電源がオフになっている場合でも、フレームワークは UMDF ドライバーに i/o 要求を提示します。 UMDF ドライバーは、要求をフォーマットし、通常の方法でデバイススタックから既定の i/o ターゲットに転送します。 特別なコードは必要ありません。 要求が PPO (WinUSB .sys) に達すると、WinUSB はデバイスを起動し、必要な i/o 操作を実行します。

**% WinDDK%\\の\\Src\\Usb\\OsrUsbFx2\\umdf\\Fx2\_driver\\IdleWake**のサンプルドライバーは、電源 \_ポリシー\_ない定数を定義\_"OWNER" は、非 PPO バージョンのドライバーをビルドするときに\_ ます。 ドライバーは、読み取り要求と書き込み要求のキューを作成するときに、定数をチェックすることによって、電源管理キューを作成するかどうかを決定します。

キューを作成するには、ドライバーによって定義された**CMyQueue:: Initialize**メソッドを呼び出します。このメソッドは、次の3つのパラメーターを受け取ります。

-   *DispatchType*は、キューが要求をディスパッチする方法を示す、WDF\_IO\_QUEUE\_DISPATCH\_TYPE 列挙値です。
-   *既定*値は、キューが既定のキューであるかどうかを示すブール値です。
-   *Powermanaged*。キューが電源管理されているかどうかを示すブール値です。

次のコードスニペットは、読み取り/書き込みキューの作成の一部として、ドライバーの**CMyQueue:: Initialize**メソッドの呼び出しを示しています。

```cpp
#if defined(_NOT_POWER_POLICY_OWNER_)
    powerManaged = false;
#else
    powerManaged = true;
#endif  
hr = __super::Initialize(WdfIoQueueDispatchParallel,
                         true,
                         powerManaged,
                         );
```

**CMyQueue:: Initialize**は、次のように、 [**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)を呼び出してキューを作成します。

```cpp
hr = m_FxDevice->CreateIoQueue(
                               callback,
                               Default,
                               DispatchType,
                               PowerManaged,
                               FALSE,
                               &fxQueue
                               );
```

このコードシーケンスは、要求を並列でディスパッチする既定のキューになります。 ドライバーが PPO の場合、キューは電源管理され、ドライバーが PPO でない場合、キューは電源管理されません。

## <a name="supporting-usb-selective-suspend-in-a-umdf-ppo"></a>UMDF PPO での USB 選択的中断のサポート


セレクティブサスペンドをサポートするために、デバイススタックの PPO である UMDF USB ドライバーは、次の操作を行う必要があります。

1.  前に説明したように、ドライバーコールバックオブジェクトの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドで、デバイススタックの電源ポリシーの所有権を要求します。
2.  フレームワークデバイスオブジェクトで[**IWDFDevice2:: AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)メソッドを呼び出して、選択的中断を有効にします。

**PPO から USB のセレクティブサスペンドを有効にするには**

-   [**IWDFDevice2:: AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)を呼び出します。通常は、デバイスコールバックオブジェクトの**代わっ hardware**メソッドから呼び出します。 次のように、パラメーターを AssignS0IdleSettings に設定します。
    -   *IdleCaps* **IdleUsbSelectiveSuspend**.
    -   *Dxstate*は、フレームワークがアイドル状態のデバイスを遷移するデバイスのスリープ状態になります。 USB のセレクティブサスペンドの場合は、 **PowerDeviceMaximum**を指定します。これは、バスドライバーで指定された値をフレームワークが使用する必要があることを示します。
    -   フレームワークが*Dxstate*に遷移する前に、デバイスがアイドル状態である必要があるミリ秒数に*IdleTimeout*します。
    -   UserControlOfIdleSettings は、ユーザーがアイドル設定を管理できる場合は**IdleAllowUserControl** 、それ以外の場合は**Id Onotallowusercontrol**に設定します。
    -   既定でセレクティブサスペンドを有効にし、ユーザー設定で既定値をオーバーライドできるようにするために、 **Wdfusedefault**に対し*て有効*にします。

次の例は、IdleWake\_PPO ドライバーが内部 CMyDevice:: SetPowerManagement メソッドでこのメソッドを呼び出す方法を示しています。

```cpp
hr = m_FxDevice->AssignS0IdleSettings( IdleUsbSelectiveSuspend,
                                PowerDeviceMaximum,
                                IDLE_TIMEOUT_IN_MSEC,
                                IdleAllowUserControl,
                                WdfUseDefault);                                                                                                   
```

デバイスハードウェアがウェイクアップ信号を生成できる場合、UMDF ドライバーは S1、S2、または S3 からのシステムウェイクもサポートできます。 詳細については、「 [UMDF ドライバーでのシステムのスリープ解除](#system-wake-in-a-umdf-driver)」を参照してください。

## <a name="supporting-usb-selective-suspend-in-a-non-ppo-umdf-driver"></a>PPO 以外の UMDF ドライバーでの USB 選択的中断のサポート


PPO 以外の UMDF 関数ドライバーは、基になる WinUSB .sys ドライバーの機能を使用して、選択的中断をサポートできます。 UMDF ドライバーは、デバイスとドライバーが選択的中断をサポートしていること、および INF ファイルで選択的な中断を有効にするか、USB ターゲットデバイスオブジェクトの電源ポリシーを設定する必要があることを WinUSB に通知する必要があります。

UMDF 関数ドライバーで選択的中断が有効になっている場合、基になる WinUSB .sys ドライバーによってデバイスがアイドル状態になっていることが判断されます。 WinUSB は、保留中の転送がない場合、または保留中の転送のみが割り込みまたは一括エンドポイントで転送される場合に、アイドルタイムアウトカウンターを開始します。 既定では、アイドルタイムアウトは5秒ですが、UMDF ドライバーはこの既定値を変更できます。

WinUSB によってデバイスがアイドル状態であると判断された場合は、デバイスを中断する要求をカーネルモードのデバイススタックに送信します。 バスドライバーは、ハードウェアの状態を必要に応じて変更します。 ポートのすべてのデバイス機能が中断されている場合は、USB のセレクティブサスペンドの状態になります。

デバイスが中断されているときに、WinUSB .sys に i/o 要求が到着した場合、デバイスが要求を処理するために電源をオンにする必要がある場合、WinUSB はデバイスの操作を再開します。 UMDF ドライバーでは、システムが S0 を受けている間にデバイスを再開するコードは必要ありません。 デバイスハードウェアがウェイクアップ信号を生成できる場合、UMDF ドライバーは S1、S2、または S3 からのシステムウェイクもサポートできます。 詳細については、「 [UMDF ドライバーでのシステムのスリープ解除](#system-wake-in-a-umdf-driver)」を参照してください。

PPO 以外の UMDF ドライバーは、次の2つの手順を実行することで、選択的中断をサポートできます。

1.  デバイスとドライバーが選択的中断をサポートしていることを WinUSB に通知します。
2.  USB セレクティブサスペンドを有効にしています。

また、ドライバーは必要に応じて次のことができます。

-   デバイスのタイムアウト値を設定します。
-   ユーザーが選択的中断を有効または無効にすることを許可します。

PPO 以外の UMDF USB 関数ドライバーで USB セレクティブサスペンドを実装する方法の例については、WDK の Fx2\_Driver サンプルを参照してください。 このサンプルは、 **% WinDDK%\\の\\Src\\Usb\\OsrUsbFx2\\Umdf\\Fx2\_Driver\\ IdleWake\_非 PPO**にあります。

**セレクティブサスペンドのサポートについて WinUSB に通知するには**

デバイスが USB のセレクティブサスペンドをサポートできることを WinUSB に通知するには、デバイスの INF がデバイスのハードウェアキーに DeviceIdleEnabled 値を追加し、値を1に設定する必要があります。 次の例は、Fx2\_ドライバーのサンプルで、WUDFOsrUsbFx2\_IdleWakeNon ファイルにこの値を追加して設定する方法を示しています。

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"DeviceIdleEnabled",0x00010001,1
```

**USB のセレクティブサスペンドを有効にするには**

UMDF USB ドライバーは、実行時または INF でのインストール中に、USB のセレクティブサスペンドを有効にすることができます。

-   実行時にサポートを有効にするために、関数ドライバーは[**IWDFUsbTargetDevice:: SetPowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy)を呼び出し、PolicyType パラメーターを AUTO\_SUSPEND に設定し、Value パラメーターを TRUE または1に設定します。 次の例では、Fx2\_Driver サンプルで DeviceNonPpo .cpp ファイルのセレクティブサスペンドを有効にする方法を示します。
    ```cpp
    BOOL AutoSuspend = TRUE;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( AUTO_SUSPEND,
                                              sizeof(BOOL),
                                             (PVOID) &AutoSuspend );
    ```

-   インストール中にサポートを有効にするために、INF には AddReg ディレクティブが含まれています。このディレクティブは、デバイスのハードウェアキーに DefaultIdleState 値を追加し、値を1に設定します。 次に、例を示します。
    ```cpp
    HKR,,"DefaultIdleState",0x00010001,1
    ```

**アイドル状態のタイムアウト値を設定するには**

既定では、転送が保留されていない場合、または保留中の転送のみが割り込みまたは一括エンドポイントで転送される場合、WinUSB は5秒後にデバイスを中断します。 UMDF ドライバーは、INF または実行時のインストール時に、このアイドルタイムアウト値を変更できます。

-   インストール時にアイドルタイムアウトを設定するために、INF には AddReg ディレクティブが含まれています。このディレクティブは、デバイスのハードウェアキーに DefaultIdleTimeout 値を追加し、その値をミリ秒単位のタイムアウト間隔に設定します。 次の例では、タイムアウトを7秒に設定します。
    ```cpp
    HKR,,"DefaultIdleTimeout",0x00010001,7000
    ```

-   実行時にアイドルタイムアウトを設定するために、ドライバーは**IWDFUsbTargetDevice:: SetPowerPolicy**を PolicyType に設定して、遅延と値をアイドルタイムアウト値 (ミリ秒単位) に\_設定します。 次の例では、Fx2\_Driver サンプルによって、タイムアウトが10秒に設定されています。
    ```cpp
    HRESULT hr;
    ULONG value;
    value = 10 * 1000;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( SUSPEND_DELAY,
                                              sizeof(ULONG),
                                             (PVOID) &value );
    ```

**USB のセレクティブサスペンドをユーザーが制御できるようにするには**

WinUSB 選択的中断サポートを使用する UMDF USB ドライバーでは、オプションで、ユーザーが選択的中断を有効または無効にすることを許可できます。 これを行うには、AddReg ディレクティブを INF に追加します。このディレクティブは、デバイスのハードウェアキーに UserSetDeviceIdleEnabled 値を追加し、値を1に設定します。 AddReg ディレクティブに使用する文字列を次に示します。

```cpp
HKR,,"UserSetDeviceIdleEnabled",0x00010001,1
```

UserSetDeviceIdleEnabled が設定されている場合、デバイスの [プロパティ] ダイアログボックスに [電源管理] タブが表示され、ユーザーは USB のセレクティブサスペンドを有効または無効にすることができます。

## <a name="system-wake-in-a-umdf-driver"></a>UMDF ドライバーでのシステムのスリープ解除


UMDF ドライバーでは、システム wake のサポートは、選択的中断のサポートに依存しません。 UMDF USB ドライバーでは、システムの wake とセレクティブ suspend の両方をサポートできます。システムウェイクとセレクティブサスペンドの両方をサポートしていないか、システムの wake またはセレクティブサスペンドをサポートしています。 システムウェイクアップをサポートするデバイスは、スリープ状態 (S1、S2、または S3) からシステムをウェイクアップできます。

UMDF USB PPO ドライバーは、フレームワークのドライバーオブジェクトのウェイクアップ情報を提供することによって、システムのスリープ状態をサポートできます。 外部イベントによってシステムのスリープ状態がトリガーされると、フレームワークはデバイスを動作中の状態に戻します。

USB 非 PPO ドライバーは、WinUSB .sys ドライバーが実装するシステムのウェイクアップサポートを使用できます。

**PPO である UMDF USB ドライバーでシステムのスリープ状態をサポートするには**

次のパラメーターを使用して、フレームワークの device オブジェクトに対して[**IWDFDevice2:: AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)メソッドを呼び出します。

-   *Dxstate*は、システムがウェイクアップされた Sx 状態になったときにデバイスが移行する電源状態になります。 USB デバイスの場合は、バスドライバーによって指定された値を使用するように**PowerDeviceMaximum**を指定します。
-   *UserControlOfWakeSettings*は、ユーザーがウェイクアップ設定を管理できる場合は**WakeAllowUserControl**に、それ以外の場合は WakeDoNotAllowUserControl に設定し**ます。**
-   **Wdfusedefault**が*有効になり*、既定でウェイクが有効になります。ただし、ユーザー設定で既定値を上書きできます。

次の例は、IdleWake\_PPO ドライバーが内部**CMyDevice:: SetPowerManagement**メソッドでこのメソッドを呼び出す方法を示しています。

```cpp
hr = m_FxDevice->AssignSxWakeSettings( PowerDeviceMaximum,
                                       WakeAllowUserControl,
                                       WdfUseDefault);
```

**PPO 以外のドライバーで WinUSB を使用してシステムのスリープ状態を有効にするには**

WinUSB を使用したシステムのスリープ状態を有効にするために、ドライバーの INF は、レジストリ値 SystemWakeEnabled をデバイスのハードウェアキーに追加し、それを1に設定します。 IdleWake\_以外の PPO サンプルでは、次のようにシステムウェイクが有効になります。

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"SystemWakeEnabled",0x00010001,1
```

この値を設定すると、ドライバーによってシステムウェイクが有効になり、ユーザーはデバイスがシステムをスリープ解除する機能を制御できるようになります。 デバイスマネージャーでは、デバイスの [電源管理の設定] プロパティページには、ユーザーがシステムのスリープ解除を有効または無効にするためのチェックボックスがあります。

## <a name="related-topics"></a>関連トピック
[USB ドライバーでの選択的な中断 (WDF)](selective-suspend-in-usb-drivers-wdf.md)  



