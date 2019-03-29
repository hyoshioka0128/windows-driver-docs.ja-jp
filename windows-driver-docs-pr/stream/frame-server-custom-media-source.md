---
title: フレーム サーバーのカスタム メディア ソース
description: フレーム サーバー アーキテクチャ内でカスタム メディア ソースの実装について説明します。
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 825540b9854f2431017c8ce86772ec7119f406b1
ms.sourcegitcommit: 68bfa1f69229b7ac29d0e98f049734f5bc566a30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58187471"
---
# <a name="frame-server-custom-media-source"></a>フレーム サーバーのカスタム メディア ソース 

このトピックでは、フレーム サーバー アーキテクチャ内でカスタム メディア ソースの実装について説明します。 

## <a name="av-stream-and-custom-media-source-options"></a>AV Stream とカスタム メディア ソース オプション

ビデオ キャプチャ フレーム サーバー アーキテクチャ内のストリームのサポートを提供する方法を決定する際に、2 つの主なオプションがあります。AV Stream とカスタム メディア ソース。

AV Stream モデルは、AV Stream ミニポート ドライバー (カーネル モード ドライバー) を使用して、標準カメラ ドライバー モデルです。 通常、AV Stream ドライバーは、2 つの主なカテゴリに分類されます。MIPI ベースのドライバーと USB ビデオ クラス ドライバー。

カスタムのメディア ソース オプションのドライバー モデルが完全にカスタムあります (専用) または非従来カメラ ソース (ファイル、ネットワーク ソースなど) に基づいて。

### <a name="av-stream-driver"></a>AV Stream ドライバー

AV Stream ドライバー アプローチの主な利点は、PnP と管理/デバイスの電源管理は、AV Stream フレームワークによって既に処理します。

ただし、基になるソースは、ハードウェアとのインターフェイスのカーネル モード ドライバーを使用した物理デバイスである必要がありますも意味します。 UVC デバイスでは、Windows UVC 1.5 クラス ドライバーが提供される受信トレイのためデバイスが単にファームウェアを実装する必要があります。

MIPI ベースのデバイスでは、仕入先は、独自の AV Stream ミニポート ドライバーを実装する必要があります。

### <a name="custom-media-source"></a>カスタムのメディア ソース

(ただし、AV Stream ミニポート ドライバーではなく) がデバイス ドライバが既にソースまたは非従来のカメラ キャプチャを使用するソースの場合、AV Stream ドライバーの実行可能なない場合があります。 たとえば、ネットワーク経由で接続されている、IP カメラも適合しない AV Stream ドライバー モデルに。

このような状況では、フレームのサーバー モデルを使用してカスタム メディア ソースを別の方法となります。

| 機能 | カスタムのメディア ソース | AV Stream ドライバー |
|---|---|---|
| PnP や電源管理 | ソースまたはスタブ ドライバーによって実装する必要があります。 | AV Stream フレームワークによって提供されます。 |
| ユーザー モードのプラグイン       | 使用できません。 カスタムのメディア ソースには、OEM/IHV の特定のユーザー モードのロジックが組み込まれています。 | DMFT、プラットフォーム DMFT、および従来の実装の MFT0 |
| センサーのグループ | サポートされている | サポートされている |
| カメラ プロファイル V2 | サポートされている | サポートされている |
| カメラ プロファイル V1 | サポートされていません | サポートされている |

## <a name="custom-media-source-requirements"></a>カスタムのメディア ソースの要件

Windows カメラ フレームのサーバー (サーバーのフレームと呼ばれる) サービスの導入に伴いは、これはカスタム メディア ソースを使って実現できます。 これには、2 つの主要なコンポーネントが必要です。

-   カメラ デバイスのインターフェイスを登録/有効にするように設計されたスタブ ドライバーを使用したドライバー パッケージ。

-   カスタムのメディア ソースをホストする COM DLL です。

2 つの目的は、最初の要件が必要です。

-   (ドライバー パッケージには、WHQL の認定が必要です)、信頼されたプロセスを通じてカスタム メディア ソースを使用して審査プロセスがインストールされます。

-   標準の PnP 列挙型と「カメラ」の検出をサポートします。

### <a name="security"></a>セキュリティ

フレームのサーバーのカスタム メディア ソースは、次のようにセキュリティの観点からは、汎用のカスタム メディア ソースとは異なります。

