---
title: NFC CX のクイック スタート ガイド
author: EliotSeattle
description: NFC クラスの拡張機能を使用して、NFC 機能ドライバーを記述するためのクイック スタート ガイドです。
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
- CX
ms.author: eliotgra
ms.date: 12/10/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: low
ms.openlocfilehash: 7fab3eb7b3e5d420717f88a7deab73b9687bdc9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552437"
---
# <a name="nfc-cx-quick-start-guide"></a>NFC CX のクイック スタート ガイド

このガイドでは、NFC クラスの拡張機能 (NFC CX) ドライバーを使用して、NFC 機能ドライバーを作成する方法を示します。

> [!NOTE]
> 実装クラスの拡張機能ドライバーを使用するドライバーは、クライアント ドライバーと呼ばれます。 つまり、クライアント クラスの拡張機能ドライバー。

## <a name="prerequisites"></a>前提条件

* NFC コント ローラーのファームウェアが NFC フォーラムを実装する必要があります[NFC コント ローラー インターフェイス (NCI)](https://nfc-forum.org/our-work/specifications-and-application-documents/specifications/nfc-controller-interface-nci-specification/)プロトコル。
* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_content=download+vs2017) (またはそれ以降)。
* [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)します。
* [10 Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)します。

## <a name="client-driver-responsibilities"></a>クライアント ドライバーの責任

NFC CX ドライバーは I/O に要求を処理、ドライバーに送信され、関連する NCI コマンド パケットを作成します。 クライアント ドライバーは、NFC コント ローラーに、NCI パケットを送信し、NFC CX ドライバーに戻る NCI 応答パケットを送信します。

NFC コント ローラーに NCI パケットを送信する方法を決定するクライアント ドライバーの責任です。 これについては、使用、ハードウェア バスの種類によって異なります。 NFC のコント ローラーで使用される共通のバスを含めるは<sup>2</sup>C、SPI および USB です。

## <a name="complete-project-code"></a>完全なプロジェクト コード

