---
Description: KMDF ベースの USB クライアント ドライバーのソース コードについて説明します。
title: USB クライアント ドライバー コードの構造 (KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 739708ddef79aca1fba280b640b61615cb5da598
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355153"
---
# <a name="understanding-the-usb-client-driver-code-structure-kmdf"></a>USB クライアント ドライバー コード構造について (KMDF)


このトピックでは、USB クライアント ドライバーの aKMDF ベースのソース コードについて学習します。 コード例は、によって生成される、 **USB ユーザー モード ドライバー**Microsoft Visual Studio 2012 に含まれているテンプレートです。

これらのセクションでは、テンプレート コードに関する情報を提供します。

-   [ドライバーのソース コード](#driver)
-   [デバイスのソース コード](#device)
-   [キュー ソース コード](#queue)
-   [関連トピック](#related-topics)

KMDF のテンプレート コードを生成する方法の詳細については、次を参照してください。 [、最初の USB クライアント ドライバー (KMDF) を書き込む方法](tutorial--write-your-first-usb-client-driver--kmdf-.md)します。

## <a name="driver-source-code"></a>ドライバーのソース コード


*ドライバー オブジェクト*Windows には、メモリ内のドライバーが読み込まれた後に、クライアント ドライバーのインスタンスを表します。 ドライバー オブジェクトの完全なソース コードは、Driver.h と Driver.c です。

**Driver.h**

テンプレート コードの詳細を説明する前に、KMDF ドライバーの開発に関連するヘッダー ファイル (Driver.h) 内のいくつかの宣言を見てみましょう。

Driver.h には、Windows Driver Kit (WDK) で含まれている、これらのファイルが含まれています。

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

Ntddk.h と Wdf.h ヘッダー ファイルは、KMDF ドライバーの開発のために含まれては常にします。 ヘッダー ファイルには、さまざまな宣言とメソッドと KMDF ドライバーをコンパイルする必要のある構造体の定義が含まれています。

Usb.h と Usbdlib.h には、構造体と USB デバイスのクライアント ドライバーで必要なルーチンの宣言および定義が含まれます。

Wdfusb.h には、構造体と、フレームワークによって提供される USB I/O ターゲット オブジェクトと通信するために必要なメソッドの宣言および定義が含まれています。

Device.h、Queue.h、および Trace.h は WDK に含まれていません。 これらのヘッダー ファイルでは、テンプレートによって生成され、このトピックの後半で説明されています。

ロールの種類の宣言機能を提供する Driver.h の次のブロック、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン、および[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)イベント コールバック ルーチン。 すべてのこれらのルーチンは、ドライバーによって実装されます。 ロールの種類では、Static Driver Verifier (SDV) ドライバーのソース コードを分析するのに役立ちます。 ロールの種類の詳細については、次を参照してください。[を使用して関数の役割の種類 KMDF ドライバーで関数を宣言する](https://msdn.microsoft.com/library/windows/hardware/ff544643)します。

```ManagedCPlusPlus
DRIVER_INITIALIZE DriverEntry;
EVT_WDF_DRIVER_DEVICE_ADD MyUSBDriver_EvtDeviceAdd;
EVT_WDF_OBJECT_CONTEXT_CLEANUP MyUSBDriver_EvtDriverContextCleanup;
```

Driver.c、実装ファイルには、次を使用するコードのブロックが含まれています`alloc_text`プラグマを指定するかどうか、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数とイベントのコールバック ルーチンはページング可能。メモリ。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (INIT, DriverEntry)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDeviceAdd)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDriverContextCleanup)
#endif
```

注意[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)イベント コールバック ルーチンがページとしてマークされている一方、INIT、としてマークされます。 INIT セクションでは、ことを示しますの実行可能コード*DriverEntry*ページングし、破棄からドライバーを返し、すぐにその*DriverEntry*します。 ページ セクションでは、すべての時間です。 物理メモリ内に、コードがないことを示します使用中でないときに、ページング ファイルに記述できます。 詳細については、次を参照してください。[ロック ページング可能なコードまたはデータ](https://msdn.microsoft.com/library/windows/hardware/ff554307)します。

Windows を割り当てるには、ドライバーが読み込まれると、すぐに、 [**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)ドライバーを表す構造体です。 ドライバーのエントリ ポイントのルーチンを呼び出して[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)、構造体へのポインターを渡します。 すべてのドライバーがという名前のルーチンを実装する必要がありますので、Windows は、ルーチンの名前で検索、 *DriverEntry*します。 ルーチンは、ドライバーの初期化タスクを実行し、フレームワークに、ドライバーのイベントのコールバック ルーチンを指定します。

次のコード例では、テンプレートによって生成された DriverEntry ルーチンを示します。

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

[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンが 2 つのパラメーター: へのポインター、 [**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)割り当てられている構造体Windows、およびドライバーのレジストリ パス。 *RegistryPath*パラメーターは、レジストリのドライバー固有のパスを表します。

[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)日常的なこれらのタスクは、ドライバーに実行します。

-   ドライバーの有効期間中に必要なグローバル リソースを割り当てます。 たとえば、テンプレート コードでクライアント ドライバー割り当てます、呼び出すことによって、WPP ソフトウェア トレースに必要なリソース、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)マクロ。
-   特定のイベント コールバック ルーチンをフレームワークに登録します。

    イベントのコールバックを登録するクライアント ドライバー最初に指定の実装へのポインター、 *EvtDriverXxx*ルーチンでは、特定の WDF 構造体。 ドライバーを呼び出して、 [ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)メソッドし、その構造 (次の手順で説明します) を提供します。

-   呼び出し、 [ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)メソッドを識別するハンドルを取得し、 *framework ドライバー オブジェクト*します。

    クライアント ドライバーの呼び出し後[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)フレームワークは、クライアント ドライバーを表すフレームワーク ドライバー オブジェクトを作成します。 クライアント ドライバーが WDFDRIVER のハンドルを受け取るし、そのレジストリ パス、バージョン情報など、ドライバーに関する情報を取得できます呼び出しが完了したら、(を参照してください[WDF ドライバー オブジェクト リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn265636))。

    フレームワーク ドライバー オブジェクトは記述する Windows ドライバー オブジェクトと異なることに注意してください。 [**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)します。 いつでも、クライアント ドライバーできますのポインターを取得する、Windows**ドライバー\_オブジェクト**構造 WDFDRIVER ハンドルを使用し、呼び出すことによって、 [ **WdfGetDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff547336)メソッド。

後に、 [ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)を呼び出すと、Windows との通信にクライアント ドライバーと framework パートナーです。 フレームワークは、Windows と、ドライバーの間の抽象化レイヤーとして機能し、ドライバーの複雑なタスクのほとんどを処理します。 イベントのフレームワークは、ドライバーに登録クライアント ドライバーで興味を持っています。 特定のイベントが発生すると、Windows には、フレームワークに通知します。 ドライバーには、特定のイベントのイベント コールバックが登録されている、フレームワークは、登録済みのイベントのコールバックを呼び出すことによって、ドライバーを通知します。 これにより、必要な場合、ドライバーは、イベントを処理することを指定するは。 ドライバーがそのイベントのコールバックを登録していない場合、フレームワークは、そのイベントの既定の処理を続行します。

ドライバーを登録する必要がありますイベントのコールバックの 1 つは[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)します。 フレームワークは、ドライバーを呼び出す*EvtDriverDeviceAdd*デバイス オブジェクトを作成する準備ができたら、framework の実装。 Windows では、デバイス オブジェクトは、物理デバイスのクライアント ドライバーが読み込まれます (このトピックで後述します)、関数の論理表現。

その他のドライバーが登録できるイベント コールバック[ *EvtDriverUnload*](https://msdn.microsoft.com/library/windows/hardware/ff541694)、 [ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)、および[*EvtDestroyCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540841)します。

テンプレート コードでは、クライアント ドライバーは 2 つのイベント登録します。[*EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)と[ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)します。 ドライバーへのポインターを指定する、その実装の*EvtDriverDeviceAdd*で、 [ **WDF\_ドライバー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)構造と*EvtCleanupCallback*イベント コールバックで、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造体。

Windows がリリースの準備完了の場合、 [**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)構造体、ドライバーをアンロードして、フレームワークを呼び出してドライバーのクライアント ドライバーにそのイベントを報告[*EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)実装します。 フレームワークは、フレームワークのドライバー オブジェクトを削除する前に、そのコールバックを呼び出します。 クライアント ドライバーで、割り当てられたすべてのグローバル リソースを解放できますその[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)します。 たとえば、テンプレート コードで、クライアント ドライバー停止、WPP トレースでのアクティブな*DriverEntry*します。

次のコード例では、クライアント ドライバーの EvtCleanupCallback イベント コールバックの実装を示します。

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

USB ドライバー スタックによって、デバイスが認識した後、バス ドライバーは、デバイスの物理デバイス オブジェクト (PDO) を作成し、[デバイス] ノードで PDO を関連付けます。 [デバイス] ノードが、スタックの構成、PDO は下部にします。 各スタックは、1 つの PDO があり、フィルター デバイス オブジェクトが (DOs をフィルター処理) と、関数のデバイス オブジェクト (FDO) 上に持つことができます。 詳細については、次を参照してください。[デバイス ノードとデバイス スタック](https://msdn.microsoft.com/library/windows/hardware/hh406296)します。

次に示します。 テンプレートのドライバー、MyUSBDriver デバイス スタック\_.sys します。

![テンプレートのドライバーのデバイス スタック](images/usb-device-stack.png)

名前付き「自分の USB デバイス」のスタック、デバイスに注意してください。 USB ドライバー スタックは、デバイス スタックの PDO を作成します。 例では、PDO は、Usbhub3.sys、USB ドライバー スタックに含まれているドライバーのいずれかに関連付けられます。 関数には、デバイスのドライバーが、としては、クライアント ドライバーは、デバイスの FDO をまず作成し、デバイス スタックの先頭にアタッチします倍にする必要があります。

KMDF ベースのクライアント ドライバーの場合は、フレームワークは、クライアント ドライバーに代わってそれらのタスクを実行します。 デバイスの FDO を表すため、フレームワークを作成、 *framework デバイス オブジェクト*します。 クライアント ドライバーでは、フレームワークを使用して、新しいオブジェクトを構成する特定の初期化パラメーターを指定できます、ただし、します。 フレームワークは、ドライバーを呼び出すときにクライアント ドライバに機会が与えられている[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)実装します。 オブジェクトが作成され、デバイス スタックの先頭に、FDO がアタッチされている、フレームワークはフレームワークのデバイス オブジェクトを WDFDEVICE ハンドルを持つクライアント ドライバーを提供します。 このハンドルを使用すると、クライアント ドライバーは、さまざまなデバイスに関連する操作を実行できます。

次のコード例では、クライアント ドライバーの EvtDriverDeviceAdd イベント コールバックの実装を示します。

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

実行時の実装に[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)を使用して、 [**ページ\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)ことを確認するマクロ、ルーチンは、ページング可能なコードの適切な環境で呼び出されています。 すべての変数には; を宣言した後、マクロを呼び出すかどうかを確認します。それ以外の場合、生成されたソース ファイルは、.c ファイルと .cpp ファイルではないために、コンパイルが失敗します。

クライアント ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)実装、MyUSBDriver\_CreateDevice のヘルパー関数に必要なタスクを実行します。

次のコード例に示します、MyUSBDriver\_CreateDevice ヘルパー関数。 MyUSBDriver\_CreateDevice が Device.c で定義されています。

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

[*EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)は 2 つのパラメーターがあります: 以前の呼び出しでフレームワーク ドライバー オブジェクトへのハンドルが作成された[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)へのポインター、 [**WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。 フレームワークを割り当てます、 **WDFDEVICE\_INIT**構造体し、クライアント ドライバーが初期化のパラメーターを framework デバイス オブジェクトを作成するを構造体を設定するためにポインターに渡します。

[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)実装では、クライアント ドライバーは、これらのタスクを実行する必要があります。

-   呼び出す、 [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926) WDFDEVICE を取得するメソッドを新しいデバイス オブジェクトを処理します。

    [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)メソッドにより、FDO 用 framework デバイス オブジェクトを作成し、デバイス スタックの一番上にアタッチするフレームワークです。 **WdfDeviceCreate**を呼び出すと、クライアント ドライバーは、これらのタスクを実行する必要があります。

    -   フレームワーク固有のクライアント ドライバーのプラグ アンド プレイ (PnP) power コールバック ルーチンへのポインターを指定[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。 ルーチンは最初設定、 [ **WDF\_PNPPOWER\_イベント\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff552416)構造体であり、WDFDEVICE に関連付けられている\_呼び出して INIT[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135)メソッド。

        Windows コンポーネント、PnP し電源マネージャー、ドライバーの PnP 状態 (開始、停止し、削除) の変更に応答をデバイスに関連する要求を送信および電源の状態 (操作または一時停止など)。 KMDF ベースのドライバーでは、フレームワークは、それらの要求をインターセプトします。 クライアント ドライバーは、呼び出されるコールバック ルーチンを登録することによって要求について通知を取得*電源イベントのコールバックの PnP*を使用して、フレームワークで、 [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)呼び出します。 Windows コンポーネントは、要求を送信、フレームワークは処理し、呼び出し、対応する PnP 電源イベント コールバックでは、クライアント ドライバーが登録されている場合。

        クライアント ドライバーを実装する必要があります、PnP 電源イベント コールバック ルーチンの 1 つは[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)します。 PnP マネージャーの起動時、デバイスには、そのイベントのコールバックが呼び出されます。 実装*EvtDevicePrepareHardware*については、次のセクションで説明します。

    -   ドライバーのデバイス コンテキストの構造体へのポインターを指定します。 ポインターを設定する必要があります、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)呼び出すことによって初期化される構造体、 [ **WDF\_オブジェクト\_属性\_INIT\_コンテキスト\_型**](https://msdn.microsoft.com/library/windows/hardware/ff552400_init_context_type)マクロ。

        デバイス コンテキスト (デバイスの拡張機能とも呼ばれます) は、特定のデバイス オブジェクトに関する情報を格納するための (クライアント ドライバーで定義された) データ構造です。 クライアント ドライバーは、フレームワークには、そのデバイス コンテキストへのポインターを渡します。 フレームワークは、構造体のサイズに基づいて、メモリのブロックを割り当て、そのメモリ位置へのポインターを framework デバイス オブジェクトに格納します。 クライアント ドライバーは、ポインターを使用して、アクセスして、デバイス コンテキストのメンバーに情報を格納することができます。 デバイス コンテキストの詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](https://msdn.microsoft.com/library/windows/hardware/ff542873)します。

        後に、 [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)呼び出しが完了すると、クライアント ドライバーがデバイスのフレームワークによって割り当てられたメモリ ブロックへのポインターを格納する新しいフレームワーク デバイス オブジェクトを識別するハンドルを受け取りますコンテキスト。 クライアント ドライバーられるようになりましたポインター デバイス コンテキストを呼び出すことによって、 **WdfObjectGet\_デバイス\_コンテキスト**マクロ。

-   呼び出すことによって、クライアント ドライバーのデバイス インターフェイスの GUID を登録、 [ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)メソッド。 アプリケーションは、この GUID を使用して、ドライバーと通信できます。 GUID 定数は、ヘッダーで宣言されて public.h します。
-   デバイスの I/O 転送キューを設定します。 テンプレート コード定義 MyUSBDriver\_QueueInitialize、については、キューを設定するためのヘルパー ルーチン、[ソース コードをキュー](#queue)セクション。

## <a name="device-source-code"></a>デバイスのソース コード


*デバイス オブジェクト*対象のクライアント ドライバーがメモリに読み込まれたデバイスのインスタンスを表します。 デバイス オブジェクトの完全なソース コードは、Device.h と Device.c です。

**Device.h**

Device.h ヘッダー ファイルには、プロジェクト内のすべてのファイルで使用される一般的な宣言を含む、public.h が含まれています。

Device.h の次のブロックは、クライアント ドライバー用にデバイス コンテキストを宣言します。

```ManagedCPlusPlus
typedef struct _DEVICE_CONTEXT
{
    WDFUSBDEVICE UsbDevice;
    ULONG PrivateDeviceData;  // just a placeholder

} DEVICE_CONTEXT, *PDEVICE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(DEVICE_CONTEXT)
```

**デバイス\_コンテキスト**構造体は、クライアント ドライバーによって定義され、framework デバイス オブジェクトに関する情報を格納します。 Device.h で宣言されていて、2 つのメンバーが含まれています。 フレームワークの USB を識別するハンドルをターゲット デバイスのオブジェクト (後述) と、プレース ホルダーです。 以降の演習では、この構造体が展開されます。

Device.h も含まれています、 **WDF\_DECLARE\_コンテキスト\_型**マクロで、インライン関数を生成するには、 **WdfObjectGet\_デバイス\_コンテキスト**します。 クライアント ドライバーでは、フレームワークのデバイス オブジェクトからメモリ ブロックへのポインターを取得するには、その関数を呼び出すことができます。

次のコード行宣言 MyUSBDriver\_CreateDevice、USB ターゲットのデバイス オブジェクト WDFUSBDEVICE ハンドルを取得するヘルパー関数。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_CreateDevice(
    _Inout_ PWDFDEVICE_INIT DeviceInit
    );
```

USBCreate へのポインターを受け取り、 [WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)パラメーターとして構造体。 これは、クライアント ドライバーの呼び出されたときにフレームワークによって渡されたポインターと同じ[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)実装します。 基本的に、MyUSBDriver\_CreateDevice のタスクを実行する*EvtDriverDeviceAdd*します。 ソース コード*EvtDriverDeviceAdd*実装は、前のセクションで説明します。

Device.h の次の行の関数の役割の型宣言の宣言、 [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)イベント コールバック ルーチン。 イベントのコールバックは、クライアント ドライバーによって実装され、USB デバイスの構成などのタスクを実行します。

```ManagedCPlusPlus
EVT_WDF_DEVICE_PREPARE_HARDWARE MyUSBDriver_EvtDevicePrepareHardware;
```

**Device.c**

Device.c 実装ファイルには、次を使用するコードのブロックが含まれています`alloc_text`ことを指定するプラグマのドライバーの実装[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)ページング可能では、。メモリ。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_CreateDevice)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDevicePrepareHardware)
#endif
```

実装で[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)、クライアント ドライバーが USB に固有の初期化タスクを実行します。 これらのタスクには、クライアント ドライバーの登録、特定の USB I/O ターゲットのオブジェクトの初期化および USB 構成の選択が含まれます。 次の表では、フレームワークによって提供される特殊な I/O ターゲット オブジェクトを示します。 詳細については、次を参照してください。 [USB I/O ターゲット](https://msdn.microsoft.com/library/windows/hardware/ff544752)します。

| USB I/O ターゲット オブジェクト (ハンドル)                   | 呼び出すことによって、ハンドルを取得してください.                                                          | 説明                                                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *ターゲット デバイス オブジェクトの USB* (WDFUSBDEVICE)       | [**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428) | USB デバイスを表し、デバイス記述子を取得し、デバイスに対する制御要求を送信するためのメソッドを提供します。                                                                                                                                                                                                                 |
| *USB ターゲット インターフェイス オブジェクト*(WDFUSBINTERFACE) | [**WdfUsbTargetDeviceGetInterface**](https://msdn.microsoft.com/library/windows/hardware/ff550092)             | 個別のインターフェイスを表し、代替の設定を選択し、設定に関する情報を取得するクライアント ドライバーを呼び出すことができるメソッドを提供します。                                                                                                                                                                              |
| *USB ターゲット パイプ オブジェクト*(WDFUSBPIPE)            | [**WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)         | インターフェイスの現在の代替設定で構成されているエンドポイントの個別のパイプを表します。 USB ドライバー スタックは、選択した構成の各インターフェイスを選択し、インターフェイス内で各エンドポイントへの通信チャネルを設定します。 USB 用語では、その通信チャネルと呼ばれる、*パイプ*します。 |

 

このコード例では、EvtDevicePrepareHardware の実装を示します。

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

次テンプレート コードで実装されるように、クライアント ドライバーのタスクの詳細を示します。

1.  Windows によって読み込まれる、基になる USB ドライバー スタックに登録する準備として、クライアント ドライバーのコントラクトのバージョンを指定します。

    Windows では、USB 3.0 または USB 2.0 ドライバー スタックの USB デバイスが接続されているホスト コント ローラーによってを読み込むことができます。 USB 3.0 ドライバー スタックは、Windows 8 の新機能は、し、ストリーム機能など、USB 3.0 仕様で定義されているいくつかの新機能をサポートします。 新しいドライバー スタックは、追跡との USB 要求のブロック (翻訳) URB ルーチンの新しいセットはされている処理の向上など、いくつかの機能強化も実装します。 これらの機能を使用して、または新しいルーチンを呼び出すしようとしています。 クライアント ドライバーは、USBD を指定する必要があります\_クライアント\_コントラクト\_バージョン\_602 のコントラクト バージョン。 USBD\_クライアント\_コントラクト\_バージョン\_602 のクライアント ドライバーは、特定の一連の規則に従う必要があります。 これらのルールの詳細については、次を参照してください。[ベスト プラクティス。翻訳を使用して](usb-client-driver-contract-in-windows-8.md)します。

    コントラクトのバージョンを指定するには、クライアント ドライバーを初期化する必要があります、 [ **WDF\_USB\_デバイス\_作成\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/hh406503)構造体、コントラクトのバージョンを呼び出して、 [ **WDF\_USB\_デバイス\_作成\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/hh406503_init)マクロ。

2.  呼び出し、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)メソッド。 メソッドを呼び出して、クライアント ドライバーが以前に取得する framework デバイス オブジェクトを識別するハンドルを必要と[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)のドライバーの実装で[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)します。 **WdfUsbTargetDeviceCreateWithParameters**メソッド。
    -   基になる USB ドライバー スタックをクライアント ドライバーを登録します。
    -   フレームワークによって作成される USB ターゲット デバイス オブジェクトを識別する WDFUSBDEVICE ハンドルを取得します。 テンプレート コードでは、そのデバイス コンテキストで、USB ターゲット デバイス オブジェクトを識別するハンドルを格納します。 そのハンドルを使用すると、クライアント ドライバーは、デバイスの USB に固有の情報を取得できます。

    **注**  呼び出す必要があります[ **WdfUsbTargetDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550077)の代わりに[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/ff550077withconfig)場合、
    -   クライアント ドライバーでは、Windows 8 バージョンの WDK で新しい URB ルーチンのセットは呼び出されません。

        クライアント ドライバーを呼び出す場合[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)、USB ドライバー スタックは、すべての翻訳が呼び出すことによって割り当てられている前提としています[  **。WdfUsbTargetDeviceCreateUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439423)または[ **WdfUsbTargetDeviceCreateIsochUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439420)します。 これらのメソッドによって割り当てられている翻訳には、高速化を処理するため、USB ドライバー スタックで使用される非透過の URB コンテキスト ブロックがあります。 クライアント ドライバーには、これらのメソッドによって割り当てられていない、URB が使用して、USB ドライバーのバグチェックが生成されます。

        URB 割り当ての詳細については、次を参照してください。[割り当てと構成の翻訳](how-to-add-xrb-support-for-client-drivers.md)します。

    -   説明する規則のセットに準拠するには、クライアント ドライバーは予定はありません[ベスト プラクティス。翻訳を使用して](usb-client-driver-contract-in-windows-8.md)します。

    このようなドライバーは、クライアント コントラクトのバージョンを指定する必要のないし、そのため、手順 1. をスキップする必要があります。

     

3.  USB の設定を選択します。

    テンプレートのコードでは、クライアント ドライバーを選択、*既定の構成*USB デバイスにします。 既定の構成には、0 またはデバイスの構成とその構成内の各インターフェイスの代替設定 0 が含まれています。

    クライアント ドライバーを構成する既定の構成を選択、 [ **WDF\_USB\_デバイス\_選択\_CONFIG\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552600)構造を呼び出すことによって、 [ **WDF\_USB\_デバイス\_選択\_CONFIG\_PARAMS\_INIT\_複数\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff552600_init_multiple_interfaces)関数。 関数を初期化します、**型**メンバー **WdfUsbTargetDeviceSelectConfigTypeMultiInterface**を示す場合に複数のインターフェイスを利用し、代替のものでは、各設定インターフェイスを選択する必要があります。 クライアント ドライバーが内の NULL を指定する呼び出しは、既定の構成を選択する必要があります、ため、 *SettingPairs*パラメーターとでは 0、 *NumberInterfaces*パラメーター。 完了すると、 **MultiInterface.NumberOfConfiguredInterfaces**のメンバー **WDF\_USB\_デバイス\_選択\_CONFIG\_PARAMS** 0 の代替設定が選択されているインターフェイスの数を示します。 他のメンバーは変更されません。

    **注**  クライアント ドライバーは、既定の設定以外の別の設定を選択する場合、ドライバーの配列を作成する必要があります[ **WDF\_USB\_インターフェイス\_設定\_ペア**](https://msdn.microsoft.com/library/windows/hardware/ff553023)構造体。 配列内の各要素を選択するには、デバイス定義のインターフェイスの数と、別の設定のインデックスを指定します。 呼び出すことによって取得できるデバイスの構成とインターフェイス記述子の情報を保存すること、 [ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550098)メソッド。 クライアント ドライバーは呼び出す必要がありますし、 [ **WDF\_USB\_デバイス\_選択\_CONFIG\_PARAMS\_INIT\_複数\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff552992)を渡すと、 **WDF\_USB\_インターフェイス\_設定\_ペア**フレームワークへの配列。

     

## <a name="queue-source-code"></a>キュー ソース コード


*Framework キュー オブジェクト*特定のフレームワークのデバイス オブジェクトの I/O キューを表します。 キュー オブジェクトの完全なソース コードは、Queue.h と Queue.c です。

**Queue.h**

フレームワークのキュー オブジェクトによって発生するイベントのイベント コールバック ルーチンを宣言します。

Queue.h で最初のブロックは、キューのコンテキストを宣言します。

```ManagedCPlusPlus
typedef struct _QUEUE_CONTEXT {

    ULONG PrivateDeviceData;  // just a placeholder

} QUEUE_CONTEXT, *PQUEUE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(QUEUE_CONTEXT, QueueGetContext)
```

キューのコンテキストは、デバイス コンテキストと同様に、特定のキューに関する情報を格納するクライアントによって定義されるデータ構造です。

次のコード行宣言 MyUSBDriver\_QueueInitialize 関数、ヘルパー関数を作成し、フレームワークのキュー オブジェクトを初期化します。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_QueueInitialize(
    _In_ WDFDEVICE Device
    );
```

次のコード例の関数の役割の型宣言の宣言、 [ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)イベント コールバック ルーチン。 イベントのコールバックは、クライアント ドライバーによって実装されが、フレームワークは、デバイスの I/O 制御要求を処理するときに呼び出されます。

```ManagedCPlusPlus
EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL MyUSBDriver_EvtIoDeviceControl;
```

**Queue.c**

Queue.c、実装ファイルには、次を使用するコードのブロックが含まれています。`alloc_text`ことを指定するプラグマ MyUSBDriver のドライバーの実装\_QueueInitialize はページング可能なメモリ。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_QueueInitialize)
#endif
```

WDF は、クライアント ドライバーに要求のフローを処理するために、フレームワークのキュー オブジェクトを提供します。 クライアント ドライバーを呼び出すときに、フレームワークが framework キュー オブジェクトを作成、 [ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)メソッド。 その呼び出しで、クライアント ドライバーは、フレームワークは、キューを作成する前に特定の構成オプションを指定できます。 これらのオプションには、キューは電源管理、長さ 0 の要求を許可またはドライバーの既定のキューは、かどうかが含まれます。 1 つのフレームワークのキュー オブジェクトは、いくつかの種類の読み取り、書き込み、およびデバイス I/O コントロールなどの要求を処理できます。 クライアント ドライバーでは、それらの要求の各イベントのコールバックを指定できます。

クライアント ドライバーでは、ディスパッチ種類も指定する必要があります。 キュー オブジェクトのディスパッチの型は、クライアント ドライバーに、フレームワークが要求を配信する方法を決定します。 並列、またはクライアント ドライバーで定義されたカスタムのメカニズムによって、順次配信メカニズムは使用できます。 シーケンシャルなキューの場合、クライアント ドライバーが、前回の要求を完了するまで、要求は配信されません。 ディスパッチを並列モードでは、フレームワークは、I/O マネージャーから到着すると、すぐに、要求を転送します。 これは、クライアント ドライバーは、別の処理中に 1 つの要求を受信できることを意味します。 カスタムのメカニズムで、クライアントでは、ドライバーが処理する準備ができたときフレームワークのキュー オブジェクトから、次の要求が手動で取得します。

通常、クライアント ドライバーがドライバーのキューを設定する必要があります[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)イベント コールバック。 テンプレート コードは、ヘルパー ルーチン、MyUSBDriver\_QueueInitialize、フレームワークのキュー オブジェクトを初期化します。

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

キューを設定するには、クライアント ドライバーは、これらのタスクを実行します。

1.  キューの構成オプションを指定します、 [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)構造体。 テンプレート コードを使用して、 [ **WDF\_IO\_キュー\_CONFIG\_INIT\_既定\_キュー** ](https://msdn.microsoft.com/library/windows/hardware/ff552359_init_default_queue)関数構造体を初期化します。 関数は、既定のキュー オブジェクトとして、キュー オブジェクトを指定します、電源管理は、および並列の要求を受信します。
2.  キューの I/O 要求のクライアント ドライバーのイベントのコールバックを追加します。 テンプレートでは、クライアント ドライバーには、デバイスの I/O 制御要求の場合は、そのイベント コールバックへのポインターを指定します。
3.  呼び出し[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)フレームワークによって作成されるフレームワークのキュー オブジェクトへの WDFQUEUE ハンドルを取得します。

キュー メカニズムの動作方法を示します。 USB デバイスと通信して、アプリケーション最初を開いたデバイスへのハンドルを呼び出すことによって、 **SetDixxx**ルーチンと[ **CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)します。 このハンドルを使用して、アプリケーションを呼び出す、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/hh404258)関数の特定のコントロールのコード。 、コントロールのコードの種類に応じて、アプリケーションは、その呼び出しの入力と出力バッファーを指定できます。 呼び出しは、I/O マネージャーによって、要求 (IRP) を作成し、クライアント ドライバーに転送するを最終的に受信されます。 フレームワーク要求を受信するには、フレームワーク、要求オブジェクトを作成およびフレームワークのキュー オブジェクトに追加します。 この場合、クライアント ドライバーには、デバイスの I/O 制御要求の場合は、そのイベント コールバックが登録されている、ため、フレームワークは、コールバックを呼び出します。 また、WdfIoQueueDispatchParallel フラグを使用して、キュー オブジェクトが作成されたため、コールバックが呼び出される、要求がキューに追加されるとすぐにします。

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

要求 (およびその入力と出力のバッファー) を保持している framework 要求オブジェクトにハンドルを渡すために、フレームワークが、クライアント ドライバーのイベントのコールバックを呼び出すと、アプリケーションによって送信されます。 さらに、要求を格納するフレームワークのキュー オブジェクトへのハンドルを送信します。 イベントのコールバックでは、クライアント ドライバーが要求を処理に応じて。 テンプレート コードは、単に、要求を完了します。 クライアント ドライバーより複雑なタスクを実行できます。 たとえば、アプリケーションでは、特定のデバイス情報を要求している場合イベントのコールバック、クライアント ドライバーを USB 制御の要求を作成し、送信要求されたデバイス情報を取得する USB ドライバー スタックに。 USB 制御の要求は、後ほど[USB 制御転送](usb-control-transfer.md)します。

## <a name="related-topics"></a>関連トピック
[USB クライアント ドライバー開発の概要](getting-started-with-usb-client-driver-development.md)  
[WinUSB](winusb.md)  
[最初、USB クライアント ドライバー (UMDF) の記述します。](implement-driver-entry-for-a-usb-driver--umdf-.md)  
[最初、USB クライアント ドライバー (KMDF) の記述します。](tutorial--write-your-first-usb-client-driver--kmdf-.md)  



