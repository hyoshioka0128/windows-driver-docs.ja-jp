---
title: フレーム サーバーのカスタム メディア ソース
description: フレームサーバーアーキテクチャ内でのカスタムメディアソースの実装について説明します。
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ca5c0beab801285b6bde63672f0d2e8faddc5ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842594"
---
# <a name="frame-server-custom-media-source"></a>フレーム サーバーのカスタム メディア ソース 

このトピックでは、フレームサーバーアーキテクチャ内でのカスタムメディアソースの実装について説明します。 

## <a name="av-stream-and-custom-media-source-options"></a>AV ストリームおよびカスタムメディアソースオプション

フレームサーバーアーキテクチャでビデオキャプチャストリームのサポートを提供する方法を決定する際には、主に AV ストリームとカスタムメディアソースという2つのオプションがあります。

AV Stream モデルは、AV ストリームミニポートドライバー (カーネルモードドライバー) を使用する標準のカメラドライバーモデルです。 通常、AV ストリームドライバーは、MIPI ベースのドライバーと USB ビデオクラスドライバーの2つの主なカテゴリに分類されます。

[カスタムメディアソース] オプションでは、ドライバーモデルが完全にカスタム (専用) である場合もあれば、従来のカメラソース (ファイル、ネットワークソースなど) に基づいている場合もあります。

### <a name="av-stream-driver"></a>AV ストリームドライバー

AV Stream ドライバーのアプローチの主な利点は、PnP と電源管理/デバイス管理が既に AV ストリームフレームワークによって処理されていることです。

ただし、基になるソースが、ハードウェアとのインターフェイスを持つカーネルモードドライバーを持つ物理デバイスであることも意味します。 UVC デバイスの場合、デバイスがファームウェアを実装するだけで済むように、Windows UVC 1.5 クラスドライバーが受信トレイに提供されます。

MIPI ベースのデバイスの場合、ベンダーは独自の AV ストリームミニポートドライバーを実装する必要があります。

### <a name="custom-media-source"></a>カスタムメディアソース

デバイスドライバーが既に利用可能で (AV ストリームミニポートドライバーではない)、または従来のカメラキャプチャを使用するソースの場合、AV ストリームドライバーは実行できない可能性があります。 たとえば、ネットワーク経由で接続されている IP カメラは、AV ストリームドライバーモデルには適合しません。

このような場合は、フレームサーバーモデルを使用したカスタムメディアソースが代わりに使用されます。

| 機能 | カスタムメディアソース | AV ストリームドライバー |
|---|---|---|
| PnP と電源管理 | ソースまたはスタブドライバーによって実装されている必要があります。 | AV Stream フレームワークによって提供されます。 |
| ユーザーモードプラグイン       | 使用できません。 カスタムメディアソースには、OEM/IHV 固有のユーザーモードロジックが組み込まれています。 | 従来の実装のための DMFT、Platform DMFT、MFT0 |
| センサーグループ | サポート対象 | サポート対象 |
| カメラプロファイル V2 | サポート対象 | サポート対象 |
| カメラプロファイル V1 | サポートされない | サポート対象 |

## <a name="custom-media-source-requirements"></a>カスタムメディアソースの要件

Windows Camera Frame Server (Frame Server) サービスの導入により、これはカスタムメディアソースを通じて実現できます。 これには、次の2つの主要なコンポーネントが必要です。

-   カメラデバイスインターフェイスを登録または有効にするように設計されたスタブドライバーを含むドライバーパッケージ。

-   カスタムメディアソースをホストする COM DLL。

最初の要件は、次の2つの目的で必要です。

-   カスタムメディアソースが信頼されたプロセスによってインストールされるようにする審査プロセス (ドライバーパッケージには WHQL 認定が必要です)。

-   "カメラ" の標準の PnP 列挙と検出のサポート。

### <a name="security"></a>セキュリティ

フレームサーバーのカスタムメディアソースは、次の方法で、セキュリティの観点から汎用カスタムメディアソースと異なります。

-   フレームサーバーカスタムメディアソースはローカルサービスとして実行されます (ローカルシステムと混同しないでください)。ローカルサービスは、Windows マシン上で非常に低い特権を持つアカウントです。

-   フレームサーバーのカスタムメディアソースは、セッション 0 (システムサービスセッション) で実行され、ユーザーのデスクトップと対話することはできません。

これらの制約により、フレームサーバーのカスタムメディアソースは、ファイルシステムまたはレジストリの保護された部分にアクセスしないようにする必要があります。 一般に、読み取りアクセスは許可されますが、書き込みアクセスは許可されません。

### <a name="performance"></a>パフォーマンス

フレームサーバーモデルの一部として、次の2つのケースでは、フレームサーバーによってカスタムメディアソースがインスタンス化されます。

-   センサーグループの生成/発行中。

-   "カメラ" のアクティブ化中

センサーグループの生成は、通常、デバイスのインストールや電源サイクル中に行われます。 このため、カスタムメディアソースでは、作成時の重要な処理を避け、 [Imfmediasource:: Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)関数にそのようなアクティビティを遅延させることを強くお勧めします。 センサーグループの生成では、カスタムメディアソースを開始しようとしません。使用可能なさまざまなストリーム/メディアの種類とソース/ストリーム属性の情報をクエリするだけです。

## <a name="stub-driver"></a>スタブドライバー

ドライバーパッケージとスタブドライバーには、次の2つの最小要件があります。

スタブドライバーは、WDF (UMDF または KMDF) または WDM ドライバーモデルを使用して書き込むことができます。

ドライバーの要件は次のとおりです。

-   [ [KSCATEGORY_VIDEO_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video-camera) ] カテゴリの下に "カメラ" (カスタムメディアソース) デバイスインターフェイスを登録して、列挙できるようにします。

> [!NOTE]
> レガシ DirectShow アプリケーションで列挙できるようにするには、ドライバーも[KSCATEGORY_VIDEO](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video)と[KSCATEGORY_CAPTURE](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-capture)に登録する必要があります。

-   [デバイスインターフェイス] ノードの下にレジストリエントリを追加します ( **AddReg**ディレクティブを使用してください)。これは、カスタムメディアソース COM オブジェクトの CoCreate が可能な CLSID を宣言します **。** これは、次のレジストリ値の名前を使用して追加する必要があります: **CustomCaptureSourceClsid**。

これにより、アプリケーションで "カメラ" ソースを検出し、アクティブにすると、アクティブ化呼び出しをインターセプトして、CoCreated カスタムメディアソースに再ルーティングするようにフレームサーバーサービスに通知します。

### <a name="sample-inf"></a>サンプル INF