-   ローカル サービス (ローカル システムと混同しないとしてフレーム サーバー カスタム メディア ソースが実行されます。ローカル サービスは、Windows マシンでの非常に低い特権付きアカウント)。

-   フレーム サーバー カスタム メディア ソースは、セッション 0 (システム サービスのセッション) で実行され、ユーザーのデスクトップと対話できません。

これらの制約を指定するには、フレーム サーバー カスタム メディア ソースしようとしないで、ファイル システムやレジストリの保護された部分にアクセスします。 通常、読み取りアクセスが許可されているが、書き込みアクセス権がありません。

### <a name="performance"></a>パフォーマンス

、、フレームのサーバー モデルの一部として 2 つのケースをフレーム サーバーによってカスタム メディア ソースがインスタンス化される方法でがあります。

-   センサーの中に生成/公開をグループ化します。

-   「カメラ」アクティブ化時に

センサーのグループの生成は通常、デバイスのインストールや電源サイクル中に行われます。 そのため、強くお勧めカスタム メディア ソースがその作成時に、大量の処理を回避し、に対してこのようなアクティビティの遅延、 [IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)関数。 カスタム メディア ソースを開始する、さまざまな使用可能なストリーム/メディアの種類とソース/ストリーム属性情報をクエリだけでは、センサー グループ生成を試行しません。

## <a name="stub-driver"></a>スタブのドライバー

ドライバー パッケージとスタブのドライバーの 2 つの最小要件があります。

スタブのドライバーは、(UMDF または KMDF) WDF または WDM ドライバー モデルを使用して記述できます。

ドライバーの要件は次のとおりです。

-   で、「カメラ」(カスタムのメディア ソース) デバイスのインターフェイスを登録、 [KSCATEGORY_VIDEO_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video-camera)カテゴリに列挙できるようにします。

> [!NOTE]
> DirectShow のレガシ アプリケーションによって列挙できるようにには、ドライバーが も登録する必要があります、 [KSCATEGORY_VIDEO](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video)と[KSCATEGORY_CAPTURE](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-capture)します。

-   デバイスのインターフェイス ノードの下のレジストリ エントリを追加 (を使用して、 **AddReg** 、ドライバーの INF ディレクティブ**DDInstall.Interface**セクション) CoCreate 可能なカスタム メディアのソース COM の CLSID を宣言していますオブジェクト。 これは、次のレジストリ値の名前を使用して追加する必要があります。**CustomCaptureSourceClsid**します。

これは「カメラ」ソースがアプリケーションによって検出され、アクティブになると通知をアクティブ化の呼び出しをインターセプトし、カスタム メディアの一緒ソースに再ルーティングする場合、フレーム サーバー サービス。

### <a name="sample-inf"></a>サンプル INF

次の例は、カスタム メディア ソース スタブ ドライバーの一般的な INF を示しています。

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

上記のカスタム メディア ソースを登録**KSCATEGORY\_ビデオ**、 **KSCATEGORY\_キャプチャ**、および**KSCATEGORY\_ビデオ\_カメラ**「カメラ」は標準の RGB カメラを探して UWP と UWP 以外のアプリが検出できるようにすることを確認します。

必要に応じてカスタム メディア ソースも RGB 非ストリーム (IR、深さ、およびなど) を公開している場合は登録することも、 [KSCATEGORY_SENSOR_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-sensor-camera)します。

> [!NOTE]
> ほとんどの USB ベースの web カメラを公開 YUY2 と MJPG 形式。 この動作により多くのレガシ DirectShow アプリケーションは YUY2/MJPG が使用できることを前提に書き込まれます。 このようなアプリケーションとの互換性を確認するには、YUY2 メディアの種類は提供されているカスタム メディア ソースから従来のアプリケーションの互換性が必要な場合をお勧めします。

### <a name="stub-driver-implementation"></a>スタブのドライバーの実装

だけでなく、INF、ドライバーのスタブも登録してカメラ デバイスのインターフェイスを有効にする必要があります。 中にこれは、通常、**ドライバー\_追加\_デバイス**操作。

参照してください、 [DRIVER_ADD_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device) WDM 用コールバック関数は、ドライバーをベースと[WdfDriverCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate) UMDF/KMDF ドライバー関数。

この操作を処理する UMDF ドライバー スタブのコードの領域切り取りを次に示します。

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

