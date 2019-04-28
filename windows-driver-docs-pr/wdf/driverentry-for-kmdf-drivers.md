---
title: WDF ドライバー用 DriverEntry ルーチン
description: DriverEntry は、ドライバーによって提供されるドライバーが読み込まれた後に呼び出される最初のルーチンです。 ドライバーを初期化するため、します。
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
ms.openlocfilehash: 2e031668ed6abbc5bc50412c051ecc5cb0a8f523
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379508"
---
# <a name="driverentry-for-wdf-drivers-routine"></a>WDF ドライバー用 DriverEntry ルーチン


\[KMDF および UMDF に適用されます。\]

**DriverEntry**はドライバーによって提供されるドライバーが読み込まれた後に呼び出される最初のルーチンです。 ドライバーを初期化するため、します。

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

*DriverObject* \[in\]  
ポインターを[**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)ドライバーの WDM ドライバー オブジェクトを表す構造体です。

*RegistryPath* \[で\]  
ポインターを[ **UNICODE\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff564879)ドライバーのパスを指定する構造体[パラメーター キー](https://msdn.microsoft.com/library/windows/hardware/ff544262)レジストリにします。

<a name="return-value"></a>戻り値
------------

状態を返す必要があります、ルーチンが成功すると、\_成功します。 それ以外の場合、いずれかで定義されているエラー状態の値を返す必要が*ntstatus.h*します。

<a name="remarks"></a>注釈
-------

WDM ドライバーをすべてのように、フレームワーク ベースのドライバーが必要、 **DriverEntry**ルーチンは、ドライバーが読み込まれた後に呼び出されます。 フレームワーク ベースのドライバーの**DriverEntry**ルーチンにする必要があります。

-   アクティブ化[WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/dn940485)します。

    **DriverEntry**含める必要があります、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)ソフトウェア トレースをアクティブ化するマクロ。

-   呼び出す[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)します。

    呼び出し[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175) Windows Driver Framework インターフェイスを使用するドライバーを使用します。 (ドライバーは、呼び出す前にその他のフレームワークのルーチンを呼び出すことはできません**WdfDriverCreate**)。

-   任意のデバイスに固有のシステム リソースとが必要とされるグローバル変数を割り当てます。

    通常、ドライバーは、個々 のデバイスでシステム リソースを関連付けます。 そのため、framework ベースのドライバーがほとんどのリソースを割り当てる、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693) 、個々 のデバイスが検出されたときに呼び出されるコールバック。

    UMDF ドライバーの複数のインスタンスは、Wudfhost の個別のインスタンスでホストされる場合があります、ため、グローバル変数できない可能性があります UMDF ドライバーのすべてのインスタンス。

-   ドライバー固有のパラメーターをレジストリから取得します。

    一部のドライバーでは、レジストリからパラメーターを取得します。 これらのドライバーが呼び出せる[ **WdfDriverOpenParametersRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547202)をこれらのパラメーターを格納するレジストリ キーを開きます。

-   提供、 [DriverEntry 戻り値](https://msdn.microsoft.com/library/windows/hardware/ff544119)します。

**注**  A UMDF ドライバーは、KMDF ドライバーがシステム プロセスのカーネル モードで実行中に、ユーザー モードのホスト プロセスで実行します。 フレームワークは、ホスト プロセスのインスタンスを個別に UMDF ドライバーの複数のインスタンスを読み込む可能性があります。 その結果：

 

-   フレームワークが UMDF ドライバーの DriverEntry ルーチンを複数回呼び出す別のホスト プロセス内のドライバーのインスタンスを読み込む場合。 これに対し、フレームワークは、KMDF ドライバーの DriverEntry ルーチンを 1 回だけ呼び出します。
-   UMDF ドライバーでは、その DriverEntry ルーチンでグローバル変数を作成する場合、変数できない可能性がありますが、ドライバーのすべてのインスタンスに。 ただし、その DriverEntry ルーチンで KMDF ドライバーを作成するグローバル変数は、ドライバーのすべてのインスタンスを使用できます。

タイミングの詳細については framework ベースのドライバーの**DriverEntry**ルーチンを呼び出すを参照してください[WDF ドライバーの読み込みのビルドと](https://msdn.microsoft.com/library/windows/hardware/ff540730)します。

**DriverEntry**ルーチンが WDK ヘッダーで宣言されていません。 Static Driver Verifier (SDV) とその他の検証ツールには、次のような宣言が必要とする可能性があります。

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

次のコード例に示しますシリアル (KMDF) サンプル ドライバーの**DriverEntry**ルーチン。

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
    WDF_OBJECT_ATTRIBUTES_INIT(&amp;attributes);
    attributes.EvtCleanupCallback = SerialEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(
                           &amp;config,
                           SerialEvtDeviceAdd
                           );

    status = WdfDriverCreate(
                             DriverObject,
                             RegistryPath,
                             &amp;attributes,
                             &amp;config,
                             &amp;hDriver
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
                            &amp;driverDefaults,
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

## <a name="see-also"></a>関連項目


[**WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)

[*EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)

 

 






