---
Description: KMDF ベースの USB クライアントドライバーのソースコードについて説明します。
title: USB クライアントドライバーコードの構造 (KMDF)
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: fea417702f80a7d2cc2bb04129f27cf95a6f626f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844338"
---
# <a name="understanding-the-usb-client-driver-code-structure-kmdf"></a>USB クライアント ドライバー コード構造について (KMDF)


このトピックでは、aKMDF ベースの USB クライアントドライバーのソースコードについて説明します。 このコード例は、Microsoft Visual Studio 2019 に含まれている**USB ユーザーモードドライバー**テンプレートによって生成されます。

これらのセクションでは、テンプレートコードに関する情報を提供します。

-   [ドライバーのソースコード](#driver-source-code)
-   [デバイスのソースコード](#device-source-code)
-   [キューのソースコード](#queue-source-code)
-   [関連トピック](#related-topics)

KMDF テンプレートコードを生成する手順については、「初めての[USB クライアントドライバー (kmdf) を作成する方法](tutorial--write-your-first-usb-client-driver--kmdf-.md)」を参照してください。

## <a name="driver-source-code"></a>ドライバーのソースコード


*Driver オブジェクト*は、Windows によってドライバーがメモリに読み込まれた後のクライアントドライバーのインスタンスを表します。 Driver オブジェクトの完全なソースコードは、Driver .h と Driver .c にあります。

**Driver. h**

テンプレートコードの詳細について説明する前に、KMDF ドライバーの開発に関連するヘッダーファイル (Driver .h) のいくつかの宣言を見てみましょう。

これらのファイルは、Windows Driver Kit (WDK) に含まれています。

```ManagedCPlusPlus
#include <ntddk.h>
#include <wdf.h>
#include <usb.h>
#include <usbdlib.h>
#include <wdfusb.h>

#include "device.h"
#include "queue.h"
#include "trace.h"
```

KMDF ドライバーの開発には、Ntddk と Wdf のヘッダーファイルが常に含まれています。 ヘッダーファイルには、KMDF ドライバーをコンパイルするために必要なメソッドと構造体のさまざまな宣言と定義が含まれています。

Usb デバイスのクライアントドライバーで必要とされる構造とルーチンの宣言と定義が含まれています。

Wdfusb. h には、フレームワークによって提供される USB i/o ターゲットオブジェクトとの通信に必要な構造体とメソッドの宣言と定義が含まれています。

デバイス .h、Queue .h、および .h は、WDK には含まれていません。 これらのヘッダーファイルはテンプレートによって生成され、このトピックで後ほど説明します。

Driver. h の次のブロックは、 [*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンの関数ロール型宣言、および[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)および[*evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)イベントコールバックルーチンを提供します。 これらのルーチンはすべて、ドライバーによって実装されます。 ロールの種類は、静的ドライバー検証ツール (SDV) がドライバーのソースコードを分析するのに役立ちます。 ロールの種類の詳細については、「 [KMDF ドライバーの関数ロールの種類を使用した関数の宣言](https://docs.microsoft.com/windows-hardware/drivers/devtest/declaring-functions-by-using-function-role-types-for-kmdf-drivers)」を参照してください。

```ManagedCPlusPlus
DRIVER_INITIALIZE DriverEntry;
EVT_WDF_DRIVER_DEVICE_ADD MyUSBDriver_EvtDeviceAdd;
EVT_WDF_OBJECT_CONTEXT_CLEANUP MyUSBDriver_EvtDriverContextCleanup;
```

実装ファイル Driver .c には、 [*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数とイベントコールバックルーチンがページング可能なメモリ内にあるかどうかを指定するために `alloc_text` プラグマを使用する次のコードブロックが含まれています。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (INIT, DriverEntry)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDeviceAdd)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDriverContextCleanup)
#endif
```

[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)が INIT としてマークされているのに対し、イベントコールバックルーチンはページとしてマークされていることに注意してください。 INIT セクションは、ドライバーが*driverentry*から復帰するとすぐに、 *driverentry*の実行可能コードがページングされ、破棄されることを示します。 ページセクションは、コードが常に物理メモリ内に残っている必要がないことを示します。使用されていない場合は、ページファイルに書き込むことができます。 詳細については、「ページング可能な[コードまたはデータのロック](https://docs.microsoft.com/windows-hardware/drivers/kernel/locking-pageable-code-or-data)」を参照してください。

ドライバーが読み込まれるとすぐに、ドライバーを表す[**ドライバー\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造が Windows によって割り当てられます。 次に、ドライバーのエントリポイントルーチンと[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)を呼び出し、構造体へのポインターを渡します。 Windows はルーチンを名前で検索するので、すべてのドライバーは*Driverentry*という名前のルーチンを実装する必要があります。 ルーチンは、ドライバーの初期化タスクを実行し、ドライバーのイベントコールバックルーチンをフレームワークに指定します。

次のコード例は、テンプレートによって生成される DriverEntry ルーチンを示しています。

```ManagedCPlusPlus
NTSTATUS
DriverEntry(
    _In_ PDRIVER_OBJECT  DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    //
    // Initialize WPP Tracing
    //
    WPP_INIT_TRACING( DriverObject, RegistryPath );

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = MyUSBDriver_EvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
                           MyUSBDriver_EvtDeviceAdd
                           );

    status = WdfDriverCreate(DriverObject,
                             RegistryPath,
                             &attributes,
                             &config,
                             WDF_NO_HANDLE
                             );

    if (!NT_SUCCESS(status)) {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンには、Windows によって割り当てられた[**オブジェクト構造\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)へのポインターとドライバーのレジストリパスの2つのパラメーターがあります。 *RegistryPath*パラメーターは、レジストリ内のドライバー固有のパスを表します。

[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンでは、ドライバーは次のタスクを実行します。

-   ドライバーの有効期間中に必要なグローバルリソースを割り当てます。 たとえば、テンプレートコードでは、クライアントドライバーは、 [wpp\_INIT\_tracing](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロを呼び出すことによって、wpp ソフトウェアトレースに必要なリソースを割り当てます。
-   特定のイベントコールバックルーチンをフレームワークに登録します。

    イベントコールバックを登録するために、クライアントドライバーはまず、特定の WDF 構造体での*Evtdriverxxx*ルーチンの実装へのポインターを指定します。 次に、ドライバーは[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)メソッドを呼び出し、これらの構造を提供します (次の手順で説明します)。

-   [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)メソッドを呼び出し、*フレームワークドライバーオブジェクト*へのハンドルを取得します。

    クライアントドライバーが[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出すと、フレームワークはクライアントドライバーを表すフレームワークドライバーオブジェクトを作成します。 呼び出しが完了すると、クライアントドライバーは WDFDRIVER ハンドルを受け取り、そのレジストリパスやバージョン情報などのドライバーに関する情報を取得できます (「 [WDF Driver Object Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/)」を参照してください)。

    Framework driver オブジェクトは、 [**driver\_object**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)によって記述された Windows driver オブジェクトとは異なることに注意してください。 クライアントドライバーは、WDFDRIVER ハンドルを使用し、 [**WdfGetDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfgetdriver)メソッドを呼び出すことによって、いつでも Windows**driver\_オブジェクト**構造へのポインターを取得できます。

[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)呼び出しの後、フレームワークは Windows と通信するクライアントドライバーとパートナーをします。 フレームワークは、Windows とドライバーの間の抽象化レイヤーとして機能し、複雑なドライバータスクのほとんどを処理します。 クライアントドライバーは、ドライバーが興味を持っているイベントのフレームワークに登録します。 特定のイベントが発生すると、Windows によってフレームワークに通知されます。 ドライバーが特定のイベントのイベントコールバックを登録した場合、フレームワークは、登録済みのイベントコールバックを呼び出してドライバーに通知します。 これにより、必要に応じて、ドライバーにイベントを処理する機会が与えられます。 ドライバーがイベントコールバックを登録しなかった場合、フレームワークはイベントの既定の処理を続行します。

ドライバーが登録する必要があるイベントコールバックの1つは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)です。 フレームワークは、デバイスオブジェクトを作成する準備が整ったときに、ドライバーの*Evtdriverdeviceadd*実装を呼び出します。 Windows では、デバイスオブジェクトは、クライアントドライバーが読み込まれる物理デバイスの機能を論理的に表現したものです (このトピックで後述します)。

ドライバーが登録できるその他のイベントコールバックは、 [*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)、 [*evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)、および[*evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)です。

テンプレートコードでは、クライアントドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)と[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)の2つのイベントを登録します。 ドライバーは、 [**WDF\_driver\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体の*Evtdriverdeviceadd*の実装へのポインターと、 [**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造の*evtcleanupcallback*イベントコールバックを指定します。

Windows がドライバー [ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造を解放し、ドライバーをアンロードする準備が整ったら、フレームワークは、ドライバーの[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)実装を呼び出すことによって、そのイベントをクライアントドライバーに報告します。 フレームワークは、フレームワークドライバーオブジェクトを削除する直前に、そのコールバックを呼び出します。 クライアントドライバーは、その[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)で割り当てられたすべてのグローバルリソースを解放できます。 たとえば、テンプレートコードでは、クライアントドライバーは*Driverentry*でアクティブ化された WPP トレースを停止します。

次のコード例は、クライアントドライバーの EvtCleanupCallback イベントコールバックの実装を示しています。

```ManagedCPlusPlus
VOID
MyUSBDriver_EvtDriverContextCleanup(
    _In_ WDFDRIVER Driver
    )
{
    UNREFERENCED_PARAMETER(Driver);

    PAGED_CODE ();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Stop WPP Tracing
    //
    WPP_CLEANUP( WdfDriverWdmGetDriverObject(Driver) );

}
```

デバイスが USB ドライバースタックによって認識されると、バスドライバーによってデバイスの物理デバイスオブジェクト (PDO) が作成され、PDO がデバイスノードに関連付けられます。 デバイスノードは、PDO が一番下にあるスタックフォーメーションにあります。 各スタックには1つの PDO が必要であり、フィルターデバイスオブジェクト (DOs をフィルター処理する) と、その上に関数デバイスオブジェクト (FDO) を含めることができます。 詳細については、「[デバイスノードとデバイススタック](https://docs.microsoft.com/windows-hardware/drivers/debugger/device-node-and-stack-debugger-commands)」を参照してください。

次の図は、テンプレートドライバーのデバイススタック、MyUSBDriver\_を示しています。

![テンプレートドライバーのデバイススタック](images/usb-device-stack.png)

"My USB Device" という名前のデバイススタックに注意してください。 USB ドライバースタックによって、デバイススタック用の PDO が作成されます。 この例では、PDO は、USB ドライバースタックに含まれているドライバーの1つである Usbhub3 に関連付けられています。 クライアントドライバーは、デバイスの関数ドライバーとして、まずデバイスの FDO を作成してから、デバイススタックの一番上に接続する必要があります。

KMDF ベースのクライアントドライバーの場合、フレームワークはクライアントドライバーに代わってこれらのタスクを実行します。 フレームワークは、デバイスの FDO を表すために、*フレームワークデバイスオブジェクト*を作成します。 ただし、クライアントドライバーは、フレームワークが新しいオブジェクトを構成するために使用する特定の初期化パラメーターを指定できます。 フレームワークがドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)実装を呼び出すと、クライアントドライバーにその機会が与えられます。 オブジェクトが作成され、FDO がデバイススタックの一番上にアタッチされると、フレームワークは、クライアントドライバーに、フレームワークデバイスオブジェクトへの WDFDEVICE ハンドルを提供します。 このハンドルを使用すると、クライアントドライバーはデバイス関連のさまざまな操作を実行できます。

次のコード例は、クライアントドライバーの EvtDriverDeviceAdd イベントコールバックの実装を示しています。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_EvtDeviceAdd(
    _In_    WDFDRIVER       Driver,
    _Inout_ PWDFDEVICE_INIT DeviceInit
    )
{
    NTSTATUS status;

    UNREFERENCED_PARAMETER(Driver);

    PAGED_CODE();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    status = MyUSBDriver_CreateDevice(DeviceInit);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

実行時に、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)の実装は、ページングされた[ **\_コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロを使用して、ルーチンが、ページング可能なコードに適した環境で呼び出されていることを確認します。 すべての変数を宣言した後、マクロを必ず呼び出してください。そうしないと、生成されたソースファイルは .cpp ファイルではなく .c ファイルであるため、コンパイルは失敗します。

クライアントドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)実装は、必要なタスクを実行するために、myusbdriver\_CreateDevice helper 関数を呼び出します。

次のコード例は、MyUSBDriver\_CreateDevice helper 関数を示しています。 MyUSBDriver\_CreateDevice は、Device .c で定義されています。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_CreateDevice(
    _Inout_ PWDFDEVICE_INIT DeviceInit
    )
{
    WDF_PNPPOWER_EVENT_CALLBACKS pnpPowerCallbacks;
    WDF_OBJECT_ATTRIBUTES   deviceAttributes;
    PDEVICE_CONTEXT deviceContext;
    WDFDEVICE device;
    NTSTATUS status;

    PAGED_CODE();

    WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&pnpPowerCallbacks);
    pnpPowerCallbacks.EvtDevicePrepareHardware = MyUSBDriver_EvtDevicePrepareHardware;
    WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, &pnpPowerCallbacks);

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DEVICE_CONTEXT);

    status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);

    if (NT_SUCCESS(status)) {
        //
        // Get the device context and initialize it. WdfObjectGet_DEVICE_CONTEXT is an
        // inline function generated by WDF_DECLARE_CONTEXT_TYPE macro in the
        // device.h header file. This function will do the type checking and return
        // the device context. If you pass a wrong object  handle
        // it will return NULL and assert if run under framework verifier mode.
        //
        deviceContext = WdfObjectGet_DEVICE_CONTEXT(device);
        deviceContext->PrivateDeviceData = 0;

        //
        // Create a device interface so that applications can find and talk
        // to us.
        //
        status = WdfDeviceCreateDeviceInterface(
            device,
            &GUID_DEVINTERFACE_MyUSBDriver_,
            NULL // ReferenceString
            );

        if (NT_SUCCESS(status)) {
            //
            // Initialize the I/O Package and any Queues
            //
            status = MyUSBDriver_QueueInitialize(device);
        }
    }

    return status;
}
```

[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)には、次の2つのパラメーターがあります。 [*driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)の前の呼び出しで作成されたフレームワークドライバーオブジェクトへのハンドルと、 [**wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体へのポインター。 フレームワークは、 **Wdfdevice\_INIT**構造体を割り当て、ポインターを渡します。これにより、クライアントドライバーは、作成するフレームワークデバイスオブジェクトの初期化パラメーターを使用して構造体にデータを設定できます。

[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)実装では、クライアントドライバーは次のタスクを実行する必要があります。

-   [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)メソッドを呼び出して、新しいデバイスオブジェクトへの WDFDEVICE ハンドルを取得します。

    [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)メソッドを使用すると、フレームワークは FDO のフレームワークデバイスオブジェクトを作成し、デバイススタックの一番上にアタッチします。 **WdfDeviceCreate**の呼び出しでは、クライアントドライバーは次のタスクを実行する必要があります。

    -   フレームワークによって指定された[Wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体で、クライアントドライバーのプラグアンドプレイ (PnP) 電源コールバックルーチンへのポインターを指定します。 ルーチンはまず、 [**WDF\_PNPPOWER\_イベント\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_pnppower_event_callbacks)構造体で設定され、次に[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)メソッドを呼び出して WDFDEVICE\_INIT に関連付けられます。

        Windows コンポーネント、PnP および電源マネージャーは、PnP 状態の変更 (開始、停止、削除など) と電源状態 (作業中や中断など) に応じて、デバイスに関連する要求をドライバーに送信します。 KMDF ベースのドライバーの場合、フレームワークはこれらの要求をインターセプトします。 クライアントドライバーは、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)呼び出しを使用して、 *PnP 電源イベントコールバック*と呼ばれるコールバックルーチンをフレームワークに登録することによって、要求に関する通知を受け取ることができます。 Windows コンポーネントが要求を送信すると、フレームワークはそれらを処理し、対応する PnP 電源イベントコールバックを呼び出します (クライアントドライバーが登録されている場合)。

        クライアントドライバーが実装する必要がある PnP 電源イベントコールバックルーチンの1つは、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)です。 このイベントコールバックは、PnP マネージャーがデバイスを起動したときに呼び出されます。 *Evtdevicepreparehardware*の実装については、次のセクションで説明します。

    -   ドライバーのデバイスコンテキスト構造へのポインターを指定します。 ポインターは、 [**WDF\_オブジェクト\_属性\_INIT\_CONTEXT\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/ff552400_init_context_type)マクロを呼び出すことによって初期化される、 [**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体で設定する必要があります。

        デバイスコンテキスト (デバイス拡張と呼ばれることもあります) は、特定のデバイスオブジェクトに関する情報を格納するためのデータ構造 (クライアントドライバーによって定義されます) です。 クライアントドライバーは、デバイスコンテキストへのポインターをフレームワークに渡します。 フレームワークは、構造体のサイズに基づいてメモリのブロックを割り当て、そのメモリ位置へのポインターをフレームワークデバイスオブジェクトに格納します。 クライアントドライバーは、ポインターを使用して、デバイスコンテキストのメンバーにアクセスし、情報を格納できます。 デバイスコンテキストの詳細については、「[フレームワークオブジェクトコンテキスト空間](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-context-space)」を参照してください。

        [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)の呼び出しが完了すると、クライアントドライバーは、新しいフレームワークデバイスオブジェクトへのハンドルを受け取ります。このオブジェクトは、デバイスコンテキストのフレームワークによって割り当てられたメモリブロックへのポインターを格納します。 クライアントドライバーは、 **Wdfobjectget\_device\_context**マクロを呼び出すことによって、デバイスコンテキストへのポインターを取得できるようになりました。

-   [**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)メソッドを呼び出して、クライアントドライバーのデバイスインターフェイス GUID を登録します。 アプリケーションは、この GUID を使用してドライバーと通信できます。 GUID 定数は、ヘッダーで宣言されています。
-   デバイスへの i/o 転送のキューを設定します。 このテンプレートコードでは、キューを設定するためのヘルパールーチンである、MyUSBDriver\_QueueInitialize が定義されています。これについては、「[キューのソースコード](#queue-source-code)」セクションで説明します。

## <a name="device-source-code"></a>デバイスのソースコード


*デバイスオブジェクト*は、クライアントドライバーがメモリに読み込まれるデバイスのインスタンスを表します。 デバイスオブジェクトの完全なソースコードは、デバイス .h と Device .c にあります。

**デバイス .h**

この .h ヘッダーファイルには、プロジェクト内のすべてのファイルで使用される共通の宣言が含まれています。

デバイス .h の次のブロックは、クライアントドライバーのデバイスコンテキストを宣言します。

```ManagedCPlusPlus
typedef struct _DEVICE_CONTEXT
{
    WDFUSBDEVICE UsbDevice;
    ULONG PrivateDeviceData;  // just a placeholder

} DEVICE_CONTEXT, *PDEVICE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(DEVICE_CONTEXT)
```

**デバイス\_のコンテキスト**構造は、クライアントドライバーによって定義され、フレームワークデバイスオブジェクトに関する情報を格納します。 これは、デバイス .h で宣言され、2つのメンバーが含まれています。これは、後で説明するように、フレームワークの USB ターゲットデバイスオブジェクトへのハンドルとプレースホルダーです。 この構造は、後の演習で展開されます。

また、 **WDF\_DECLARE\_CONTEXT\_TYPE**マクロも含まれています。これにより、インライン関数、 **Wdfobjectget\_デバイス\_コンテキスト**が生成されます。 クライアントドライバーは、その関数を呼び出して、フレームワークデバイスオブジェクトからメモリブロックへのポインターを取得できます。

次のコード行では、MyUSBDriver\_CreateDevice が宣言されています。これは、USB ターゲットデバイスオブジェクトへの WDFUSBDEVICE ハンドルを取得するヘルパー関数です。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_CreateDevice(
    _Inout_ PWDFDEVICE_INIT DeviceInit
    );
```

USBCreate は、パラメーターとして[Wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体へのポインターを取得します。 これは、クライアントドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)実装を呼び出したときにフレームワークによって渡されたポインターと同じです。 基本的に、MyUSBDriver\_CreateDevice は、 *Evtdriverdeviceadd*のタスクを実行します。 *Evtdriverdeviceadd*実装のソースコードについては、前のセクションで説明しました。

デバイス .h の次の行では、 [*Evtdeviceのハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベントコールバックルーチンの関数ロール型宣言を宣言しています。 イベントコールバックは、クライアントドライバーによって実装され、USB デバイスの構成などのタスクを実行します。

```ManagedCPlusPlus
EVT_WDF_DEVICE_PREPARE_HARDWARE MyUSBDriver_EvtDevicePrepareHardware;
```

**Device. c**

Device. c 実装ファイルには、`alloc_text` プラグマを使用する次のコードブロックが含まれています。これは、ドライバーの[*Evtdeviceのハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)実装がページング可能なメモリ内にあることを指定するために使用します。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_CreateDevice)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDevicePrepareHardware)
#endif
```

[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)の実装では、クライアントドライバーは USB 固有の初期化タスクを実行します。 これらのタスクには、クライアントドライバーの登録、USB 固有の i/o ターゲットオブジェクトの初期化、および USB 構成の選択が含まれます。 次の表は、フレームワークによって提供される特殊な i/o ターゲットオブジェクトを示しています。 詳細については、「 [USB I/o ターゲット](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets)」を参照してください。

| USB i/o ターゲットオブジェクト (ハンドル)                   | を呼び出してハンドルを取得します。                                                          | 説明                                                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *USB ターゲットデバイスオブジェクト*(WDFUSBDEVICE)       | [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) | USB デバイスを表し、デバイス記述子を取得し、デバイスに制御要求を送信するためのメソッドを提供します。                                                                                                                                                                                                                 |
| *USB ターゲットインターフェイスオブジェクト*(WDFUSBINTERFACE) | [**WdfUsbTargetDeviceGetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)             | 個々のインターフェイスを表し、クライアントドライバーが別の設定を選択して設定に関する情報を取得するために呼び出すことができるメソッドを提供します。                                                                                                                                                                              |
| *USB ターゲットパイプオブジェクト*(WDFUSBPIPE)            | [**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)         | インターフェイスの現在の代替設定で構成されているエンドポイントの個々のパイプを表します。 USB ドライバースタックは、選択された構成内の各インターフェイスを選択し、インターフェイス内の各エンドポイントへの通信チャネルを設定します。 USB 用語では、その通信チャネルは*パイプ*と呼ばれます。 |

 

このコード例は、EvtDevicePrepareHardware の実装を示しています。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_EvtDevicePrepareHardware(
    _In_ WDFDEVICE Device,
    _In_ WDFCMRESLIST ResourceList,
    _In_ WDFCMRESLIST ResourceListTranslated
    )
{
    NTSTATUS status;
    PDEVICE_CONTEXT pDeviceContext;
    WDF_USB_DEVICE_CREATE_CONFIG createParams;
    WDF_USB_DEVICE_SELECT_CONFIG_PARAMS configParams;

    UNREFERENCED_PARAMETER(ResourceList);
    UNREFERENCED_PARAMETER(ResourceListTranslated);

    PAGED_CODE();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    status = STATUS_SUCCESS;
    pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);

    if (pDeviceContext->UsbDevice == NULL) {

        //
        // Specifying a client contract version of 602 enables us to query for
        // and use the new capabilities of the USB driver stack for Windows 8.
        // It also implies that we conform to rules mentioned in the documentation
        // documentation for WdfUsbTargetDeviceCreateWithParameters.
        //
        WDF_USB_DEVICE_CREATE_CONFIG_INIT(&createParams,
                                         USBD_CLIENT_CONTRACT_VERSION_602
                                         );

        status = WdfUsbTargetDeviceCreateWithParameters(Device,
                                                    &createParams,
                                                    WDF_NO_OBJECT_ATTRIBUTES,
                                                    &pDeviceContext->UsbDevice
                                                    );

        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE,
                        "WdfUsbTargetDeviceCreateWithParameters failed 0x%x", status);
            return status;
        }

        //
        // Select the first configuration of the device, using the first alternate
        // setting of each interface
        //
        WDF_USB_DEVICE_SELECT_CONFIG_PARAMS_INIT_MULTIPLE_INTERFACES(&configParams,
                                                                     0,
                                                                     NULL
                                                                     );
        status = WdfUsbTargetDeviceSelectConfig(pDeviceContext->UsbDevice,
                                                WDF_NO_OBJECT_ATTRIBUTES,
                                                &configParams
                                                );

        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE,
                        "WdfUsbTargetDeviceSelectConfig failed 0x%x", status);
            return status;
        }
    }

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

次に、テンプレートコードによって実装されるクライアントドライバーのタスクについて詳しく見ていきます。

1.  Windows によって読み込まれる、基になる USB ドライバースタックに自身を登録する準備として、クライアントドライバーのコントラクトバージョンを指定します。

    Usb デバイスが接続されているホストコントローラーに応じて、Windows は USB 3.0 または USB 2.0 ドライバースタックを読み込むことができます。 USB 3.0 ドライバースタックは Windows 8 の新機能であり、ストリーム機能など、USB 3.0 仕様で定義されているいくつかの新機能をサポートしています。 新しいドライバースタックには、USB 要求ブロック (URBs) の追跡と処理の向上など、いくつかの機能強化も実装されています。これは、新しい URB ルーチンのセットを通じて利用できます。 これらの機能を使用したり新しいルーチンを呼び出したりするクライアントドライバーは、USBD\_CLIENT\_CONTRACT\_VERSION\_602 コントラクトバージョンを指定する必要があります。 USBD\_クライアント\_コントラクト\_バージョン\_602 クライアントドライバーは、特定のルールセットに準拠している必要があります。 これらのルールの詳細については、「[ベストプラクティス: URBs の使用](usb-client-driver-contract-in-windows-8.md)」を参照してください。

    コントラクトのバージョンを指定するには、クライアントドライバーは[**WDF\_usb\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_create_config)を初期化する必要があります。この場合、 [**WDF\_usb\_デバイス\_作成 @no__ を呼び出して、コントラクトのバージョンで\_CONFIG 構造を作成\_ますt_11_ CONFIG\_INIT**](https://msdn.microsoft.com/library/windows/hardware/hh406503_init)マクロ。\_

2.  [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドを呼び出します。 メソッドでは、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)の実装で[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すことによって、クライアントドライバーが以前に取得したフレームワークデバイスオブジェクトをハンドルする必要があります。 **WdfUsbTargetDeviceCreateWithParameters**メソッド:
    -   クライアントドライバーを基になる USB ドライバースタックに登録します。
    -   フレームワークによって作成される USB ターゲットデバイスオブジェクトへの WDFUSBDEVICE ハンドルを取得します。 テンプレートコードは、デバイスコンテキストで USB ターゲットデバイスオブジェクトへのハンドルを格納します。 クライアントドライバーは、そのハンドルを使用することによって、デバイスに関する USB 固有の情報を取得できます。

    WdfUsbTargetDeviceCreate ではなく、 [**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/ff550077withconfig)の代わりに[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate)を呼び出す必要がある  **ことに注意**してください。
    -   クライアントドライバーは、WDK の Windows 8 バージョンで使用可能な新しい URB ルーチンのセットを呼び出しません。

        クライアントドライバーが[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出す場合、USB ドライバースタックは、 [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)または[**WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)を呼び出すことによってすべての URBs が割り当てられていると想定します。 これらのメソッドによって割り当てられる URBs には、より高速な処理のために USB ドライバースタックによって使用される不透明な URB コンテキストブロックがあります。 クライアントドライバーが、これらの方法で割り当てられていない URB を使用する場合、USB ドライバーはバグチェックを生成します。

        URB 割り当ての詳細については、「 [URBs の割り当てとビルド](how-to-add-xrb-support-for-client-drivers.md)」を参照してください。

    -   クライアントドライバーは、「[ベストプラクティス: URBs の使用](usb-client-driver-contract-in-windows-8.md)」で説明されている規則のセットに従わないことを意図していません。

    このようなドライバーは、クライアントコントラクトのバージョンを指定する必要がないため、手順 1. を省略する必要があります。

     

3.  USB 構成を選択します。

    テンプレートコードでは、クライアントドライバーは、USB デバイスの*既定の構成*を選択します。 既定の構成では、デバイスの構成0と、その構成内の各インターフェイスの代替設定0が含まれます。

    既定の構成を選択するために、クライアントドライバーは、WDF\_USB\_デバイスを呼び出すことによって[**WDF\_usb\_デバイスを構成\_\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_select_config_params)\_params 構造を選択します。\_[**構成\_params\_INIT\_MULTIPLE\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff552600_init_multiple_interfaces)関数を呼び出します。\_ 関数は、**型**のメンバーを**WdfUsbTargetDeviceSelectConfigTypeMultiInterface**に初期化して、複数のインターフェイスが使用可能である場合は、それらの各インターフェイスの代替設定を選択する必要があることを示します。 呼び出しでは既定の構成を選択する必要があるため、クライアントドライバーは*Settingpairs*パラメーターに NULL を指定し、 *number インターフェイス*パラメーターに0を指定します。 完了すると、 **WDF\_USB\_\_デバイス**の**Multiinterface. NumberOfConfiguredInterfaces**メンバーが\_CONFIG\_PARAMS を選択すると、代替設定0があるインターフェイスの数が示されます。オフ. 他のメンバーは変更されません。

    **注**  クライアントドライバーで既定の設定以外の代替設定を選択する必要がある場合は、ドライバーは、\_のペアの構造を[**設定\_、WDF\_USB\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_interface_setting_pair)の配列を作成する必要があります。 配列の各要素は、デバイス定義のインターフェイス番号と、選択する代替設定のインデックスを指定します。 その情報は、 [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)メソッドを呼び出すことによって取得できるデバイスの構成とインターフェイス記述子に格納されます。 次に、クライアントドライバーは、 [**WDF\_usb\_デバイスを呼び出す必要があり\_\_構成\_PARAMS\_INIT\_複数の\_インターフェイスを選択**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_device_select_config_params_init_multiple_interfaces)し、 **WDF\_USB\_インターフェイスを渡す必要があり\_** 配列をフレームワークにペア\_設定しています。

     

## <a name="queue-source-code"></a>キューのソースコード


*Framework queue オブジェクト*は、特定のフレームワークデバイスオブジェクトの i/o キューを表します。 Queue オブジェクトの完全なソースコードは、Queue. h および Queue. c にあります。

**Queue .h**

フレームワークの queue オブジェクトによって発生するイベントのイベントコールバックルーチンを宣言します。

Queue 内の最初のブロックは、キューコンテキストを宣言します。

```ManagedCPlusPlus
typedef struct _QUEUE_CONTEXT {

    ULONG PrivateDeviceData;  // just a placeholder

} QUEUE_CONTEXT, *PQUEUE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(QUEUE_CONTEXT, QueueGetContext)
```

デバイスコンテキストと同様に、キューコンテキストは、特定のキューに関する情報を格納するためにクライアントによって定義されるデータ構造です。

次のコード行では、フレームワークキューオブジェクトを作成および初期化するヘルパー関数である、MyUSBDriver\_QueueInitialize 関数が宣言されています。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_QueueInitialize(
    _In_ WDFDEVICE Device
    );
```

次のコード例では、 [*Evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)イベントコールバックルーチンの関数ロール型宣言を宣言しています。 イベントコールバックはクライアントドライバーによって実装され、フレームワークがデバイス i/o 制御要求を処理するときに呼び出されます。

```ManagedCPlusPlus
EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL MyUSBDriver_EvtIoDeviceControl;
```

**Queue .c**

実装ファイル (Queue. c) には、`alloc_text` プラグマを使用して、ドライバーの MyUSBDriver\_QueueInitialize がページング可能なメモリ内にあることを指定する次のコードブロックが含まれています。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_QueueInitialize)
#endif
```

WDF は、クライアントドライバーへの要求フローを処理するフレームワークキューオブジェクトを提供します。 フレームワークは、クライアントドライバーが[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)メソッドを呼び出すと、フレームワークキューオブジェクトを作成します。 この呼び出しでは、フレームワークがキューを作成する前に、クライアントドライバーで特定の構成オプションを指定できます。 これらのオプションには、キューが電源管理されているか、長さがゼロの要求を許可するか、またはドライバーの既定のキューであるかが含まれます。 単一のフレームワークキューオブジェクトは、読み取り、書き込み、デバイス i/o 制御など、いくつかの種類の要求を処理できます。 クライアントドライバーは、これらの要求ごとにイベントコールバックを指定できます。

クライアントドライバーは、ディスパッチの種類も指定する必要があります。 キューオブジェクトのディスパッチ型によって、フレームワークがクライアントドライバーに要求を配信する方法が決まります。 配信メカニズムは、順次、並列、またはクライアントドライバーによって定義されたカスタムメカニズムによって実現できます。 順次キューの場合、クライアントドライバーが前の要求を完了するまで、要求は配信されません。 並列ディスパッチモードでは、フレームワークは、i/o マネージャーから到着するとすぐに要求を転送します。 これは、クライアントドライバーが別の要求を処理するときに、1つの要求を受信できることを意味します。 カスタム機構では、クライアントは、ドライバーが処理する準備ができたときに、フレームワークのキューオブジェクトから次の要求を手動でプルします。

通常、クライアントドライバーは、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベントコールバックでキューを設定する必要があります。 このテンプレートコードは、フレームワークキューオブジェクトを初期化するヘルパールーチン MyUSBDriver\_QueueInitialize を提供します。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_QueueInitialize(
    _In_ WDFDEVICE Device
    )
{
    WDFQUEUE queue;
    NTSTATUS status;
    WDF_IO_QUEUE_CONFIG    queueConfig;

    PAGED_CODE();
    
    //
    // Configure a default queue so that requests that are not
    // configure-fowarded using WdfDeviceConfigureRequestDispatching to goto
    // other queues get dispatched here.
    //
    WDF_IO_QUEUE_CONFIG_INIT_DEFAULT_QUEUE(
         &queueConfig,
        WdfIoQueueDispatchParallel
        );

    queueConfig.EvtIoDeviceControl = MyUSBDriver_EvtIoDeviceControl;

    status = WdfIoQueueCreate(
                 Device,
                 &queueConfig,
                 WDF_NO_OBJECT_ATTRIBUTES,
                 &queue
                 );

    if( !NT_SUCCESS(status) ) {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_QUEUE, "WdfIoQueueCreate failed %!STATUS!", status);
        return status;
    }

    return status;
}
```

キューを設定するために、クライアントドライバーは次のタスクを実行します。

1.  [**WDF\_IO\_queue\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構成構造のキューの構成オプションを指定します。 このテンプレートコードでは、 [**WDF\_IO\_queue\_CONFIG\_INIT\_DEFAULT\_queue**](https://msdn.microsoft.com/library/windows/hardware/ff552359_init_default_queue)関数を使用して構造体を初期化します。 関数は、キューオブジェクトを既定のキューオブジェクトとして指定し、電源管理を行い、要求を並列で受信します。
2.  キューの i/o 要求に対するクライアントドライバーのイベントコールバックを追加します。 テンプレートでは、クライアントドライバーは、デバイス i/o 制御要求のイベントコールバックへのポインターを指定します。
3.  [**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して、フレームワークによって作成されたフレームワークキューオブジェクトへの WDFQUEUE ハンドルを取得します。

キューメカニズムのしくみを次に示します。 アプリケーションは、USB デバイスと通信するために、 **Setdixxx**ルーチンと[**createhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)を呼び出すことによって、まずデバイスへのハンドルを開きます。 このハンドルを使用すると、アプリケーションは特定の制御コードを使用して[**DeviceIoControl**](https://docs.microsoft.com/previous-versions/windows/desktop/api/deviceaccess/nn-deviceaccess-ideviceiocontrol)関数を呼び出します。 コントロールコードの種類に応じて、アプリケーションはその呼び出しで入力バッファーと出力バッファーを指定できます。 この呼び出しは、最終的に i/o マネージャーによって受信されます。これにより、要求 (IRP) が作成され、クライアントドライバーに転送されます。 フレームワークは、要求をインターセプトし、フレームワーク要求オブジェクトを作成して、フレームワークキューオブジェクトに追加します。 この場合、クライアントドライバーはデバイス i/o 制御要求に対してイベントコールバックを登録したため、フレームワークはコールバックを呼び出します。 また、キューオブジェクトは WdfIoQueueDispatchParallel フラグを使用して作成されているため、要求がキューに追加されるとすぐにコールバックが呼び出されます。

```ManagedCPlusPlus
VOID
MyUSBDriver_EvtIoDeviceControl(
    _In_ WDFQUEUE Queue,
    _In_ WDFREQUEST Request,
    _In_ size_t OutputBufferLength,
    _In_ size_t InputBufferLength,
    _In_ ULONG IoControlCode
    )
{
    TraceEvents(TRACE_LEVEL_INFORMATION, 
                TRACE_QUEUE, 
                "!FUNC! Queue 0x%p, Request 0x%p OutputBufferLength %d InputBufferLength %d IoControlCode %d", 
                Queue, Request, (int) OutputBufferLength, (int) InputBufferLength, IoControlCode);

    WdfRequestComplete(Request, STATUS_SUCCESS);

    return;
}
```

フレームワークは、クライアントドライバーのイベントコールバックを呼び出すときに、アプリケーションによって送信された要求 (およびその入力バッファーと出力バッファー) を保持するフレームワークの要求オブジェクトにハンドルを渡します。 さらに、要求を含むフレームワークキューオブジェクトへのハンドルを送信します。 イベントコールバックでは、クライアントドライバーは必要に応じて要求を処理します。 テンプレートコードは単に要求を完了します。 クライアントドライバーは、さらに複雑なタスクを実行できます。 たとえば、アプリケーションが特定のデバイス情報を要求した場合、イベントコールバックでは、クライアントドライバーは USB コントロール要求を作成し、USB ドライバースタックに送信して、要求されたデバイス情報を取得できます。 Usb 制御の要求については、「 [Usb 制御転送](usb-control-transfer.md)」で説明します。

## <a name="related-topics"></a>関連トピック
[USB クライアント ドライバー開発の概要](getting-started-with-usb-client-driver-development.md)  
[WinUSB](winusb.md)  
[最初の USB クライアントドライバー (UMDF) を作成する](implement-driver-entry-for-a-usb-driver--umdf-.md)  
[最初の USB クライアントドライバー (KMDF) を作成する](tutorial--write-your-first-usb-client-driver--kmdf-.md)  