その他の物理的なカメラと同様、スタブは、ドライバーは PnP の操作を有効にして、基になるソースが削除/接続されている場合は、デバイスを無効にするので管理少なくともをお勧めします。 など、カスタム メディア ソースが IP カメラの場合) などのネットワーク ソースを使用している場合、そのネットワークのソースが使用可能ながなくなったときにデバイスの削除をトリガーします。

これにより、適切な通知のデバイスの追加/削除、PnP Api get 経由でのアプリケーションがリッスンします。 なりは使用できなくするソースを列挙することはできません。

UMDF および KMDF ドライバーでは、次を参照してください。、 [WdfDeviceSetDeviceState](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)関数のドキュメント。

WMD ドライバーでは、次を参照してください。、 [IoSetDeviceInterfaceState](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)関数のドキュメント。

## <a name="custom-media-source-dll"></a>カスタムのメディア ソース DLL

カスタムのメディア ソースは、次のインターフェイスを実装する必要があります、標準の inproc COM サーバーを示します。

-   [IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

-   [IMFMediaSource](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasource)

-   [IMFMediaSourceEx](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasourceex)

-   [IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nn-ks-ikscontrol)

-   [IMFGetService](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfgetservice)

> [!NOTE]
> **IMFMediaSourceEx**継承**IMFMediaSource**と**IMFMediaSource**継承**IMFMediaEventGenerator**します。

カスタム メディア ソース内でサポートされている各ストリームは、次のインターフェイスをサポートする必要があります。

-   **IMFMediaEventGenerator**

-   [IMFMediaStream](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediastream)

-   **IMFMediaStream2**

> [!NOTE]
> **IMFMediaStream2**継承**IMFMediaStream**と**IMFMediaStream**継承**IMFMediaEventGenerator**します。

参照してください、[カスタム メディア ソースを記述](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source)カスタム メディア ソースを作成する方法について説明します。 このセクションの残りの部分は、フレームのサーバー フレームワーク内で、カスタムのメディア ソースをサポートするために必要な相違点について説明します。

### <a name="imfgetservice"></a>IMFGetService

**IMFGetService**フレーム サーバー カスタム メディア ソースが、必須インターフェイス。 **IMFGetService**返す可能性があります**MF\_E\_UNSUPPORTED\_サービス**場合は、カスタム メディア ソースが、その他のサービス インターフェイスを公開する必要はありません。

次の例に示す、 **IMFGetService**サポート サービス インターフェイスを実装します。

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

上記のように、ソースと、ソース内の個別のストリームの両方サポートする必要が独自[IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)インターフェイス。 特定の送信によってイベント ジェネレーターを通じて管理全体 MF パイプライン データと制御フロー元の[IMFMediaEvent](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaevent)します。

IMFMediaEventGenerator を実装するには、カスタムのメディア ソースを使用する必要があります、 [MFCreateEventQueue](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreateeventqueue) API を作成する、 [IMFMediaEventQueue](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventqueue)ルーティングのすべてのメソッドと**IMFMediaEventGenerator**のキュー オブジェクト。

**IMFMediaEventGenerator**次の方法があります。

```cpp
// IMFMediaEventGenerator
IFACEMETHOD(BeginGetEvent)(_In_ IMFAsyncCallback *pCallback, _In_ IUnknown *punkState);
IFACEMETHOD(EndGetEvent)(_In_ IMFAsyncResult *pResult, _COM_Outptr_ IMFMediaEvent **ppEvent);
IFACEMETHOD(GetEvent)(DWORD dwFlags, _Out_ IMFMediaEvent **ppEvent);
IFACEMETHOD(QueueEvent)(MediaEventType met, REFGUID guidExtendedType, HRESULT hrStatus, _In_opt_ const PROPVARIANT *pvValue);
```

次のコードの推奨される実装を示しています、 **IMFMediaEventGenerator**インターフェイス。 メディア ソースのカスタム実装は、公開、 **IMFMediaEventGenerator**インターフェイス、およびそのインターフェイスのメソッドに要求をルーティングするが、 **IMFMediaEventQueue**オブジェクトメディアのソースの作成/初期化中に作成します。

次のコードで **\_spEventQueue**オブジェクトが、 **IMFMediaEventQueue**を使用して作成、 **MFCreateEventQueue**関数。

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

### <a name="seeking-and-pausing"></a>一時停止して、シーク

フレームのサーバー フレームワークを通じてサポートされているカスタムのメディア ソースがシークをサポートしてまたは一時停止操作。 カスタム メディア ソースをこれらの操作のサポートを提供する必要はありませんし、いずれかを post する必要があります、 **MFSourceSeeked**または**MEStreamSeeked**イベント。

[IMFMediaSource::Pause](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-pause)返す必要があります**MF\_E\_無効な\_状態\_遷移**(または**MF\_E\_シャット ダウン**ソースが既ににシャット ダウンされた場合)。

### <a name="ikscontrol"></a>IKsControl

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nn-ks-ikscontrol)すべての標準コントロールのインターフェイスは、カメラの関連するコントロール。 カスタム メディア ソースが、カメラ コントロールを実装している場合、 **IKsControl**インターフェイスは、パイプラインは、コントロールの I/O をルーティングする方法。