次のサンプルは、カスタムメディアソーススタブドライバーの一般的な INF を示しています。

```INF
;/*++
;
;Module Name:
; SimpleMediaSourceDriver.INF
;
;Abstract:
; INF file for installing the Usermode SimpleMediaSourceDriver Driver
;
;Installation Notes:
; Using Devcon: Type "devcon install SimpleMediaSourceDriver.inf root\SimpleMediaSource" to install
;
;--*/

[Version]
Signature="$WINDOWS NT$"
Class=Sample
ClassGuid={5EF7C2A5-FF8F-4C1F-81A7-43D3CBADDC98}
Provider=%ProviderString%
DriverVer=01/28/2016,0.10.1234
CatalogFile=SimpleMediaSourceDriver.cat

[DestinationDirs]
DefaultDestDir = 12

; ================= Class section =====================

[ClassInstall32]
Addreg=SimpleMediaSourceClassReg

[SimpleMediaSourceClassReg]

HKR,,,0,%ClassName%
HKR,,Icon,,-24

[SourceDisksNames]
1 = %DiskId1%,,,""

[SourceDisksFiles]
SimpleMediaSourceDriver.dll = 1,,
SimpleMediaSource.dll = 1,,

;*****************************************
; SimpleMFSource Install Section
;*****************************************

[Manufacturer]
%StdMfg%=Standard,NT$ARCH$

[Standard.NT$ARCH$]
%SimpleMediaSource.DeviceDesc%=SimpleMediaSource, root\SimpleMediaSource

;---------------- copy files

[SimpleMediaSource.NT]
CopyFiles=UMDriverCopy, CustomCaptureSourceCopy
AddReg = CustomCaptureSource.ComRegistration

[SimpleMediaSource.NT.Interfaces]
AddInterface = %KSCATEGORY_VIDEO_CAMERA%, %CustomCaptureSource.ReferenceString%, CustomCaptureSourceInterface
AddInterface = %KSCATEGORY_VIDEO%, %CustomCaptureSource.ReferenceString%, CustomCaptureSourceInterface
AddInterface = %KSCATEGORY_CAPTURE%, %CustomCaptureSource.ReferenceString%, CustomCaptureSourceInterface

[CustomCaptureSourceInterface]
AddReg = CustomCaptureSourceInterface.AddReg, CustomCaptureSource.ComRegistration

[CustomCaptureSourceInterface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,CustomCaptureSourceClsid,,%CustomCaptureSource.CLSID%
HKR,,FriendlyName,,%CustomCaptureSource.Desc%

[CustomCaptureSource.ComRegistration]
HKCR,CLSID\%CustomCaptureSource.CLSID%,,,%CustomCaptureSource.Desc%
HKCR,CLSID\%CustomCaptureSource.CLSID%\InprocServer32,,%REG_EXPAND_SZ%,%CustomCaptureSource.Location%
HKCR,CLSID\%CustomCaptureSource.CLSID%\InprocServer32,ThreadingModel,,Both

[UMDriverCopy]
SimpleMediaSourceDriver.dll,,,0x00004000 ; COPYFLG_IN_USE_RENAME

[CustomCaptureSourceCopy]
SimpleMediaSource.dll,,,0x00004000 ; COPYFLG_IN_USE_RENAME

[DestinationDirs]
UMDriverCopy=12,UMDF ; copy to driversMdf
CustomCaptureSourceCopy=11

;-------------- Service installation
[SimpleMediaSource.NT.Services]
AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall

[WUDFRD_ServiceInstall]
DisplayName = %WudfRdDisplayName%
ServiceType = 1
StartType = 3
ErrorControl = 1
ServiceBinary = %12%\WUDFRd.sys

;-------------- WDF specific section -------------
[SimpleMediaSource.NT.Wdf]
UmdfService=SimpleMediaSource, SimpleMediaSource_Install
UmdfServiceOrder=SimpleMediaSource

[SimpleMediaSource_Install]
UmdfLibraryVersion=$UMDFVERSION$
ServiceBinary=%12%\UMDF\SimpleMediaSourceDriver.dll

[Strings]
ProviderString = "Microsoft Corporation"
StdMfg = "(Standard system devices)"
DiskId1 = "SimpleMediaSource Disk \#1"
SimpleMediaSource.DeviceDesc = "SimpleMediaSource Capture Source" ; what you will see under SimpleMediaSource dummy devices
ClassName = "SimpleMediaSource dummy devices" ; device type this driver will install as in device manager
WudfRdDisplayName="Windows Driver Foundation - User-mode Driver Framework Reflector"
KSCATEGORY_VIDEO_CAMERA = "{E5323777-F976-4f5b-9B55-B94699C46E44}"
KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_VIDEO="{6994AD05-93EF-11D0-A3CC-00A0C9223196}"
ProxyVCap.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
CustomCaptureSource.Desc = "SimpleMediaSource Source"
CustomCaptureSource.ReferenceString = "CustomCameraSource"
CustomCaptureSource.CLSID = "{9812588D-5CE9-4E4C-ABC1-049138D10DCE}"
CustomCaptureSource.Location = "%SystemRoot%\System32\SimpleMediaSource.dll"
CustomCaptureSource.Binary = "SimpleMediaSource.dll"
REG_EXPAND_SZ = 0x00020000
```

上記のカスタムメディアソースは、UWP と UWP 以外のアプリの検索によって "カメラ" が検出可能であることを確認するために、 **KSCATEGORY\_video**、 **KSCATEGORY\_CAPTURE**、 **KSCATEGORY\_video\_カメラ**の下に登録されています。標準の RGB カメラの場合。

カスタムメディアソースでも RGB 以外のストリーム (IR、深度など) が公開される場合は、必要に応じて[KSCATEGORY_SENSOR_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-sensor-camera)で登録することもできます。

> [!NOTE]
> ほとんどの USB ベースの web カメラでは、YUY2 形式と MJPG 形式が公開されます。 この動作のため、多くの従来の DirectShow アプリケーションは、YUY2/MJPG が使用可能であるという前提で記述されています。 このようなアプリケーションとの互換性を確保するために、レガシアプリの互換性が必要な場合は、カスタムメディアソースから YUY2 メディアの種類を使用できるようにすることをお勧めします。

### <a name="stub-driver-implementation"></a>スタブドライバーの実装

INF に加えて、ドライバースタブもカメラデバイスインターフェイスを登録して有効にする必要があります。 これは通常、**ドライバー\_\_デバイス**操作の追加によって行われます。

「WDM ベースのドライバー用の[DRIVER_ADD_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)コールバック関数」および「UMDF/kmdf ドライバー用の[Wdfdrivercreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)関数」を参照してください。