このサンプル コードの完全なバージョンは、GitHub で入手できます。[クライアント ドライバーのサンプルの NFC CX](https://github.com/Microsoft/Windows-driver-samples/tree/master/nfc/NfcCxSample)します。

## <a name="project-setup"></a>プロジェクトのセットアップ

1. Visual Studio で、作成、新しい「ユーザー モード ドライバー、空 (UMDF V2)」プロジェクト。

    **ファイル**メニューで、**新規**、 をクリックし、**プロジェクト**します。 **Visual C**ノード [ **Windows ドライバー**、] をクリックして**WDF**、順にクリックします**ユーザー モード ドライバー、空 (UMDF V2)**

    ![image](images/quick-start-new-project.png)

2. INF ファイルを開きます。

   **ソリューション エクスプ ローラー**下で、 **\<プロジェクト名 >** ノードで、**ドライバー ファイル**フォルダーをダブルクリック **\<プロジェクト名 > .inf**します。

3. INF ファイルでは、次の手順を使用して、カスタムのデバイス クラスを削除します。

    1. 次の 2 つのセクションを削除します。

        ```inf
        [ClassInstall32]
        AddReg=SampleClass_RegistryAdd

        [SampleClass_RegistryAdd]
        HKR,,,,%ClassName%
        HKR,,Icon,,"-10"
        ```

    2. で、`[Strings]`セクションで、次の行を削除します。 

        ```inf
        ClassName="Samples" ; TODO: edit ClassName
        ```

4. INF ファイルでドライバーのデバイス クラスを設定**近接**:

    1. 値を変更`Class`に `Proximity`
    2. 値を変更`ClassGuid`に `{5630831C-06C9-4856-B327-F5D32586E060}`
        - これは、近接デバイス クラスの GUID です。

    ```ini
    [Version]
    ...
    Class=Proximity
    ClassGuid={5630831C-06C9-4856-B327-F5D32586E060} ; Proximity class GUID
    ...
    ```

5. INF ファイルでは、NFC クラスの拡張機能への参照を追加します。 これには、クライアント ドライバーの読み込み時に、Windows Driver Framework (WDF) が、NFC CX ドライバーを読み込むことにより保証されます。
  
    1. 検索、`<project-name>_Install`セクション。
    2. 追加`UmdfExtensions=NfcCx0102`します。

    ```ini
    [<project-name>_Install]
    ...
    UmdfExtensions=NfcCx0102
    ```

6. ドライバーのビルド設定、NFC クラスの拡張機能にリンクします。 これには、コードのコンパイル時に、NFC CX API があるにより保証されます。

    1. **ソリューション エクスプ ローラー**、プロジェクトを右クリックし、クリックして、**プロパティ**します。 **構成プロパティ**[**ドライバー設定**、] をクリックして**NFC**します。
    2. いることを確認**構成**に設定されている`All Configurations`します。
    3. いることを確認**プラットフォーム**に設定する`All Platforms`します。
    4. 設定**NFC クラスの拡張機能へのリンク**に`Yes`します。

    ![image](images/quick-start-link-to-nfc-cx.png)

7. という名前のファイルを追加`Driver.cpp`をプロジェクトにします。

8. 作成、`DriverEntry`で日常的な`Driver.cpp`します。 これは、ドライバーのエントリ ポイントです。 主な目的は WDF を初期化するために登録して、 [ `EvtDriverDeviceAdd` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

    ```cpp
    #include <windows.h>
    #include <wdf.h>

    #include "Device.h" // created in Step 9

    // The entry point for the driver.
    extern "C" NTSTATUS DriverEntry(
        _In_ PDRIVER_OBJECT DriverObject,
        _In_ PUNICODE_STRING RegistryPath
        )
    {
        NTSTATUS status = STATUS_SUCCESS;

        // Specify `DeviceContext::AddDevice` as the 
        // `EvtDriverDeviceAdd` function for the driver.
        WDF_DRIVER_CONFIG driverConfig;
        WDF_DRIVER_CONFIG_INIT(&driverConfig, DeviceContext::AddDevice);

        // Initialize WDF.
        status = WdfDriverCreate(
            DriverObject,
            RegistryPath,
            WDF_NO_OBJECT_ATTRIBUTES,
            &driverConfig,
            WDF_NO_HANDLE);
        if (!NT_SUCCESS(status))
        {
            return status;
        }

        return STATUS_SUCCESS;
    }
    ```

9. という名前の 2 つのファイルを追加`Device.cpp`と`Device.h`をプロジェクトにします。

10. `Device.h`、定義、`DeviceContext`クラス。

    ```cpp
    #pragma once

    #include <windows.h>
    #include <wdf.h>
    #include <NfcCx.h>

    // The class that will store the driver's custom state for
    // a device instance.
    class DeviceContext
    {
    public:
        // Implementation of `EvtDriverDeviceAdd`.
        static NTSTATUS AddDevice(
            _In_ WDFDRIVER Driver,
            _Inout_ PWDFDEVICE_INIT DeviceInit);

    private:
        // Implementation of `EvtDevicePrepareHardware`.
        static NTSTATUS PrepareHardware(
            _In_ WDFDEVICE Device,
            _In_ WDFCMRESLIST ResourcesRaw,
            _In_ WDFCMRESLIST ResourcesTranslated);

        // Implementation of `EvtDeviceReleaseHardware`.
        static NTSTATUS ReleaseHardware(
            _In_ WDFDEVICE Device,
            _In_ WDFCMRESLIST ResourcesTranslated);

        // Implementation of `EvtDeviceD0Entry`.
        static NTSTATUS D0Entry(
            _In_ WDFDEVICE Device,
            _In_ WDF_POWER_DEVICE_STATE PreviousState);

        // Implementation of `EvtDeviceD0Exit`.
        static NTSTATUS D0Exit(
            _In_ WDFDEVICE Device,
            _In_ WDF_POWER_DEVICE_STATE TargetState);

        // Implementation of `EvtNfcCxWriteNciPacket`.
        static void WriteNciPacket(
            _In_ WDFDEVICE Device,
            _In_ WDFREQUEST Request);
    };

    // Define the `DeviceGetContext` function.
    WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(DeviceContext, DeviceGetContext);
    ```

11. `Device.cpp`、開始、`DeviceContext::AddDevice`関数の定義。

    ```cpp
    #include "Device.h"

    NTSTATUS DeviceContext::AddDevice(
        _In_ WDFDRIVER Driver,
        _Inout_ PWDFDEVICE_INIT DeviceInit)
    {
        NTSTATUS status;

    ```

12. NFC CX のデバイスの構成を設定します。 デバイスの構成には、提供することが含まれています、 [ `EvtNfcCxWriteNciPacket` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nc-nfccx-evt_nfc_cx_write_nci_packet)コールバック関数。 このコールバックは、クライアント ドライバーは、NFC コント ローラーに転送する必要があります、NFC CX ドライバーから NCI パケットを受信します。

    ```cpp
        // Create the NfcCx config.
        NFC_CX_CLIENT_CONFIG nfcCxConfig;
        NFC_CX_CLIENT_CONFIG_INIT(&nfcCxConfig, NFC_CX_TRANSPORT_CUSTOM);
        nfcCxConfig.EvtNfcCxWriteNciPacket = WriteNciPacket;
        nfcCxConfig.DriverFlags = NFC_CX_DRIVER_ENABLE_EEPROM_WRITE_PROTECTION;

        // Set the NfcCx config.
        status = NfcCxDeviceInitConfig(DeviceInit, &nfcCxConfig);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

13. 登録、 [power コールバックの PnP](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-pnp-and-power-management-in-function-drivers)クライアント ドライバーで必要です。

    一般的なクライアント ドライバーの方が、 [ `EvtDevicePrepareHardware` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)、 [ `EvtDeviceReleaseHardware` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)、 [ `EvtDeviceD0Entry` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)と[ `EvtDeviceD0Exit`](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)関数。 要件は、クライアント ドライバーによる電源管理の処理方法によって異なります。

    ```cpp
        // Create the PnP power callbacks configuration.
        WDF_PNPPOWER_EVENT_CALLBACKS pnpCallbacks;
        WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&pnpCallbacks);
        pnpCallbacks.EvtDevicePrepareHardware = PrepareHardware;
        pnpCallbacks.EvtDeviceReleaseHardware = ReleaseHardware;
        pnpCallbacks.EvtDeviceD0Entry = D0Entry;
        pnpCallbacks.EvtDeviceD0Exit = D0Exit;

        // Set the PnP power callbacks.
        WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, &pnpCallbacks);
    ```

14. 呼び出す、 [ `WdfDeviceCreate` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)関数を作成する、 [ `WDFDEVICE` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/)オブジェクト。

    ```cpp
        // Create WDF object attributes for the WDFDEVICE object.
        WDF_OBJECT_ATTRIBUTES deviceAttributes;
        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DeviceContext);

        // Create the device.
        WDFDEVICE device;
        status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