詳細については、次のコントロールの設定ドキュメント トピックを参照してください。

-   [PROPSETID_VIDCAP_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)

-   [PROPSETID_VIDCAP_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)

-   [KSPROPERTYSETID_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)

コントロールは省略可能と推奨されるエラー コードを返すにはサポートされていない場合**HRESULT\_FROM\_WIN32 (エラー\_セット\_NOT\_が見つかりました)** します。

次のコード例は、 **IKsControl**実装でサポートされているコントロールがありません。

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

説明したよう[カスタム メディア ソースを記述](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source)、 **IMFMediaStream2**を使用して、カスタムのメディア ソースのフレームの作業にインターフェイスが提供される、 [MENewStream](https://docs.microsoft.com/windows/desktop/medfound/menewstream)メディア完了中に、イベントが送信元のイベント キューにポスト、 [IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)メソッド。

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

これで選択されている各ストリームを行う必要があります、 [IMFPresentationDescriptor](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfpresentationdescriptor)します。

ビデオ ストリームをメディア ソースのカスタム[MEEndOfStream](https://docs.microsoft.com/windows/desktop/medfound/meendofstream)と[MEEndOfPresentation](https://docs.microsoft.com/windows/desktop/medfound/meendofpresentation)イベントを送信しない必要があります。

### <a name="stream-attributes"></a>Stream 属性

すべてのカスタム メディア ソース ストリームする必要がありますが、 [MF_DEVICESTREAM_STREAM_CATEGORY](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category)に設定**PINNAME\_ビデオ\_キャプチャ**します。 **PINNAME\_ビデオ\_プレビュー**カスタム メディア ソースはサポートされていません。

> [!NOTE]
> **PINNAME\_イメージ**、サポートされていますが、推奨はされません。 ストリームを公開する**PINNAME\_イメージ**フォト トリガーのすべてのコントロールをサポートするカスタム メディア ソースが必要です。 参照してください、 [Photo Stream コントロール](#photo-stream-controls)詳細については後述します。

[MF_DEVICESTREAM_STREAM_ID](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-id)はすべてのストリームの必須の属性です。 0 から始まるインデックスである必要があります。 ID は 0 を最初のストリームには、第 2 1, の ID をストリームします。

次に、ストリームで推奨される属性の一覧を示します。

-   [MF_DEVICESTREAM_ATTRIBUTE_FRAMESOURCE_TYPES](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-attribute-framesource-types)

-   [MF_DEVICESTREAM_FRAMESERVER_SHARED](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-frameserver-shared)

#### <a name="mfdevicestreamattributeframesourcetypes"></a>MF\_DEVICESTREAM\_属性\_FRAMESOURCE\_型

**MF\_DEVICESTREAM\_属性\_FRAMESOURCE\_型**は stream 型のビットマスク値である UINT32 属性です。 次のいずれかに設定する必要があります (これらの型には、ビットマスクのフラグが、これはソースの種類を可能であれば混在させないでをお勧めします)。

| 型                         | Flag   | 説明                                      |
|------------------------------|--------|--------------------------------------------------|
| MFFrameSourceTypes\_色    | 0x0001 | RGB 色の標準のストリーム                        |
| MFFrameSourceTypes\_赤外線 | 0x0002 | IR ストリーム                                        |
| MFFrameSourceTypes\_深さ    | 0x0004 | 深さのストリーム                                     |
| MFFrameSourceTypes\_イメージ    | 0x0008 | イメージ ストリーム (通常は JPEG のサブタイプ ビデオ以外) |
| MFFrameSourceTypes\_カスタム   | 0x0080 | カスタム ストリームの種類                               |

#### <a name="mfdevicestreamframeservershared"></a>MF\_DEVICESTREAM\_FRAMESERVER\_共有

**MF\_DEVICESTREAM\_FRAMESERVER\_SHARED**は UINT32 属性は 0 または 1 に設定できます。 かどうか 1 に設定すると、マークとしてフレーム サーバーで「共有」されているストリーム。 これによって、アプリケーションを別のアプリで使用する場合でも、共有モードでストリームを開きます。

フレームのサーバーで共有する最初のマークされている非ストリームを許可するこの属性が設定されていない場合 (そのストリームをマークするカスタムのメディア ソースに 1 つのみのストリームがある場合は、共有として)。

この属性が 0 に設定されている場合、フレームのサーバーは共有されたアプリからのストリームをブロックします。 場合は、カスタム メディア ソースは、この属性を 0 に設定されたすべてのストリームをマーク、共有アプリケーションはされません、ソースを初期化できません。

### <a name="sample-allocation"></a>サンプルの割り当て

としてメディアのすべてのフレームを生成する必要があります、 [IMFSample](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfsample)します。 カスタムのメディア ソースを使用する必要があります、 [MFCreateSample](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatesample) IMFSample と使用のインスタンスを割り当てるため、 [AddBuffer](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfsample-addbuffer)メディア バッファーを追加します。

各**IMFSample**サンプル時間と設定のサンプル期間があります。 すべてのサンプルのタイムスタンプは、QPC の時刻 (QueryPerformanceCounter) に基づいている必要があります。

カスタム メディア ソースが使用することをお勧めしますが、 [MFGetSystemTime](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfgetsystemtime)可能な限り機能します。 この関数は、ラッパー **QueryPerformanceCounter** QPC タイマー刻みを 100 ナノ秒単位に変換します。

カスタムのメディア ソースが内部クロックを使用して可能性がありますが、すべてのタイムスタンプは、現在 QPC に基づいて 100 ナノ秒の単位に関連付ける必要があります。

#### <a name="media-buffer"></a>メディアをバッファリングします。

追加されたすべてのメディア バッファー、 **IMFSample**標準 MF バッファー割り当て関数を使用する必要があります。 カスタムのメディア ソース必要がありますいない実装独自[IMFMediaBuffer](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediabuffer)インターフェイスまたはメディアのバッファーを直接割り当てようとして (たとえば、新しい/malloc/VirtualAlloc と、必要がありますいない使用フレーム データの)。

メディア フレームを割り当てるには、次の Api のいずれかを使用します。

-   [MFCreateMemoryBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatememorybuffer)

-   [MFCreateAlignedMemoryBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatealignedmemorybuffer)

-   [MFCreate2DMediaBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreate2dmediabuffer)

-   [MFCreateDXGISurfaceBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatedxgisurfacebuffer)

**MFCreateMemoryBuffer**と**MFCreateAlignedMemoryBuffer** stride 非固定メディア データを使用する必要があります。 通常、カスタムのサブタイプまたは (H264/HEVC/MJPG) などの圧縮のサブタイプこれらがあります。

(YUY2、NV12 など) の既知の圧縮されていないメディアの種類のシステム メモリを使用して、使用する推奨が**MFCreate2DMediaBuffer**します。

DX サーフェス (処理に使用する GPU アクセラレータによるレンダリングやエンコードなど) の**MFCreateDXGISurfaceBuffer**使用する必要があります。

**MFCreateDXGISurfaceBuffer** DX 画面を作成できません。 使用してメディア ソースに渡される DXGI マネージャーを使用して、画面を作成、 [IMFMediaSourceEx::SetD3DManager](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-setd3dmanager)メソッド。

[IMFDXGIDeviceManager::OpenDeviceHandle](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-opendevicehandle)選択 D3D デバイスに関連付けられているハンドルが提供されます。 [ID3D11Device](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11device)インターフェイスから取得できますを使用して、 [IMFDXGIDeviceManager::GetVideoService](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-getvideoservice)メソッド。

バッファーの種類を使用するに関係なく、 **IMFSample**作成する必要がありますをパイプラインに提供する、 **MEMediaSample**上のイベント、 **IMFMediaEventGenerator**のメディア ストリーム。

同じを使用することはできますが**IMFMediaEventQueue**カスタム メディア ソースとの基になるコレクションの両方の**IMFMediaStream**、することでは、シリアル化に注意してくださいメディア ソースのイベント、およびストリーム イベント (をメディアのフローを含む)。 複数のストリーム ソースの場合、これは望ましくありません。

次のコードの切り取り領域は、メディア ストリームの実装例を示しています。

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

## <a name="custom-media-source-extension-to-expose-imfactivate-available-in-windows-10-version-1809"></a>IMFActivate (Windows 10、バージョンは 1809 で使用可能) を公開するカスタムのメディア ソース拡張機能

のみあること"activated"UMDF ドライバーの 1 つのインスタンスは、フレーム サーバー アーキテクチャ内でのカスタム メディア ソース操作によって課される制限のいずれかのカスタム メディア ソースをサポートする必要があるインターフェイスの上記のリストだけでなくパイプライン。

その AV 以外の Stream ドライバー パッケージだけでなくスタブ UMDF ドライバーをインストールする物理デバイスがあるし、UMDF ドライバーの各インスタンスの中に、コンピューターにそれらの物理デバイスの 1 つ以上をアタッチする場合がシンボリック リンクの一意の名前を取得するなど、、カスタムのメディア ソースのアクティブ化パスには、作成時にカスタムのメディア ソースに関連付けられているシンボリック リンクの名前との通信手段はありません。

カスタムのメディア ソースが標準的な検索[MF_DEVSOURCE_ATTRIBUTE_SOURCE_TYPE_VIDCAP_SYMBOLIC_LINK](https://docs.microsoft.com/windows/desktop/medfound/mf-devsource-attribute-source-type-vidcap-symbolic-link)カスタム メディア ソースの属性ストア (属性ストアからカスタムのメディア ソースから返される属性[IMFMediaSourceEx::GetSourceAttributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)メソッド) 時に[IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)が呼び出されます。

ただし、この可能性起動の待機時間にこれを作成/初期化時ではなく、時間を開始するハードウェア リソースの取得で遅延があるためです。

このため、Windows 10、バージョンは 1809、カスタム メディア ソース公開される可能性が必要に応じて、 [IMFActivate](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfactivate)インターフェイス。

> [!NOTE] 
> **IMFActivate**継承[IMFAttributes](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfattributes)します。

### <a name="imfactivate"></a>IMFActivate

カスタムのメディア ソースの COM サーバー サポート**IMFActivate**インターフェイス、デバイスの初期化情報は、COM サーバーに提供されます、 **IMFAttributes** によって継承されます**IMFActivate**します。 したがって、 [IMFActivate::ActivateObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-activateobject)が呼び出されるの属性ストア、 **IMFActivate** UMDF スタブ ドライバーと、追加の構成設定のシンボリック リンク名が含まれますソースの作成と初期化の時点で、パイプライン/アプリケーションによって提供されます。

カスタムのメディア ソースは、必要なすべてのハードウェア リソースを取得する、このメソッドの呼び出しを使用してください。

> [!NOTE]
> ハードウェア resource acquisition 200 ミリ秒よりも大きい場合は、ハードウェア リソースが非同期的に取得したをお勧めします。 ハードウェア リソースの購入にカスタムのメディア ソースのアクティブ化をブロックしないでください。 代わりに[IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)操作は、ハードウェア リソースの購入に対するシリアル化する必要があります。

によって公開されている 2 つの追加方法**IMFActivate**、 [DetachObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-detachobject)と[ShutdownObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-shutdownobject)、返す必要があります**E\_NOTIMPL**.

カスタムのメディア ソースを実装することもできます、 **IMFActivate**と**IMFAttributes**内と同じ COM オブジェクトのインターフェイス、 [IMFMediaSource](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasource)します。 これは場合、お勧め、 [IMFMediaSourceEx::GetSourceAttributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)返す同じ**IMFAttributes**インターフェイスからのものとして、 **IMFActivate**します。

カスタムのメディア ソースが実装していない場合、 **IMFActivate**と**IMFAttributes**同一のオブジェクトとカスタム メディア ソースが すべての属性をコピーする必要があります、 **IMFActivate**カスタム メディア ソースのソース属性ストアに格納する属性。

## <a name="encoded-camera-stream"></a>エンコードされたカメラ Stream

カスタムのメディア ソースが圧縮されたメディアの種類 (HEVC または H264 基本ストリーム) に公開される可能性が、OS のパイプラインは、ソースとエンコード パラメーターの構成を完全にサポートすると、カスタム メディア ソース (エンコード パラメーターを通じて伝達は、[ICodecAPI](https://docs.microsoft.com/previous-versions/windows/desktop/api/strmif/nn-strmif-icodecapi)、としてルーティングされますが、 [IKsControl::KsProperty](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksproperty)呼び出す)。

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

**KSPROPERTY**に渡された構造体、 **IKsControl::KsProperty**メソッドで、次の情報が必要があります。

```cpp
KSPROPERTY.Set = Encoder Property GUID
KSPROPERTY.Id = 0
KSPROPERTY.Flags = (KSPROPERTY_TYPE_SET or KSPROPERTY_TYPE_GET)
```

エンコーダーのプロパティの GUID がで定義されている使用可能なプロパティの一覧を[コーデック API プロパティ](https://docs.microsoft.com/windows/desktop/DirectShow/codec-api-properties)します。

エンコーダーのプロパティのペイロードでを通じて渡される、 *pPropertyData*のフィールド、 **KsProperty**上で宣言されたメソッド。

### <a name="capture-engine-requirements"></a>エンジンの要件をキャプチャします。

クライアント側エンジンのキャプチャのフレームのサーバーでサポートされる完全にエンコードされたソースは中、(**IMFCaptureEngine**) によって使用される、 [Windows.Media.Capture.MediaCapture](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture)オブジェクトでは、追加要件:

-   Stream すべてエンコード (HEVC または H264) にする必要がありますか、またはすべての非圧縮 (このコンテキストで MJPG が扱われますとして圧縮されていない)。

-   少なくとも 1 つの非圧縮ストリームが使用可能なあります。

> [!NOTE]
> これらの要件はこのトピックで説明されているカスタム メディア ソース要件です。 ただし、キャプチャ Engine の要件はのみ適用されるクライアント アプリケーションを使用してカスタムのメディア ソースを使用して、 **IMFCaptureEngine**または**Windows.Media.Capture.MediaCapture** API。

## <a name="camera-profiles-available-in-windows-10-version-1803-and-later"></a>カメラのプロファイル (Windows 10、バージョン 1803 以降で使用可能)

カメラのプロファイルのサポートは、カスタム メディア ソース使用できます。 推奨されるメカニズムを使用して、プロファイルを発行する、 **MF\_DEVICEMFT\_SENSORPROFILE\_コレクション**属性を無効にソース属性 ([IMFMediaSourceEx:。GetSourceAttributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes))。

**MF\_DEVICEMFT\_SENSORPROFILE\_コレクション**属性は、 **IUnknown**の[IMFSensorProfileCollection](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfsensorprofilecollection)インターフェイス。 **IMFSensorProfileCollection**を使用して取得できます、 [MFCreateSensorProfileCollection](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatesensorprofilecollection)関数。

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

Windows こんにちは顔認識をサポートするためには、カスタム メディア ソースがデザインされている場合は顔認証プロファイルを発行する必要があます。 顔認証プロファイルの要件は次のとおりです。

-   1 つの IR ストリームでは、顔認証 DDI コントロールをサポートする必要があります。 詳細については、次を参照してください。 [KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode)します。

-   IR ストリームは、少なくとも 340 x 340 15 fps である必要があります。 L8、NV12 または MJPG L8 圧縮とマークされているか、フォーマットを使用する必要があります。

-   RGB ストリームは、少なくとも 480 x 480 7.5 の fps (これはのみ必要 Multispectrum 認証を適用する場合) である必要があります。

-   顔認証プロファイルのプロファイル ID が必要です。KSCAMERAPROFILE\_FaceAuth\_モードは 0。

顔認証プロファイルは、IR および RGB のストリームの各メディアの種類を 1 つをだけ通知をお勧めします。

## <a name="photo-stream-controls"></a>Photo Stream コントロール

ストリームのいずれかをマークすることで、独立系のフォト ストリームが公開されているかどうか[MF\_DEVICESTREAM\_ストリーム\_カテゴリ](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category)として**PINNAME\_イメージ**、ストリームのカテゴリでストリームし**PINNAME\_ビデオ\_キャプチャ**が必要です (など、1 つのストリームを公開するだけで**PINNAME\_イメージ**有効なメディア ソースがありません)。

を通じて**IKsControl**、 **PROPSETID\_しました\_VIDEOCONTROL**プロパティ セットをサポートする必要があります。 詳細については、次を参照してください。[ビデオ コントロールのプロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/video-control-properties)します。
