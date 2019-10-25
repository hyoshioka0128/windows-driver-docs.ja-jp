---
title: NFC CX クイック スタート ガイド
author: EliotSeattle
description: NFC クラス拡張を使用して NFC 機能ドライバーを作成するためのクイックスタートガイドです。
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
- シリーズ
ms.author: eliotgra
ms.date: 12/10/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: low
ms.openlocfilehash: c335cf7386a33fddbe11316b5727938e12065191
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831891"
---
# <a name="nfc-cx-quick-start-guide"></a>NFC CX クイック スタート ガイド

このガイドでは、nfc クラス拡張 (NFC CX) ドライバーを使用して、NFC 機能ドライバーを記述する方法について説明します。

> [!NOTE]
> 実装でクラス拡張ドライバーを使用するドライバーは、"クライアントドライバー" と呼ばれます。 つまり、クラス拡張ドライバーのクライアントであるとします。

## <a name="prerequisites"></a>前提条件

* NFC コントローラーのファームウェアは、NFC フォーラムの[Nfc コントローラーインターフェイス (NCI)](https://nfc-forum.org/our-work/specifications-and-application-documents/specifications/nfc-controller-interface-nci-specification/)プロトコルを実装する必要があります。
* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_content=download+vs2017) (またはそれ以降)。
* [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。
* [Windows 10 Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。

## <a name="client-driver-responsibilities"></a>クライアントドライバーの役割

NFC CX ドライバーは、ドライバーに送信された i/o 要求の処理と、関連する NCI コマンドパケットの作成を担当します。 クライアントドライバーは、これらの NCI パケットを NFC コントローラーに送信し、NCI 応答パケットを NFC CX ドライバーに送り返します。

NCI パケットを NFC コントローラーに送信する方法は、クライアントドライバーによって決定されます。 これは、使用されるハードウェアバスの種類によって異なります。 NFC コントローラーで使用される一般的なバスには、I<sup>2</sup>C、SPI、USB があります。

## <a name="complete-project-code"></a>完成したプロジェクトコード

このサンプルコードの完全なバージョンについては、GitHub: [NFC CX クライアントドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/nfc/NfcCxSample)を参照してください。

## <a name="project-setup"></a>プロジェクトのセットアップ

1. Visual Studio で、新しい "User Mode Driver, Empty (UMDF V2)" プロジェクトを作成します。

    **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 **ビジュアルC++** ノードの **[Windows ドライバー]** で、 **[WDF]** をクリックし、[**ユーザーモードドライバー]、[空 (UMDF V2)** ] の順にクリックします。

    ![image](images/quick-start-new-project.png)

2. INF ファイルを開きます。

   **ソリューションエクスプローラー**で、[ **\<プロジェクト名 >** ] ノードの下の **[ドライバーファイル]** フォルダーで、[ **\<プロジェクト名 > .inf**] をダブルクリックします。

3. INF ファイルで、次の手順に従ってカスタムデバイスクラスを削除します。

    1. 次の2つのセクションを削除します。

        ```inf
        [ClassInstall32]
        AddReg=SampleClass_RegistryAdd

        [SampleClass_RegistryAdd]
        HKR,,,,%ClassName%
        HKR,,Icon,,"-10"
        ```

    2. [`[Strings]`] セクションで、次の行を削除します。 

        ```inf
        ClassName="Samples" ; TODO: edit ClassName
        ```

4. INF ファイルで、ドライバーの device クラスを**近接**に設定します。

    1. `Class` の値をに変更し `Proximity`
    2. `ClassGuid` の値をに変更し `{5630831C-06C9-4856-B327-F5D32586E060}`
        - これは近接デバイスクラスの GUID です。

    ```ini
    [Version]
    ...
    Class=Proximity
    ClassGuid={5630831C-06C9-4856-B327-F5D32586E060} ; Proximity class GUID
    ...
    ```

5. INF ファイルで、NFC クラス拡張への参照を追加します。 これにより、クライアントドライバーの読み込み時に Windows Driver Framework (WDF) が NFC CX ドライバーを読み込むようになります。
  
    1. `<project-name>_Install` セクションを見つけます。
    2. `UmdfExtensions=NfcCx0102`を追加します。

    ```ini
    [<project-name>_Install]
    ...
    UmdfExtensions=NfcCx0102
    ```

6. ドライバーのビルド設定で、NFC クラス拡張にリンクします。 これにより、コードのコンパイル中に NFC CX API を使用できるようになります。

    1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[プロパティ]** をクリックします。 **[構成プロパティ]** の **[ドライバーの設定]** で、 **[NFC]** をクリックします。
    2. **構成**が `All Configurations`に設定されていることを確認します。
    3. **プラットフォーム**が `All Platforms`に設定されていることを確認します。
    4. **NFC クラス拡張へのリンク**を `Yes`に設定します。

    ![image](images/quick-start-link-to-nfc-cx.png)

7. `Driver.cpp` という名前のファイルをプロジェクトに追加します。

8. `Driver.cpp`に `DriverEntry` ルーチンを作成します。 これは、ドライバーのエントリポイントです。 主な目的は、WDF を初期化し、 [`EvtDriverDeviceAdd`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を登録することです。

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

9. `Device.cpp` と `Device.h` という名前の2つのファイルをプロジェクトに追加します。

10. `Device.h`で、`DeviceContext` クラスを定義します。

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

11. `Device.cpp`で、`DeviceContext::AddDevice` 関数の定義を開始します。

    ```cpp
    #include "Device.h"

    NTSTATUS DeviceContext::AddDevice(
        _In_ WDFDRIVER Driver,
        _Inout_ PWDFDEVICE_INIT DeviceInit)
    {
        NTSTATUS status;

    ```

12. NFC CX デバイス構成を設定します。 デバイス構成には、 [`EvtNfcCxWriteNciPacket`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nc-nfccx-evt_nfc_cx_write_nci_packet)コールバック関数の提供が含まれます。 このコールバックは、クライアントドライバーが NFC コントローラーに転送する必要がある、NFC CX ドライバーからの NCI パケットを受信します。

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

13. クライアントドライバーに必要な[PnP 電源コールバック](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-pnp-and-power-management-in-function-drivers)を登録します。

    一般的なクライアントドライバーでは、 [`EvtDevicePrepareHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)、 [`EvtDeviceReleaseHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)、 [`EvtDeviceD0Entry`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 、および[`EvtDeviceD0Exit`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)の機能が必要になる可能性があります。 要件は、クライアントドライバーが電源管理を処理する方法によって異なります。

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

14. [`WdfDeviceCreate`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)関数を呼び出して、 [`WDFDEVICE`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/)オブジェクトを作成します。

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

15. [`NfcCxDeviceInitialize`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)関数を呼び出します。

    この関数は、 [`WDFDEVICE`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/)オブジェクトが作成された後に呼び出され、NFC CX ドライバーがデバイスインスタンスの初期化を完了できるようにします。

    ```cpp
        // Let NFC CX finish initializing the device instance.
        status = NfcCxDeviceInitialize(device);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

16. [`NfcCxSetRfDiscoveryConfig`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)を呼び出して、nfc コントローラーでサポートされている nfc テクノロジとプロトコルを指定します。

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

17. `DeviceContext::AddDevice` 関数を終了します。

    ```cpp
        return STATUS_SUCCESS;
    }
    ```

18. [`PrepareHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)および[`ReleaseHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を実装します。

    この2つの関数は、NFC コントローラーのデバイスインスタンスに割り当てられたハードウェアリソースの初期化と初期化解除に使用されます。 これらの実装は、デバイスが接続されているバスの種類 (例: I<sup>2</sup>C、SPI、USB) によって異なります。

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

19. NCI ステートマシンを適切なタイミングで開始および停止するには、 [`HostActionStart`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ne-nfccx-_nfc_cx_host_action)と[`HostActionStop`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ne-nfccx-_nfc_cx_host_action)を使用して[`NfcCxHardwareEvent`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxhardwareevent)関数を呼び出します。

    一部のドライバーは、 [`D0Entry`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)中にこの処理を行い、PnP 電源コールバックを[`D0Exit`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)します。 ただし、クライアントドライバーが電源管理を処理する方法によって異なります。

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

20. [`WriteNciPacket`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nc-nfccx-evt_nfc_cx_write_nci_packet)関数を実装します。

    このコールバックは、nfc コントローラーに送信する NCI パケットがある場合に、NFC CX によって呼び出されます。

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

21. Nfc コントローラーの NCI パケットが NFC CX に送信される必要がある場合は、 [`NfcCxNciReadNotification`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)関数を呼び出します。 これは通常、ハードウェアイベントコールバックで行われます。

    次に、例を示します。
    - [GPIO interrupt](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)イベントのコールバック。 (I<sup>2</sup>C と SPI)
    - [USB 連続リーダー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-)コールバック。

## <a name="logging"></a>ログ

デバッグを容易にするために、クライアントドライバーにログ記録を追加することを検討してください。 [ETW トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)と[WPP トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)はどちらも適切なオプションです。