15. 呼び出す、 [ `NfcCxDeviceInitialize` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdeviceinitialize)関数。

    後に、この関数を呼び出す必要があります、 [ `WDFDEVICE` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/) NFC CX ドライバーがデバイスのインスタンスの初期化を完了するを許可するオブジェクトが作成されています。

    ```cpp
        // Let NFC CX finish initializing the device instance.
        status = NfcCxDeviceInitialize(device);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

16. 呼び出す[ `NfcCxSetRfDiscoveryConfig` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig) NFC テクノロジと NFC コント ローラーでサポートされるプロトコルを指定します。

    ```cpp
        // Create the RF config. (Enable everything.)
        NFC_CX_RF_DISCOVERY_CONFIG discoveryConfig;
        NFC_CX_RF_DISCOVERY_CONFIG_INIT(&discoveryConfig);
        discoveryConfig.PollConfig =
            NFC_CX_POLL_NFC_A | NFC_CX_POLL_NFC_B |
            NFC_CX_POLL_NFC_F_212 | NFC_CX_POLL_NFC_F_424 |
            NFC_CX_POLL_NFC_15693 | NFC_CX_POLL_NFC_ACTIVE |
            NFC_CX_POLL_NFC_A_KOVIO;
        discoveryConfig.NfcIPMode =
            NFC_CX_NFCIP_NFC_A | NFC_CX_NFCIP_NFC_F_212 |
            NFC_CX_NFCIP_NFC_F_424 | NFC_CX_NFCIP_NFC_ACTIVE |
            NFC_CX_NFCIP_NFC_ACTIVE_A | NFC_CX_NFCIP_NFC_ACTIVE_F_212 |
            NFC_CX_NFCIP_NFC_ACTIVE_F_424;
        discoveryConfig.NfcIPTgtMode =
            NFC_CX_NFCIP_TGT_NFC_A | NFC_CX_NFCIP_TGT_NFC_F |
            NFC_CX_NFCIP_TGT_NFC_ACTIVE_A | NFC_CX_NFCIP_TGT_NFC_ACTIVE_F;
        discoveryConfig.NfcCEMode =
            NFC_CX_CE_NFC_A | NFC_CX_CE_NFC_B |
            NFC_CX_CE_NFC_F;

        // Set the RF config.
        status = NfcCxSetRfDiscoveryConfig(device, &discoveryConfig);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

17. 終了、`DeviceContext::AddDevice`関数。

    ```cpp
        return STATUS_SUCCESS;
    }
    ```

