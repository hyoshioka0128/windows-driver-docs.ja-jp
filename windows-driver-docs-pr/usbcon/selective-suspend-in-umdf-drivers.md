---
Description: This topic describes how UMDF function drivers support USB selective suspend.
title: USB UMDF ドライバーでのセレクティブ サスペンドします。
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e8103a70187fdac429671a5b6296edd8e314cfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572608"
---
# <a name="selective-suspend-in-usb-umdf-drivers"></a>USB UMDF ドライバーでのセレクティブ サスペンドします。


**重要な API**

-   [**IWDFUsbTargetDevice::SetPowerPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff560385)
-   [**IWDFDevice2::AssignSxWakeSettings**](https://msdn.microsoft.com/library/windows/hardware/ff556923)
-   [**IWDFDevice2::AssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff556920)

このトピックでは、UMDF 関数のドライバー サポート USB のセレクティブを中断する方法について説明します。

UMDF 関数ドライバーは、USB のセレクティブをサポートできる 2 つの方法のいずれかで中断します。

-   電源ポリシーを主張してアイドル状態の電源の所有権とデバイスを処理し、再開します。
-   WinUSB.sys ドライバーを依存することで、選択的に処理するために、マイクロソフトが提供するが中断します。 WinUSB.sys は、UMDF USB ドライバーのインストール中に、カーネル モード デバイス スタックの一部としてインストールされます。 WinUSB.sys の中断と再開の USB デバイスの操作の基になるメカニズムを実装します。

どちらの方法では、少量のコードのみが必要です。 WDK で提供される IdleWake サンプルをサポートする方法を選択的に示しています、UMDF USB ドライバーを中断します。 このサンプルは、%winddk で確認できます\\BuildNumber\\Src\\Usb\\OsrUsbFx2\\ UMDF\\Fx2\_ドライバー\\IdleWake します。 フォルダーには、PPO と PPO 以外のバージョンのサンプルの両方が含まれています。

選択的なサポートを中断 UMDF ドライバーは、次のガイドラインに従う必要があります。

-   UMDF ドライバーでは、そのデバイス スタックの電源ポリシーの所有権を主張することができますが、そう必要はありません。 既定では、基になる WinUSB.sys ドライバーには、電源ポリシーが所有しています。
-   サポート オプションを選択する UMDF ドライバーは中断し、電源管理対象のキューまたはキューを電源管理されていない、PPO を使用できます。 サポート オプションを選択する UMDF ドライバーでは、中断が、電源管理対象のキューを使用する必要があります、PPO ではありません。

## <a name="power-policy-ownership-in-umdf-usb-drivers"></a>UMDF USB ドライバーでの電源ポリシーの所有権


既定では、WinUSB.sys は UMDF USB ドライバーを含むデバイス スタックの PPO です。 WDF 1.9 以降、UMDF に基づく USB ドライバーは、電源ポリシーの所有権を要求できます。 各デバイス スタックの 1 つだけのドライバー、PPO 使用できる、ので、PPO UMDF USB ドライバー WinUSB.sys で電源ポリシーの所有権を無効に明示的にする必要があります。

**UMDF USB ドライバーの電源ポリシーの所有権を要求**

1.  呼び出す**IWDFDeviceInitialize::SetPowerPolicyOwnership**渡します**TRUE**から通常、 **IDriverEntry::OnDeviceAdd**ドライバー コールバック オブジェクトのメソッド。 以下に例を示します。

    ``` syntax
    FxDeviceInit->SetPowerPolicyOwnership(TRUE);
    ```

2.  WinUSB で電源ポリシーの所有権を無効にします。 ドライバーの INF ファイルに含める、 **AddReg**を設定するディレクティブ、 **WinUsbPowerPolicyOwnershipDisabled** 0 以外の値をレジストリ内の値。 **AddReg**ディレクティブが DDInstall.HW セクションに表示する必要があります。 例:

    ``` syntax
    [MyDriver_Install.NT.hw]
    AddReg=MyDriver_AddReg

    [MyDriver_AddReg]
    HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
    ```

サポート オプションを選択する UMDF USB ドライバーを中断し、1.9 が電源ポリシーの所有権を主張する必要がありますよりも早く WDF のバージョンで構築されます。 WDF、以前のバージョンで USB のセレクティブは、WinUSB.sys が、PPO 場合にのみ正しく動作を中断します。

## <a name="io-queues-in-umdf-usb-drivers"></a>USB の UMDF ドライバーでの I/O キュー


選択的にサポートする UMDF ドライバーの中断、UMDF ドライバーでは、そのデバイスの電源ポリシーは、使用可能な I/O キューの種類を決定します。 所有しているかどうか。 選択的にサポートする UMDF ドライバーを中断しは PPOs は電源管理の対象または電源管理の対象ではないキューを使用できます。 サポート オプションを選択する UMDF USB ドライバーでは、中断が、電源管理対象の I/O キューを使用しないでください、PPO ではありません。

デバイスが中断されている間は、電源管理対象のキューの I/O 要求が到着した、フレームワークが存在しない場合、要求、ドライバーは PPO、しない限りで図のように、 [USB ドライバーでのセレクティブ サスペンド](https://msdn.microsoft.com/library/windows/hardware/dn449739)します。 UMDF ドライバーでない場合、デバイスの PPO フレームワークは、自身のためにデバイスを電源ことはできません。 その結果、要求は、電源管理対象のキューにとどまります。 要求には、デバイスに電源を WinUSB できませんので、WinUSB に到達しません。 その結果、デバイス スタックが停止することができます。

キューが電源管理の対象でない場合、デバイスの電源を切るときでも、framework I/O 要求 UMDF ドライバーを表示します。 UMDF ドライバーでは、要求をフォーマットして、通常の方法でデバイス スタックを既定の I/O ターゲットに転送します。 特別なコードは必要ありません。 要求には、PPO (WinUSB.sys) に達すると、WinUSB.sys はデバイスを補強し、必要な I/O 操作を実行します。

サンプル ドライバー **%winddk\\BuildNumber\\Src\\Usb\\OsrUsbFx2\\umdf\\Fx2\_ドライバー\\IdleWake**定数を定義\_いない\_POWER\_ポリシー\_所有者\_PPO 以外のバージョンのドライバーをビルドする場合。 ドライバーの読み取りキューの作成し、書き込みを要求することを決定します定数に対してオンにして電源管理対象のキューを作成するかどうか。

ドライバーがドライバーの定義を呼び出して、キューを作成する**CMyQueue::Initialize**メソッドで、次の 3 つのパラメーターを受け取ります。

-   *DispatchType*、WDF\_IO\_キュー\_ディスパッチ\_キューが要求をディスパッチする方法を示す型の列挙値。
-   *既定*キューが既定のキューであるかどうかを示すブール値。
-   *PowerManaged*キューが電源管理の対象であるかどうかを示すブール値。

次のコード スニペットは、ドライバーの呼び出しを示しています、 **CMyQueue::Initialize**読み取り/書き込みキューの作成の一部としてメソッド。

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

**CMyQueue::Initialize**呼び出して[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)次のようにキューを作成します。

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

このコード シーケンスは並列で要求をディスパッチする既定のキューになります。 キューは、電源管理の対象、ドライバーが、PPO 場合と、キューが電源管理の対象でない場合は、ドライバーが、PPO でないです。

## <a name="supporting-usb-selective-suspend-in-a-umdf-ppo"></a>UMDF PPO で中断 USB のセレクティブをサポートしています。


選択的なサポートの中断、そのデバイス スタックは、次を実行する必要があります、PPO になっている UMDF USB ドライバー。

1.  通常、デバイス スタックの電源ポリシーの所有権を要求で、 [ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)そのドライバー コールバック オブジェクト、前述のメソッド。
2.  有効にするオプションを選択を呼び出すことによって中断、 [ **IWDFDevice2::AssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556920) framework デバイス オブジェクトのメソッド。

**PPO USB のセレクティブ サスペンドを有効にするには**

-   呼び出す[ **IWDFDevice2::AssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff556920)、通常、 **OnPrepareHardware**デバイス コールバック オブジェクトのメソッド。 パラメーターを AssignS0IdleSettings よう設定します。
    -   *IdleCaps*に**IdleUsbSelectiveSuspend**します。
    -   *DxState*フレームワークがアイドル状態のデバイスを移行するデバイスのスリープ状態にします。 USB のセレクティブ サスペンドは、指定**PowerDeviceMaximum**フレームワークがバス ドライバーが指定されている値を使用することを示します。
    -   *IdleTimeout*をミリ秒数に、framework の前にアイドル状態、デバイスである必要があります遷移に*DxState*します。
    -   *UserControlOfIdleSettings*に**IdleAllowUserControl** 、ドライバーがアイドル状態の設定を管理するユーザーを許可する場合にそれ以外の場合、または**IdleDoNotAllowUserControl**します。
    -   *有効になっている*に**WdfUseDefault**選択的に有効にするユーザーの既定値の設定を許可するが、既定を中断します。

次の例は方法、IdleWake\_PPO ドライバーは、その内部 CMyDevice::SetPowerManagement メソッドでこのメソッドを呼び出します。

```cpp
hr = m_FxDevice->AssignS0IdleSettings( IdleUsbSelectiveSuspend,
                                PowerDeviceMaximum,
                                IDLE_TIMEOUT_IN_MSEC,
                                IdleAllowUserControl,
                                WdfUseDefault);                                                                                                   
```

デバイスのハードウェアでは、ウェイク信号を生成できますが、UMDF ドライバーによりサポート システム S1、S2、S3 からスリープ状態の解除ができます。 詳細については、次を参照してください。 [UMDF ドライバーでは、システムがスリープ解除](#systemwake)します。

## <a name="supporting-usb-selective-suspend-in-a-non-ppo-umdf-driver"></a>USB のセレクティブをサポートしている PPO 以外の UMDF ドライバーで中断


基になる WinUSB.sys ドライバーの機能を使用して、PPO を選択的にサポートできるない UMDF 機能ドライバーを中断します。 UMDF ドライバーは、選択的なデバイスとドライバーのサポートを中断 WinUSB を通知する必要があり、する必要があります有効にする選択的な中断 INF ファイルで、または USB ターゲット デバイス オブジェクトの電源ポリシーを設定します。

UMDF 関数ドライバーにより、選択的な場合は、中断、デバイスがアイドル状態の場合、基になる WinUSB.sys ドライバーを決定します。 WinUSB は保留中の転送がない場合に、または、アイドル タイムアウト カウンターを開始、中断や一括エンドポイント上の転送が保留中の転送のみです。 既定では、アイドル タイムアウトが、5 秒間には、UMDF ドライバーは、この既定を変更できます。

デバイスがアイドル状態であると判断 WinUSB.sys、カーネル モード デバイス スタック、デバイスを中断する要求を送信します。 バス ドライバーでは、適切なハードウェアの状態を変更します。 すべてのデバイスがポートに使用する関数が中断されているポートを入力した場合、USB のセレクティブ サスペンド状態になります。

WinUSB.sys に、I/O 要求は、デバイスが中断されている間に、WinUSB.sys に到着する、要求を処理するデバイスを利用した場合デバイスの操作を再開します。 UMDF ドライバーでは、システムの S0 のままに、デバイスを再開するためのコードは必要ありません。 デバイスのハードウェアでは、ウェイク信号を生成できますが、UMDF ドライバーによりサポート システム S1、S2、S3 からスリープ状態の解除ができます。 詳細については、次を参照してください。 [UMDF ドライバーでは、システムがスリープ解除](#systemwake)します。

UMDF ドライバーが、PPO を選択的にサポートできるは、次の 2 つの手順を実行して中断します。

1.  選択的なデバイスとドライバーのサポートが中断 WinUSB.sys に通知します。
2.  USB のセレクティブの有効化を中断します。

さらに、ドライバーは必要に応じてが可能です。

-   デバイスのタイムアウト値を設定します。
-   有効にするユーザーを許可または無効にする選択的に中断します。

USB のセレクティブを実装する方法の例、PPO ではない UMDF USB 機能ドライバーでの中断を参照してください、Fx2\_ドライバー WDK サンプル。 このサンプルは **%winddk\\BuildNumber\\Src\\Usb\\OsrUsbFx2\\Umdf\\Fx2\_ドライバー\\ IdleWake\_非 PPO**します。

**選択的について WinUSB サスペンドのサポートに通知するには**

通知デバイスが USB を選択的にサポートできることを WinUSB.sys の中断、デバイス INF がデバイスのハードウェア キーへ DeviceIdleEnabled 値を追加し、値を 1 に設定する必要があります。 次の例はどのように、Fx2\_ドライバーのサンプルを追加し、WUDFOsrUsbFx2 にこの値を設定\_IdleWakeNon PPO.Inx ファイル。

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"DeviceIdleEnabled",0x00010001,1
```

**USB のセレクティブがサスペンドを有効にするには**

UMDF USB ドライバーには、USB のセレクティブが有効にすることができますか、実行時に、または、INF でのインストール中に中断します。

-   関数のドライバーの呼び出し時のサポートを有効にする[ **IWDFUsbTargetDevice::SetPowerPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff560385) PolicyType パラメーターを AUTO に設定し、\_中断し、値のパラメーターを TRUE または 1 をします。 次の例はどの、Fx2\_DeviceNonPpo.cpp ファイルでドライバーのサンプルにより選択的なが中断します。
    ```cpp
    BOOL AutoSuspend = TRUE;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( AUTO_SUSPEND,
                                              sizeof(BOOL),
                                             (PVOID) &AutoSuspend );
    ```

-   をインストール中にサポートを有効にする、INF には、デバイスのハードウェア キーに DefaultIdleState 値を追加し、値が 1 に設定する AddReg ディレクティブが含まれています。 以下に例を示します。
    ```cpp
    HKR,,"DefaultIdleState",0x00010001,1
    ```

**アイドル タイムアウト値を設定するには**

既定では、WinUSB 中断デバイス 5 秒後に保留中の転送がない場合、または場合、保留中の転送のみが中断や一括エンドポイントに転送されます。 UMDF ドライバーは、INF でインストールまたは実行時にこのアイドル タイムアウト値を変更できます。

-   インストール時に、アイドル状態のタイムアウトを設定するには、INF とデバイスのハードウェア キー DefaultIdleTimeout 値を加算し、タイムアウト間隔 (ミリ秒単位) を値を設定する AddReg ディレクティブが含まれています。 次の例では、タイムアウトを 7 秒に設定します。
    ```cpp
    HKR,,"DefaultIdleTimeout",0x00010001,7000
    ```

-   ドライバーの呼び出し、実行時にアイドル状態のタイムアウトを設定する**IWDFUsbTargetDevice::SetPowerPolicy** PolicyType 中断に設定と\_遅延と値をミリ秒単位で、アイドル タイムアウト値。 Device.cpp ファイル、Fx2 から次の例では\_ドライバー サンプル タイムアウトを 10 秒に設定します。
    ```cpp
    HRESULT hr;
    ULONG value;
    value = 10 * 1000;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( SUSPEND_DELAY,
                                              sizeof(ULONG),
                                             (PVOID) &value );
    ```

**USB のセレクティブのユーザーによる制御の中断を提供するには**

サスペンドのサポートを使用して選択的 WinUSB UMDF USB ドライバーできます必要に応じてユーザーに許可を有効または無効にする選択的中断します。 これを行うとデバイスのハードウェア キー UserSetDeviceIdleEnabled 値を追加し、値が 1 に設定する INF で、AddReg ディレクティブが含まれます。 AddReg ディレクティブを使用する文字列を次に示します。

```cpp
HKR,,"UserSetDeviceIdleEnabled",0x00010001,1
```

UserSetDeviceIdleEnabled が設定されている場合、デバイスのプロパティ ダイアログ ボックスには、電源管理が有効にまたは USB のセレクティブを無効にするユーザーを許可する タブの中断が含まれています。

## <a name="system-wake-in-a-umdf-driver"></a>UMDF ドライバーでは、システムのスリープ解除


UMDF ドライバーでは、システムのスリープ解除はサポートに依存しないのためのサポート オプションを選択を中断します。 UMDF USB ドライバーが両方のシステムのスリープ解除をサポート オプションを選択し、中断、どちらのシステムのスリープ解除も選択的中断、またはいずれかのシステムのスリープ解除または選択的中断します。 システム スリープ解除をサポートするデバイスは、(S1、S2、または S3) は、スリープ状態からシステムをスリープ解除できます。

USB PPO の UMDF ドライバーでは、フレームワークのドライバー オブジェクトのウェイク アップ情報を提供することによってサポート システムのスリープ解除ができます。 外部イベントには、システムのスリープ解除がトリガーされたときに、フレームワークは稼働状態にデバイスを返します。

USB PPO 以外のドライバーが WinUSB.sys のドライバーを実装するシステムのスリープ解除のサポートを使用できます。

**UMDF USB ドライバーのサポート システムのスリープ解除するには、PPO です。**

呼び出す、 [ **IWDFDevice2::AssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556923)次のパラメーターを framework のデバイス オブジェクトのメソッド。

-   *DxState*するデバイスは遷移ときに電源状態をシステムはウェイク アップ可能 Sx 状態になります。 USB デバイスの場合は、指定**PowerDeviceMaximum**バス ドライバーが指定されている値を使用します。
-   *UserControlOfWakeSettings*に**WakeAllowUserControl**かどうかには、ドライバーが、ウェイク アップの設定を管理するユーザーにそれ以外の場合、または**WakeDoNotAllowUserControl します。**
-   *有効になっている*に**WdfUseDefault**ユーザーの既定値の設定を許可するが、既定では、スリープ解除を有効にします。

次の例はどのように、IdleWake\_PPO ドライバーでは、このメソッドを呼び出してその内部で**CMyDevice::SetPowerManagement**メソッド。

```cpp
hr = m_FxDevice->AssignSxWakeSettings( PowerDeviceMaximum,
                                       WakeAllowUserControl,
                                       WdfUseDefault);
```

**WinUSB を通じてシステム ウェイク PPO 以外のドライバーで有効にするには**

WinUSB を通じてシステム スリープ解除を有効にするのには、ドライバーの INF とデバイスのハードウェア キー SystemWakeEnabled レジストリ値を追加し、1 に設定します。 IdleWake\_非 PPO サンプルにより、次のようにシステムのスリープ解除。

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"SystemWakeEnabled",0x00010001,1
```

この値を設定するには、ドライバーにより、システムのスリープ解除との両方をシステムをスリープ解除するデバイスの機能を制御できます。 デバイス マネージャーで、デバイスの電源管理設定のプロパティ ページには、ユーザーで有効または、システムのスリープ解除を無効にするが、チェック ボックスが含まれています。

## <a name="related-topics"></a>関連トピック
[USB drivers (WDF) でのセレクティブ サスペンドします。](selective-suspend-in-usb-drivers-wdf.md)  