次に、この操作を処理する UMDF ドライバースタブのコード切り取りを示します。

```cpp
NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
/*++

Routine Description:

    DriverEntry initializes the driver and is the first routine called by the
    system after the driver is loaded. DriverEntry specifies the other entry
    points in the function driver, such as EvtDevice and DriverUnload.

Parameters Description:

    DriverObject - represents the instance of the function driver that is loaded
    into memory. DriverEntry must initialize members of DriverObject before it
    returns to the caller. DriverObject is allocated by the system before the
    driver is loaded, and it is released by the system after the system unloads
    the function driver from memory.

RegistryPath - represents the driver specific path in the Registry.

    The function driver can use the path to store driver related data between
    reboots. The path does not store hardware instance specific data.

Return Value:

    STATUS_SUCCESS if successful,  
    STATUS_UNSUCCESSFUL otherwise.

--*/

{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;

    WDF_DRIVER_CONFIG_INIT(&config,
                    EchoEvtDeviceAdd
                    );

    status = WdfDriverCreate(DriverObject,
                            RegistryPath,
                            WDF_NO_OBJECT_ATTRIBUTES,
                            &config,
                            WDF_NO_HANDLE);

    if (!NT_SUCCESS(status)) {
        KdPrint(("Error: WdfDriverCreate failed 0x%x\n", status));
        return status;
    }

    // ...

    return status;
}

NTSTATUS
EchoEvtDeviceAdd(
    IN WDFDRIVER Driver,
    IN PWDFDEVICE_INIT DeviceInit
    )
/*++
Routine Description:

    EvtDeviceAdd is called by the framework in response to AddDevice
    call from the PnP manager. We create and initialize a device object to
    represent a new instance of the device.

Arguments:

    Driver - Handle to a framework driver object created in DriverEntry

    DeviceInit - Pointer to a framework-allocated WDFDEVICE_INIT structure.

Return Value:

    NTSTATUS

--*/
{
    NTSTATUS status;

    UNREFERENCED_PARAMETER(Driver);

    KdPrint(("Enter EchoEvtDeviceAdd\n"));

    status = EchoDeviceCreate(DeviceInit);

    return status;
}

NTSTATUS
EchoDeviceCreate(
    PWDFDEVICE_INIT DeviceInit  
/*++

Routine Description:

    Worker routine called to create a device and its software resources.

Arguments:

    DeviceInit - Pointer to an opaque init structure. Memory for this
                    structure will be freed by the framework when the WdfDeviceCreate
                    succeeds. Do not access the structure after that point.

Return Value:

    NTSTATUS

--*/  
{
    WDF_OBJECT_ATTRIBUTES deviceAttributes;
    PDEVICE_CONTEXT deviceContext;
    WDF_PNPPOWER_EVENT_CALLBACKS pnpPowerCallbacks;
    WDFDEVICE device;
    NTSTATUS status;
    UNICODE_STRING szReference;
    RtlInitUnicodeString(&szReference, L"CustomCameraSource");

    WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&pnpPowerCallbacks);

    //
    // Register pnp/power callbacks so that we can start and stop the timer as the device
    // gets started and stopped.
    //
    pnpPowerCallbacks.EvtDeviceSelfManagedIoInit = EchoEvtDeviceSelfManagedIoStart;
    pnpPowerCallbacks.EvtDeviceSelfManagedIoSuspend = EchoEvtDeviceSelfManagedIoSuspend;

    #pragma prefast(suppress: 28024, "Function used for both Init and Restart Callbacks")
    pnpPowerCallbacks.EvtDeviceSelfManagedIoRestart = EchoEvtDeviceSelfManagedIoStart;

    //
    // Register the PnP and power callbacks. Power policy related callbacks will be registered
    // later in SotwareInit.
    //
    WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, &pnpPowerCallbacks);

    {
        WDF_FILEOBJECT_CONFIG cameraFileObjectConfig;
        WDF_OBJECT_ATTRIBUTES cameraFileObjectAttributes;

        WDF_OBJECT_ATTRIBUTES_INIT(&cameraFileObjectAttributes);

        cameraFileObjectAttributes.SynchronizationScope = WdfSynchronizationScopeNone;

        WDF_FILEOBJECT_CONFIG_INIT(
            &cameraFileObjectConfig,
            EvtCameraDeviceFileCreate,
            EvtCameraDeviceFileClose,
            WDF_NO_EVENT_CALLBACK);

        WdfDeviceInitSetFileObjectConfig(
            DeviceInit,
            &cameraFileObjectConfig,
            &cameraFileObjectAttributes);
    }

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DEVICE_CONTEXT);

    status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);

    if (NT_SUCCESS(status)) {
        //
        // Get the device context and initialize it. WdfObjectGet_DEVICE_CONTEXT is an
        // inline function generated by WDF_DECLARE_CONTEXT_TYPE macro in the
        // device.h header file. This function will do the type checking and return
        // the device context. If you pass a wrong object handle
        // it will return NULL and assert if run under framework verifier mode.
        //
        deviceContext = WdfObjectGet_DEVICE_CONTEXT(device);
        deviceContext->PrivateDeviceData = 0;

        //
        // Create a device interface so that application can find and talk
        // to us.
        //
        status = WdfDeviceCreateDeviceInterface(
            device,
            &CAMERA_CATEGORY,
            &szReference // ReferenceString
            );

        if (NT_SUCCESS(status)) {
            //
            // Create a device interface so that application can find and talk
            // to us.
            //
            status = WdfDeviceCreateDeviceInterface(
            device,
            &CAPTURE_CATEGORY,
            &szReference // ReferenceString
            );
        }

        if (NT_SUCCESS(status)) {
            //
            // Create a device interface so that application can find and talk
            // to us.
            //
            status = WdfDeviceCreateDeviceInterface(
            device, 
            &VIDEO_CATEGORY,
            &szReference // ReferenceString
            );
        }

        if (NT_SUCCESS(status)) {
            //
            // Initialize the I/O Package and any Queues
            //
            status = EchoQueueInitialize(device);
        }       
    }

    return status;
}
```

### <a name="pnp-operation"></a>PnP 操作

他の物理カメラと同じように、スタブドライバーは少なくとも、基になるソースが削除またはアタッチされたときにデバイスを有効または無効にする PnP 操作を管理することをお勧めします。 たとえば、カスタムメディアソースがネットワークソース (IP カメラなど) を使用している場合、そのネットワークソースが使用できなくなったときに、デバイスの削除をトリガーすることができます。

これにより、アプリケーションは PnP Api を使用してデバイスの追加と削除をリッスンし、適切な通知を受け取ることができます。 また、使用できなくなったソースを列挙できないようにします。