18. 実装、 [ `PrepareHardware` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)と[ `ReleaseHardware` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数。

    これら 2 つの関数は、デバイスの NFC コント ローラーのインスタンスに割り当てられたハードウェア リソースを初期化してに使用されます。 その実装に、デバイスが接続されているバスの種類によって異なります (例: は<sup>2</sup>C、SPI および USB)。

    ```cpp
    NTSTATUS DeviceContext::PrepareHardware(
        _In_ WDFDEVICE Device,
        _In_ WDFCMRESLIST ResourcesRaw,
        _In_ WDFCMRESLIST ResourcesTranslated)
    {
        // FIX ME: Initialize hardware resources.
        return STATUS_SUCCESS;
    }

    NTSTATUS DeviceContext::ReleaseHardware(
        _In_ WDFDEVICE Device,
        _In_ WDFCMRESLIST ResourcesTranslated)
    {
        // FIX ME: Uninitialize hardware resources.
        return STATUS_SUCCESS;
    }
    ```

19. 呼び出す、 [ `NfcCxHardwareEvent` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxhardwareevent)関数と[ `HostActionStart` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/ne-nfccx-_nfc_cx_host_action)と[ `HostActionStop` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/ne-nfccx-_nfc_cx_host_action)を起動し、適切なタイミングで NCI のステート マシンを停止します。

    一部のドライバーはこの中に、 [ `D0Entry` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)と[ `D0Exit` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) PnP power コールバック。 これには、クライアント ドライバーがただし、電源管理を処理によって異なります。

    ```cpp
    // Device exiting low power state (or is booting up).
    NTSTATUS DeviceContext::D0Entry(
        _In_ WDFDEVICE Device,
        _In_ WDF_POWER_DEVICE_STATE PreviousState)
    {
        (void)PreviousState;

        NTSTATUS status;

        // Invoke the HostActionStart event, so that the NFC CX initializes
        // the NFC Controller.
        NFC_CX_HARDWARE_EVENT eventArgs = {};
        eventArgs.HostAction = HostActionStart;

        status = NfcCxHardwareEvent(Device, &eventArgs);
        if (!NT_SUCCESS(status))
        {
            return status;
        }

        return STATUS_SUCCESS;
    }

    // Device entering low power state.
    NTSTATUS DeviceContext::D0Exit(
        _In_ WDFDEVICE Device,
        _In_ WDF_POWER_DEVICE_STATE TargetState)
    {
        (void)TargetState;

        NTSTATUS status;

        // Trigger the HostActionStop event, so that the NFC CX
        // uninitializes the NFC Controller.
        NFC_CX_HARDWARE_EVENT eventArgs = {};
        eventArgs.HostAction = HostActionStop;

        status = NfcCxHardwareEvent(Device, &eventArgs);
        if (!NT_SUCCESS(status))
        {
            return status;
        }

        return STATUS_SUCCESS;
    }
    ```

20. 実装、 [ `WriteNciPacket` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nc-nfccx-evt_nfc_cx_write_nci_packet)関数。

    このコールバックは、NFC コント ローラーに送信する、NCI パケットがある場合に、NFC CX によって呼び出されます。

    ```cpp
    void DeviceContext::WriteNciPacket(
        _In_ WDFDEVICE Device,
        _In_ WDFREQUEST Request)
    {
        NTSTATUS status;

        // Get the NCI packet as a raw byte buffer.
        void* nciPacket;
        size_t nciPacketLength;
        status = WdfRequestRetrieveInputBuffer(Request, 0, &nciPacket, &nciPacketLength);
        if (!NT_SUCCESS(status))
        {
            WdfRequestComplete(Request, status);
            return;
        }

        // FIX ME: Use the NCI packet in some way.

        // FIX ME: Call `WdfRequestComplete` on `Request` with failure 
        // or success `NTSTATUS` code.
    };
    ```

21. 呼び出す、 [ `NfcCxNciReadNotification` ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxncireadnotification)関数の NFC コント ローラーが、NCI パケット NFC CX に送信する必要があります。 これは通常、ハードウェア イベントのコールバックで行われます。

    次に、例を示します。
    - A [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)イベント コールバック。 (は<sup>2</sup>C および SPI)
    - A [USB の継続的なリーダー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-)コールバック。

## <a name="logging"></a>ログ記録

デバッグを容易にできるように、クライアント ドライバーへのログ記録の追加を検討してください。 両方[ETW トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)と[WPP トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)優れたオプションです。
