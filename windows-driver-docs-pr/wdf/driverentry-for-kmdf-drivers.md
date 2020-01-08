---
title: WDF ドライバー用 DriverEntry ルーチン
description: DriverEntry は、ドライバーによって提供される最初のルーチンで、ドライバーが読み込まれた後に呼び出されます。 ドライバーを初期化する必要があります。
ms.assetid: b49d1767-7cfd-45bb-a2be-0597f7373e79
keywords:
- DriverEntry ルーチン
- ルーチン
- DRIVER_INITIALIZE ルーチン
topic_type:
- apiref
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 05aeeb2605ce6c2300754b6db01874182344d0e8
ms.sourcegitcommit: 9355a80229bb2384dd45493d36bdc783abdd8d7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694248"
---
# <a name="driverentry-for-wdf-drivers-routine"></a>WDF ドライバー用 DriverEntry ルーチン


\[KMDF と UMDF\] に適用されます

**Driverentry**は、ドライバーによって提供される最初のルーチンで、ドライバーが読み込まれた後に呼び出されます。 ドライバーを初期化する必要があります。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>パラメーター
----------

*Driverobject* \[\]  
ドライバーの WDM ドライバーオブジェクトを表す[**ドライバー\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造体へのポインター。

\] の*RegistryPath* \[  
レジストリ内のドライバーの[パラメーターキー](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-registry-keys-for-drivers)へのパスを指定する[**UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)構造体へのポインター。

<a name="return-value"></a>戻り値
------------

ルーチンが成功した場合、状態\_SUCCESS を返す必要があります。 それ以外の場合は、 *ntstatus*に定義されているエラー状態の値の1つを返す必要があります。

<a name="remarks"></a>注釈
-------

すべての WDM ドライバーと同様に、フレームワークベースのドライバーには**Driverentry**ルーチンが必要です。これは、ドライバーが読み込まれた後に呼び出されます。 フレームワークベースのドライバーの**Driverentry**ルーチンでは、次のことを行う必要があります。

-   [WPP ソフトウェアトレース](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers)をアクティブにします。

    **Driverentry**には、ソフトウェアトレースをアクティブ化するために、 [WPP\_INIT\_TRACING](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロが含まれている必要があります。

-   [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出します。

    [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出すと、ドライバーは Windows driver Framework インターフェイスを使用できるようになります。 (ドライバーは、 **Wdfdrivercreate**を呼び出す前に他のフレームワークルーチンを呼び出すことはできません)。

-   必要に応じて、デバイス固有ではないシステムリソースとグローバル変数を割り当てます。

    通常、ドライバーは、システムリソースを個々のデバイスに関連付けます。 したがって、フレームワークベースのドライバーは、ほとんどのリソースを[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックに割り当てます。これは、個々のデバイスが検出されたときに呼び出されます。

    UMDF ドライバーの複数のインスタンスは Wudfhost の個別のインスタンスによってホストされる可能性があるため、グローバル変数は、UMDF ドライバーのすべてのインスタンスで使用できない可能性があります。

-   レジストリからドライバー固有のパラメーターを取得します。

    一部のドライバーでは、レジストリからパラメーターを取得します。 これらのドライバーは、 [**WdfDriverOpenParametersRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey)を呼び出して、これらのパラメーターを含むレジストリキーを開くことができます。

-   [Driverentry の戻り値](https://docs.microsoft.com/windows-hardware/drivers/kernel/driverentry-return-values)を指定してください。

UMDF ドライバーはユーザーモードのホストプロセスで実行されますが、KMDF ドライバーはシステムプロセスでカーネルモードで実行される  に**注意**してください。 フレームワークは、UMDF ドライバーの複数のインスタンスをホストプロセスの個別のインスタンスに読み込む場合があります。 結果:

 

-   フレームワークは、さまざまなホストプロセスでドライバーのインスタンスを読み込む場合、UMDF ドライバーの DriverEntry ルーチンを複数回呼び出す場合があります。 これに対して、フレームワークは KMDF ドライバーの DriverEntry ルーチンを1回だけ呼び出します。
-   UMDF ドライバーが DriverEntry ルーチンにグローバル変数を作成した場合、その変数はドライバーのすべてのインスタンスで使用できない可能性があります。 ただし、KMDF ドライバーが DriverEntry ルーチンに作成するグローバル変数は、ドライバーのすべてのインスタンスで使用できます。

フレームワークベースのドライバーの**Driverentry**ルーチンが呼び出されるタイミングの詳細については、「 [WDF ドライバーのビルドと読み込み](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-and-loading-a-kmdf-driver)」を参照してください。

**Driverentry**ルーチンが WDK ヘッダーで宣言されていません。 Static Driver Verifier (SDV) およびその他の検証ツールでは、次のような宣言が必要になる場合があります。

``` syntax
DRIVER_INITIALIZE MyDriverEntry;

NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT  DriverObject,
    IN PUNICODE_STRING  RegistryPath
    )
{
// Function body
}
```

<a name="examples"></a>例
--------

次のコード例は、シリアル (KMDF) サンプルドライバーの**Driverentry**ルーチンを示しています。

```cpp
NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT  DriverObject,
    IN PUNICODE_STRING  RegistryPath
    )
{
    WDF_DRIVER_CONFIG  config;
    WDFDRIVER  hDriver;
    NTSTATUS  status;
    WDF_OBJECT_ATTRIBUTES  attributes;
    SERIAL_FIRMWARE_DATA driverDefaults;

    //
    // Initialize WPP tracing.
    //
    WPP_INIT_TRACING(
                     DriverObject,
                     RegistryPath
                     );

    SerialDbgPrintEx(
                     TRACE_LEVEL_INFORMATION,
                     DBG_INIT,
                     "Serial Sample (WDF Version) - Built %s %s\n",
                     __DATE__, __TIME__
                     );
    //
    // Register a cleanup callback function (which calls WPP_CLEANUP)
    // for the framework driver object. The framework will call
    // the cleanup callback function when it deletes the driver object,
    // before the driver is unloaded.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = SerialEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(
                           &config,
                           SerialEvtDeviceAdd
                           );

    status = WdfDriverCreate(
                             DriverObject,
                             RegistryPath,
                             &attributes,
                             &config,
                             &hDriver
                             );
    if (!NT_SUCCESS(status)) {
        SerialDbgPrintEx(
                         TRACE_LEVEL_ERROR,
                         DBG_INIT,
                         "WdfDriverCreate failed with status 0x%x\n",
                         status
                         );
        //
        // Clean up tracing here because WdfDriverCreate failed.
        //
        WPP_CLEANUP(DriverObject);
        return status;
    }

    //
    // Call an internal routine to obtain registry values
    // to use for all the devices that the driver 
    // controls, including whether or not to break on entry.
    //
    SerialGetConfigDefaults(
                            &driverDefaults,
                            hDriver
                            );

    //
    // Break on entry if requested bt registry value.
    //
    if (driverDefaults.ShouldBreakOnEntry) {
        DbgBreakPoint();
    }

    return status;
}
```

## <a name="see-also"></a>「


[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)

[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)

 

 