UMDF および KMDF ドライバーについては、 [Wdfdevicesetdevicestate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)関数のドキュメントを参照してください。

WMD ドライバーについては、 [Iosetdeviceinterfacestate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)関数のドキュメントを参照してください。

## <a name="custom-media-source-dll"></a>カスタムメディアソース DLL

カスタムメディアソースは標準の inproc COM サーバーで、次のインターフェイスを実装する必要があります。

-   [IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

-   [IMFMediaSource](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasource)

-   [IMFMediaSourceEx](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasourceex)

-   [Iksk コントロール](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-ikscontrol)

-   [IMFGetService](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfgetservice)

> [!NOTE]
> **Imfmediasourceex**は**Imfmediasource**から継承され、 **Imfmediasource**は**imfmediaeventgenerator**から継承されます。

カスタムメディアソース内でサポートされている各ストリームは、次のインターフェイスをサポートしている必要があります。

-   **IMFMediaEventGenerator**

-   [IMFMediaStream](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediastream)

-   **IMFMediaStream2**

> [!NOTE]
> **IMFMediaStream2**は**Imfmediastream**から継承し、Imfmediastream は**imfmediaeventgenerator**から継承します。

カスタムメディアソースを作成する方法については、[カスタムメディアソース](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source)の作成に関するドキュメントを参照してください。 このセクションの残りの部分では、フレームサーバーフレームワーク内でカスタムメディアソースをサポートするために必要な違いについて説明します。

### <a name="imfgetservice"></a>IMFGetService

**IMFGetService**は、フレームサーバーカスタムメディアソースに必須のインターフェイスです。 カスタムメディアソースが追加のサービスインターフェイスを公開する必要がない場合、 **IMFGetService**は、サポートされて**いない\_サービス\_、MF\_E**を返すことがあります。

次の例は、サポートサービスインターフェイスのない**IMFGetService**実装を示しています。

```cpp
_Use_decl_annotations_
IFACEMETHODIMP
SimpleMediaSource::GetService(
    _In_ REFGUID guidService,
    _In_ REFIID riid,
    _Out_ LPVOID * ppvObject
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());

    if (!ppvObject)
    {
        return E_POINTER;
    }
    *ppvObject = NULL;

    // We have no supported service, just return
    // MF_E_UNSUPPORTED_SERVICE for all calls.

    return MF_E_UNSUPPORTED_SERVICE;
}
```

### <a name="imfmediaeventgenerator"></a>IMFMediaEventGenerator

上に示すように、ソース内のソースと個々のストリームは、それぞれ独自の[Imfmediaeventgenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)インターフェイスをサポートしている必要があります。 ソースからのすべての MF パイプラインデータおよび制御フローは、特定の[Imfmediaevent](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaevent)を送信することによって、イベントジェネレーターによって管理されます。

IMFMediaEventGenerator を実装する場合、カスタムメディアソースは、 [](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreateeventqueue)次のように、mffmediaeventqueue API を使用して imfmediaeventgenerator を作成し、 **imfmediaeventgenerator**のすべてのメソッドをキューオブジェクトにルーティングする必要があります。 [](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventqueue)

**Imfmediaeventgenerator**には、次のメソッドがあります。

```cpp
// IMFMediaEventGenerator
IFACEMETHOD(BeginGetEvent)(_In_ IMFAsyncCallback *pCallback, _In_ IUnknown *punkState);
IFACEMETHOD(EndGetEvent)(_In_ IMFAsyncResult *pResult, _COM_Outptr_ IMFMediaEvent **ppEvent);
IFACEMETHOD(GetEvent)(DWORD dwFlags, _Out_ IMFMediaEvent **ppEvent);
IFACEMETHOD(QueueEvent)(MediaEventType met, REFGUID guidExtendedType, HRESULT hrStatus, _In_opt_ const PROPVARIANT *pvValue);
```

次のコードは、 **Imfmediaeventgenerator**インターフェイスの推奨される実装を示しています。 カスタムメディアソースの実装は**Imfmediaeventgenerator**インターフェイスを公開し、そのインターフェイスのメソッドは、メディアソースの作成時に作成された**Imfmediaeventgenerator**オブジェクトに要求をルーティングします。イニシャライズ.

次のコードでは、 **\_speventqueue**オブジェクトは、 **mfcreateeventqueue**関数を使用して作成された**imfmediaeventqueue**です。

```cpp
// IMFMediaEventGenerator methods
IFACEMETHODIMP
SimpleMediaSource::BeginGetEvent(
    _In_ IMFAsyncCallback *pCallback,
    _In_ IUnknown *punkState
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (_spEventQueue->BeginGetEvent(pCallback, punkState));

    return hr;
}

IFACEMETHODIMP
SimpleMediaSource::EndGetEvent(
    _In_ IMFAsyncResult *pResult,
    _COM_Outptr_ IMFMediaEvent **ppEvent
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (_spEventQueue->EndGetEvent(pResult, ppEvent));

    return hr;
}

IFACEMETHODIMP
SimpleMediaSource::GetEvent(
    DWORD dwFlags,
    _COM_Outptr_ IMFMediaEvent **ppEvent
    )
{
    // NOTE:
    // GetEvent can block indefinitely, so we do not hold the lock.
    // This requires some juggling with the event queue pointer.

    HRESULT hr = S_OK;

    ComPtr<IMFMediaEventQueue> spQueue;

    {
        auto lock = _critSec.Lock();

        RETURN_IF_FAILED (_CheckShutdownRequiresLock());
        spQueue = _spEventQueue;
    }

    // Now get the event.
    RETURN_IF_FAILED (_spEventQueue->GetEvent(dwFlags, ppEvent));

    return hr;
}

IFACEMETHODIMP
SimpleMediaSource::QueueEvent(
    MediaEventType eventType,
    REFGUID guidExtendedType,
    HRESULT hrStatus,
    _In_opt_ PROPVARIANT const *pvValue
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (_spEventQueue->QueueEventParamVar(eventType, guidExtendedType, hrStatus, pvValue));

    return hr;
}
```

### <a name="seeking-and-pausing"></a>シークと一時停止

フレームサーバーフレームワークでサポートされているカスタムメディアソースでは、シーク操作または一時停止操作はサポートされていません。 カスタムメディアソースは、これらの操作のサポートを提供する必要がなく、 **MFSourceSeeked**イベントまたは**MEStreamSeeked**イベントをポストしないようにする必要があります。

[Imfmediasource::P ause](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-pause)は、**無効な\_状態\_遷移**(または、ソースが既にシャットダウンされている場合は、 **mf\_E\_シャットダウン**) を\_、mf\_e を返す必要があります。

### <a name="ikscontrol"></a>Iksk コントロール

[Ikscontrol](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-ikscontrol)は、すべてのカメラ関連コントロールの標準コントロールインターフェイスです。 カスタムメディアソースでカメラコントロールが実装されている場合、 **Iksk コントロール**インターフェイスは、パイプラインが制御 i/o をルーティングする方法を示します。

詳細については、次のコントロールセットに関するドキュメントのトピックを参照してください。

-   [PROPSETID_VIDCAP_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)

-   [PROPSETID_VIDCAP_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)

-   [KSPROPERTYSETID_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)

これらのコントロールは省略可能であり、サポートされていない場合、返されるエラーコードは **\_WIN32 からの HRESULT\_です (エラー\_設定\_\_見つかりません)** 。

次のコードは、サポートされていないコントロールを使用した**Iksk コントロール**の実装例です。

```cpp
// IKsControl methods
_Use_decl_annotations_
IFACEMETHODIMP
SimpleMediaSource::KsProperty(
    _In_reads_bytes_(ulPropertyLength) PKSPROPERTY pProperty,
    _In_ ULONG ulPropertyLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pPropertyData,
    _In_ ULONG ulDataLength,
    _Out_ ULONG* pBytesReturned
    )
{
    // ERROR_SET_NOT_FOUND is the standard error code returned
    // by the AV Stream driver framework when a miniport
    // driver does not register a handler for a KS operation.
    // We want to mimic the driver behavior here if we do not
    // support controls.
    return HRESULT_FROM_WIN32(ERROR_SET_NOT_FOUND);
}

_Use_decl_annotations_
IFACEMETHODIMP SimpleMediaSource::KsMethod(
    _In_reads_bytes_(ulMethodLength) PKSMETHOD pMethod,
    _In_ ULONG ulMethodLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pMethodData,
    _In_ ULONG ulDataLength,
    _Out_ ULONG* pBytesReturned
    )
{
    return HRESULT_FROM_WIN32(ERROR_SET_NOT_FOUND);
}

_Use_decl_annotations_
IFACEMETHODIMP SimpleMediaSource::KsEvent(
    _In_reads_bytes_opt_(ulEventLength) PKSEVENT pEvent,
    _In_ ULONG ulEventLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pEventData,
    _In_ ULONG ulDataLength,
    _Out_opt_ ULONG* pBytesReturned
    )
{
    return HRESULT_FROM_WIN32(ERROR_SET_NOT_FOUND);
}
```

### <a name="imfmediastream2"></a>IMFMediaStream2

「[カスタムメディアソースの作成](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source)」で説明されているように、 [Imfmediasource:: Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)メソッドの完了時にソースイベントキューにポストされた[menewstream](https://docs.microsoft.com/windows/desktop/medfound/menewstream)メディアイベントを使用して、カスタムメディアソースからフレーム作業に**IMFMediaStream2**インターフェイスを提供します。

```cpp
IFACEMETHODIMP
SimpleMediaSource::Start(
    _In_ IMFPresentationDescriptor *pPresentationDescriptor,
    _In_opt_ const GUID *pguidTimeFormat,
    _In_ const PROPVARIANT *pvarStartPos
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();
    DWORD count = 0;
    PROPVARIANT startTime;
    BOOL selected = false;
    ComPtr<IMFStreamDescriptor> streamDesc;
    DWORD streamIndex = 0;

    if (pPresentationDescriptor == nullptr || pvarStartPos == nullptr)
    {
        return E_INVALIDARG;
    }
    else if (pguidTimeFormat != nullptr && *pguidTimeFormat != GUID_NULL)
    {
        return MF_E_UNSUPPORTED_TIME_FORMAT;
    }

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());

    if (_sourceState != SourceState::Stopped)
    {
        return MF_E_INVALID_STATE_TRANSITION;
    }

    _sourceState = SourceState::Started;

    // This checks the passed in PresentationDescriptor matches the member of streams we
    // have defined internally and that at least one stream is selected

    RETURN_IF_FAILED (_ValidatePresentationDescriptor(pPresentationDescriptor));
    RETURN_IF_FAILED (pPresentationDescriptor->GetStreamDescriptorCount(&count));
    RETURN_IF_FAILED (InitPropVariantFromInt64(MFGetSystemTime(), &startTime));

    // Send event that the source started. Include error code in case it failed.
    RETURN_IF_FAILED (_spEventQueue->QueueEventParamVar(MESourceStarted,
                                                            GUID_NULL,
                                                            hr,
                                                            &startTime));

    // We are hardcoding this to the first descriptor
    // since this sample is a single stream sample. For
    // multiple streams, we need to walk the list of streams
    // and for each selected stream, send the MEUpdatedStream
    // or MENewStream event along with the MEStreamStarted
    // event.
    RETURN_IF_FAILED (pPresentationDescriptor->GetStreamDescriptorByIndex(0,
                                                                            &selected,
                                                                            &streamDesc));

    RETURN_IF_FAILED (streamDesc->GetStreamIdentifier(&streamIndex));
    if (streamIndex >= NUM_STREAMS)
    {
        return MF_E_INVALIDSTREAMNUMBER;
    }

    if (selected)
    {
        ComPtr<IUnknown> spunkStream;
        MediaEventType met = (_wasStreamPreviouslySelected ? MEUpdatedStream : MENewStream);

        // Update our internal PresentationDescriptor
        RETURN_IF_FAILED (_spPresentationDescriptor->SelectStream(streamIndex));
        RETURN_IF_FAILED (_stream.Get()->SetStreamState(MF_STREAM_STATE_RUNNING));
        RETURN_IF_FAILED (_stream.As(&spunkStream));

        // Send the MEUpdatedStream/MENewStream to our source event
        // queue.

        RETURN_IF_FAILED (_spEventQueue->QueueEventParamUnk(met,
                                                                GUID_NULL,
                                                                S_OK,
                                                                spunkStream.Get()));

        // But for our stream started (MEStreamStarted), we post to our
        // stream event queue.
        RETURN_IF_FAILED (_stream.Get()->QueueEvent(MEStreamStarted,
                                                        GUID_NULL,
                                                        S_OK,
                                                        &startTime));
    }
    _wasStreamPreviouslySelected = selected;

    return hr;
}
```

これは、 [Imfプレゼンテーション記述子](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfpresentationdescriptor)によって選択されたストリームごとに実行する必要があります。

ビデオストリームを使用したカスタムメディアソースの場合、 [Meendofstream](https://docs.microsoft.com/windows/desktop/medfound/meendofstream)イベントと[meendofstream](https://docs.microsoft.com/windows/desktop/medfound/meendofpresentation)イベントを送信することはできません。

### <a name="stream-attributes"></a>ストリーム属性

すべてのカスタムメディアソースストリームには、 [MF_DEVICESTREAM_STREAM_CATEGORY](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category)を**PINNAME\_VIDEO\_CAPTURE**として設定する必要があります。 カスタムメディアソースでは、 **Pinname\_VIDEO\_PREVIEW**はサポートされていません。

> [!NOTE]
> **Pinname\_IMAGE**はサポートされていますが、推奨されていません。 **Pinname\_IMAGE**でストリームを公開するには、すべてのフォトトリガーコントロールをサポートするためにカスタムメディアソースが必要です。 詳細については、後述の「[写真ストリームコントロール](#photo-stream-controls)」セクションを参照してください。

[MF_DEVICESTREAM_STREAM_ID](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-id)は、すべてのストリームに必須の属性です。 0から始まるインデックスを指定する必要があります。 そのため、最初のストリームの ID は0、2番目のストリームの ID は1のようになります。

ストリームで推奨される属性の一覧を次に示します。

-   [MF_DEVICESTREAM_ATTRIBUTE_FRAMESOURCE_TYPES](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-attribute-framesource-types)

-   [MF_DEVICESTREAM_FRAMESERVER_SHARED](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-frameserver-shared)

#### <a name="mf_devicestream_attribute_framesource_types"></a>MF\_DEVICESTREAM\_属性\_FRAMESOURCE\_型

**MF\_DEVICESTREAM\_属性\_FRAMESOURCE\_TYPES**は、ストリーム型のビットマスク値である UINT32 属性です。 次のいずれかに設定されている場合があります (これらの型はビットマスクフラグですが、可能な限りソースの種類を混在させないことをお勧めします)。

| 種類                         | Flag   | 説明                                      |
|------------------------------|--------|--------------------------------------------------|
| MFFrameSourceTypes\_Color    | 0x0001 | 標準の RGB カラーストリーム                        |
| MFFrameSourceTypes\_赤外線 | 0x0002 | IR ストリーム                                        |
| MFFrameSourceTypes\_の深さ    | 0x0004 | 深度ストリーム                                     |
| MFFrameSourceTypes\_イメージ    | 0x0008 | イメージストリーム (ビデオ以外のサブタイプ、通常は JPEG) |
| MFFrameSourceTypes\_カスタム   | 0x0080 | カスタムストリームの種類                               |

#### <a name="mf_devicestream_frameserver_shared"></a>MF\_DEVICESTREAM\_FRAMESERVER\_SHARED

**MF\_DEVICESTREAM\_FRAMESERVER\_SHARED**は、0または1のいずれかに設定できる UINT32 属性です。 1に設定すると、フレームサーバーによってストリームが "共有可能" としてマークされます。 これにより、他のアプリで使用されている場合でも、アプリケーションは共有モードでストリームを開くことができます。

この属性が設定されていない場合、フレームサーバーでは、最初のマークされていないストリームを共有できます (カスタムメディアソースにストリームが1つしかない場合、そのストリームは共有としてマークされます)。

この属性が0に設定されている場合、フレームサーバーは共有アプリからのストリームをブロックします。 カスタムメディアソースで、この属性が0に設定されているすべてのストリームがマークされている場合、共有アプリケーションはソースを初期化できません。

### <a name="sample-allocation"></a>割り当てのサンプル

すべてのメディアフレームは[Imfsample](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfsample)として生成される必要があります。 カスタムメディアソースでは、 [Mfcreatesample](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatesample)のインスタンスを割り当て、 [addbuffer](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfsample-addbuffer)メソッドを使用してメディアバッファーを追加する必要があります。

各**Imfsample**には、サンプル時間とサンプル期間を設定する必要があります。 すべてのサンプルタイムスタンプは、QPC の時刻 (QueryPerformanceCounter) に基づいている必要があります。

カスタムメディアソースでは、可能な限り、 [Mfgetsystemtime](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfgetsystemtime)関数を使用することをお勧めします。 この関数は、 **Queryperformancecounter**のラッパーであり、qpc タイマー刻みを100ナノ秒単位に変換します。

カスタムメディアソースは内部時計を使用する場合がありますが、すべてのタイムスタンプは、現在の QPC に基づく100ナノ秒単位に関連付けられている必要があります。

#### <a name="media-buffer"></a>メディアバッファー

**Imfsample**に追加されるすべてのメディアバッファーは、標準の MF バッファー割り当て関数を使用する必要があります。 カスタムメディアソースは、独自の[IMFMediaBuffer](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediabuffer)インターフェイスを実装したり、メディアバッファーを直接割り当てることはできません (たとえば、new/Malloc/VirtualAlloc などをフレームデータに対して使用しないでください)。

次のいずれかの Api を使用して、メディアフレームを割り当てます。

-   [MFCreateMemoryBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatememorybuffer)

-   [MFCreateAlignedMemoryBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatealignedmemorybuffer)

-   [MFCreate2DMediaBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreate2dmediabuffer)

-   [MFCreateDXGISurfaceBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatedxgisurfacebuffer)

**MFCreateMemoryBuffer**と**MFCreateAlignedMemoryBuffer**は、非 stride アラインメディアデータに対して使用する必要があります。 通常、これらはカスタムのサブタイプまたは圧縮されたサブタイプ (H264/HEVC/MJPG など) です。

システムメモリを使用する一般的な非圧縮メディアの種類 (YUY2、NV12 など) については、 **MFCreate2DMediaBuffer**を使用することをお勧めします。

DX サーフェイスを使用する場合 (レンダリングやエンコードなどの GPU アクセラレータ操作の場合) は、 **MFCreateDXGISurfaceBuffer**を使用する必要があります。

**MFCreateDXGISurfaceBuffer**では、DX サーフェイスは作成されません。 サーフェイスは、 [Imfmediasourceex:: SetD3DManager](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-setd3dmanager)メソッドを使用してメディアソースに渡される DXGI マネージャーを使用して作成されます。

[Imfdxgidevicemanager:: OpenDeviceHandle](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-opendevicehandle)は、選択した D3D デバイスに関連付けられているハンドルを提供します。 [ID3D11Device](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11device)インターフェイスは、 [Imfdxgidevicemanager:: getvideoservice](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-getvideoservice)メソッドを使用して取得できます。

使用されるバッファーの種類に関係なく、作成された**Imfsample**は、メディアストリームの**Imfmediaeventgenerator**にある**memediasample**イベントを使用してパイプラインに提供する必要があります。

カスタムメディアソースと**imfmediastream**の基になるコレクションの両方に同じ**Imfmediaeventqueue**を使用できますが、これを行うと、メディアソースイベントとストリームイベントのシリアル化が行われることに注意する必要があります (これには、メディアフローが含まれます)。 複数のストリームを含むソースの場合、これは望ましくありません。

次のコード領域は、メディアストリームの実装例を示しています。

```cpp
IFACEMETHODIMP
    SimpleMediaStream::RequestSample(
    _In_ IUnknown *pToken
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();
    ComPtr<IMFSample> sample;
    ComPtr<IMFMediaBuffer> outputBuffer;
    LONG pitch = IMAGE_ROW_SIZE_BYTES;
    BYTE *bufferStart = nullptr; // not used
    DWORD bufferLength = 0;
    BYTE *pbuf = nullptr;
    ComPtr<IMF2DBuffer2> buffer2D;

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (MFCreateSample(&sample));
    RETURN_IF_FAILED (MFCreate2DMediaBuffer(NUM_IMAGE_COLS,
                                            NUM_IMAGE_ROWS,
                                            D3DFMT_X8R8G8B8,
                                            false,
                                            &outputBuffer));
    RETURN_IF_FAILED (outputBuffer.As(&buffer2D));
    RETURN_IF_FAILED (buffer2D->Lock2DSize(MF2DBuffer_LockFlags_Write,
                                                &pbuf,
                                                &pitch,
                                                &bufferStart,
                                                &bufferLength));
    RETURN_IF_FAILED (WriteSampleData(pbuf, pitch, bufferLength));
    RETURN_IF_FAILED (buffer2D->Unlock2D());
    RETURN_IF_FAILED (sample->AddBuffer(outputBuffer.Get()));
    RETURN_IF_FAILED (sample->SetSampleTime(MFGetSystemTime()));
    RETURN_IF_FAILED (sample->SetSampleDuration(333333));
    if (pToken != nullptr)
    {
        RETURN_IF_FAILED (sample->SetUnknown(MFSampleExtension_Token, pToken));
    }
    RETURN_IF_FAILED (_spEventQueue->QueueEventParamUnk(MEMediaSample,
                                                            GUID_NULL,
                                                            S_OK,
                                                            sample.Get()));

    return hr;
}
```

## <a name="custom-media-source-extension-to-expose-imfactivate-available-in-windows-10-version-1809"></a>IMFActivate を公開するカスタムメディアソース拡張機能 (Windows 10 バージョン1809で使用可能)

カスタムメディアソースに対してサポートする必要がある上記のインターフェイスの一覧に加えて、フレームサーバーアーキテクチャ内でカスタムメディアソース操作によって課される制限事項の1つに、UMDF ドライバー "アクティブ化" のインスタンスは1つしか存在できないということがあります。パイプラインを使用します。

たとえば、非 AV ストリームドライバーパッケージに加えて UMDF スタブドライバーをインストールし、それらの物理デバイスの1つをコンピューターに接続し、各 UMDF ドライバーの各インスタンスが一意のシンボリックリンク名を取得する物理デバイスがあるとします。では、カスタムメディアソースのアクティブ化パスには、作成時にカスタムメディアソースに関連付けられたシンボリックリンク名を通信する手段がありません。

カスタムメディアソースは、 [Imfmediasource:: Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)が呼び出されたときに、カスタムメディアソースの属性ストア ( [Imfmediasourceex:: getsourceattributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)メソッドを介してカスタムメディアソースから返された属性ストア) の標準[MF_DEVSOURCE_ATTRIBUTE_SOURCE_TYPE_VIDCAP_SYMBOLIC_LINK](https://docs.microsoft.com/windows/desktop/medfound/mf-devsource-attribute-source-type-vidcap-symbolic-link)属性を検索する場合があります。

ただし、これにより起動時の待機時間が長くなる可能性があります。これは、ハードウェアリソースの取得が作成/初期化時ではなく開始時刻になるためです。

このため、Windows 10 バージョン1809では、必要に応じてカスタムメディアソースが[Imfactivate](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfactivate)インターフェイスを公開する場合があります。

> [!NOTE] 
> **Imfactivate**は[imfactivate](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfattributes)から継承します。

### <a name="imfactivate"></a>IMFActivate

カスタムメディアソースの COM サーバーが**imfactivate**インターフェイスをサポートしている場合、 **imfactivate**によって継承された**imfactivate**を通じて、デバイスの初期化情報が com サーバーに提供されます。 [Imfactivate:: Activate オブジェクト](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-activateobject)が呼び出されると、 **imfactivate**の属性ストアには、UMDF スタブドライバーのシンボリックリンク名と、パイプライン/アプリケーションによって提供されるその他の構成設定が含まれます。ソースの作成/初期化の。

カスタムメディアソースは、このメソッド呼び出しを使用して、必要なハードウェアリソースを取得する必要があります。

> [!NOTE]
> ハードウェアリソースの取得にかかる時間が200ミリ秒を超える場合は、ハードウェアリソースを非同期に取得することをお勧めします。 カスタムメディアソースのライセンス認証では、ハードウェアリソースの取得をブロックしないでください。 代わりに、 [Imfmediasource:: Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)操作をハードウェアリソースの取得に対してシリアル化する必要があります。

**Imfactivate**、 [DetachObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-detachobject) 、および[ShutdownObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-shutdownobject)によって公開されている2つの追加のメソッドは、 **E\_NOTIMPL**を返す必要があります。

カスタムメディアソースは、 [Imfmediasource](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasource)と同じ COM オブジェクト内に**imfactivate**および**imfactivate**インターフェイスを実装することができます。 これを行う場合は、 [Imfmediasourceex:: GetSourceAttributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)が**imfactivate**と同じ**imfattributes**インターフェイスを返すことをお勧めします。

カスタムメディアソースが、同じオブジェクトを使用して**imfactivate**および**imfactivate**を実装していない場合、カスタムメディアソースは、 **imfactivate**属性ストアに設定されているすべての属性をカスタムメディアソースのソースにコピーする必要があります。属性ストア。

## <a name="encoded-camera-stream"></a>エンコードされたカメラストリーム

カスタムメディアソースは、圧縮されたメディアの種類 (HEVC または H264 の基本ストリーム) を公開する場合があり、OS パイプラインはカスタムメディアソースのエンコードパラメーターのソースと構成を完全にサポートします (エンコーディングパラメーターは、[ICodecAPI](https://docs.microsoft.com/previous-versions/windows/desktop/api/strmif/nn-strmif-icodecapi)は、 [Ikscontrol:: ksk プロパティ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksproperty)呼び出しとしてルーティングされます。

```cpp
// IKsControl methods
_Use_decl_annotations_
IFACEMETHODIMP
SimpleMediaSource::KsProperty(
    _In_reads_bytes_(ulPropertyLength) PKSPROPERTY pProperty,
    _In_ ULONG ulPropertyLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pPropertyData,
    _In_ ULONG ulDataLength,
    _Out_ ULONG* pBytesReturned
    );
```

**Ikscontrol:: Ksk プロパティ**メソッドに渡される**ksk プロパティ**構造体には、次の情報が含まれます。

```cpp
KSPROPERTY.Set = Encoder Property GUID
KSPROPERTY.Id = 0
KSPROPERTY.Flags = (KSPROPERTY_TYPE_SET or KSPROPERTY_TYPE_GET)
```

エンコーダーのプロパティ GUID は、[コーデック API のプロパティ](https://docs.microsoft.com/windows/desktop/DirectShow/codec-api-properties)で定義されている使用可能なプロパティの一覧です。

エンコーダープロパティのペイロードは、前に宣言した**Ksk プロパティ**メソッドの*ppropertydata*フィールドを介して渡されます。

### <a name="capture-engine-requirements"></a>キャプチャエンジンの要件

エンコードされたソースはフレームサーバーによって完全にサポートされていますが、 [MediaCapture](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture)オブジェクトによって使用されるクライアント側キャプチャエンジン (**IMFCaptureEngine**) には追加の要件があります。

-   ストリームは、すべてエンコードされている (HEVC または H264) か、すべて非圧縮である必要があります (このコンテキストでは、MJPG は非圧縮として扱われます)。

-   少なくとも1つの圧縮されていないストリームが使用可能である必要があります。

> [!NOTE]
> これらの要件は、このトピックで説明するカスタムメディアソースの要件に追加されます。 ただし、キャプチャエンジンの要件は、クライアントアプリケーションが**IMFCaptureEngine**または**MediaCapture** API を介してカスタムメディアソースを使用する場合にのみ適用されます。

## <a name="camera-profiles-available-in-windows-10-version-1803-and-later"></a>カメラプロファイル (Windows 10 バージョン1803以降で使用可能)

カスタムメディアソースでは、カメラプロファイルのサポートを利用できます。 推奨されるメカニズムは、 **MF\_DEVICEMFT\_SENSORPROFILE\_COLLECTION**属性を使用して、ソース属性 ([Imfmediasourceex:: getsourceattributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)) からプロファイルを発行することです。

**MF\_DEVICEMFT\_SENSORPROFILE\_COLLECTION**属性は、 [Imfsensorprofilecollection](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfsensorprofilecollection)インターフェイスの**IUnknown**です。 **Imfsensorprofilecollection**は、次のように、 [Mf、ensorprofilecollection](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatesensorprofilecollection)関数を使用して取得できます。

```cpp
IFACEMETHODIMP
SimpleMediaSource::GetSourceAttributes(
    _COM_Outptr_ IMFAttributes** sourceAttributes
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    if (nullptr == sourceAttributes)
    {
        return E_POINTER;
    }

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());

    *sourceAttributes = nullptr;
    if (_spAttributes.Get() == nullptr)
    {
        ComPtr<IMFSensorProfileCollection> profileCollection;
        ComPtr<IMFSensorProfile> profile;

        // Create our source attribute store
        RETURN_IF_FAILED (MFCreateAttributes(_spAttributes.GetAddressOf(), 1));

        // Create an empty profile collection
        RETURN_IF_FAILED (MFCreateSensorProfileCollection(&profileCollection));

        // In this example since we have just one stream, we only have one
        // pin to add: Pin0

        // Legacy profile is mandatory. This is to ensure non-profile
        // aware applications can still function, but with degraded
        // feature sets.
        RETURN_IF_FAILED (MFCreateSensorProfile(KSCAMERAPROFILE_Legacy, 0, nullptr,
                                                profile.ReleaseAndGetAddressOf()));
        RETURN_IF_FAILED (profile->AddProfileFilter(0, L"((RES==;FRT<=30,1;SUT==))"));
        RETURN_IF_FAILED (profileCollection->AddProfile(profile.Get()));

        // High Frame Rate profile will only allow >=60fps
        RETURN_IF_FAILED (MFCreateSensorProfile(KSCAMERAPROFILE_HighFrameRate, 0, nullptr,
                                                profile.ReleaseAndGetAddressOf()));
        RETURN_IF_FAILED (profile->AddProfileFilter(0, L"((RES==;FRT>=60,1;SUT==))"));
        RETURN_IF_FAILED (profileCollection->AddProfile(profile.Get()));

        // See the profile collection to the attribute store of the IMFTransform
        RETURN_IF_FAILED (_spAttributes->SetUnknown(MF_DEVICEMFT_SENSORPROFILE_COLLECTION,
                                                        profileCollection.Get()));
    }

    return _spAttributes.CopyTo(sourceAttributes);
}
```

### <a name="face-authentication-profile"></a>顔認証プロファイル

カスタムメディアソースが Windows Hello 顔認識をサポートするように設計されている場合は、顔認証プロファイルを公開することをお勧めします。 顔認証プロファイルの要件は次のとおりです。

-   Face Authentication DDI コントロールは、単一の IR ストリームでサポートされている必要があります。 詳細については、「 [KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode)」を参照してください。

-   IR ストリームは、15 fps で 340 x 340 以上である必要があります。 形式は、l8 圧縮でマークされた L8、NV12、または MJPG のいずれかである必要があります。

-   RGB ストリームは、7.5 fps で 480 x 480 以上である必要があります (これは、Multispectrum 認証が適用されている場合にのみ必要です)。

-   顔認証プロファイルのプロファイル ID は、KSCAMERAPROFILE\_FaceAuth\_Mode、0である必要があります。

顔認証プロファイルでは、IR および RGB ストリームごとに1種類のメディアをアドバタイズすることをお勧めします。

## <a name="photo-stream-controls"></a>フォトストリームコントロール

ストリームのいずれかの[MF\_DEVICESTREAM\_ストリームの\_カテゴリ](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category)を**ピン名\_イメージ**としてマークすることによって、独立したフォトストリームが公開されている場合は、ストリームカテゴリの**pinname\_VIDEO というストリームを\_キャプチャ**が必要です (たとえば、 **pinname\_イメージ**だけを公開する1つのストリームが有効なメディアソースではありません)。

**Iksk コントロール**を使用して、 **PROPSETID\_VIDCAP\_videocontrol**プロパティセットをサポートする必要があります。 詳細については、「[ビデオコントロールのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/video-control-properties)」を参照してください。
