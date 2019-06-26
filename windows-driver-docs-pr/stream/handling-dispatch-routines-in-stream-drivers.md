---
title: ストリーム ドライバーのディスパッチ ルーチンの処理
description: ドライバーのディスパッチ ルーチンの処理に関するガイダンスを提供します。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 96ee7740ce65caa8c981912125f2d2e19512dc81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384051"
---
# <a name="handling-dispatch-routines-in-stream-drivers"></a>ストリーム ドライバーのディスパッチ ルーチンの処理

このトピックでは、ドライバーのディスパッチ ルーチンの処理に関するガイダンスを提供します。

## <a name="adddevice-routine-for-avstream-minidrivers"></a>AVStream ミニドライバーの AddDevice ルーチン

ほとんどの AVStream ミニドライバーを指定しない独自*AddDevice*ルーチン。 代わりに、使用[ **KsAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksadddevice)、既定の*AddDevice*によってインストールされているハンドラー [ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver). それでもの提供を希望独自ミニドライバー *AddDevice*ハンドラーは、次のガイドラインに従う必要があります。

ドライバーを呼び出す場合[ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)中に*DriverEntry*され、後で置き換えられます、 *AddDevice*ハンドラー、ミニドライバーできます呼び出す[ **KsAddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksadddevice)からこのルーチン内で実行する既定の処理を追加します。

呼び出すことができます、ミニドライバー [ **KsCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatedevice)名目上オプションを渡して、このルーチンから[ **KSDEVICE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_descriptor). 場合[ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)がこれには、記述子によって記述された AVStream デバイスを作成する最高レベルの呼び出しが呼び出されない。

呼び出す必要がありますが、ミニドライバーは、独自 FDO を作成し、手動でデバイス スタックに添付されて場合、 [ **KsInitializeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedevice) AVStream デバイスを作成します。

ドライバーが提供されていない場合、 [ **KSDEVICE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_descriptor)デバイスがまだ作成して AVStream 既定 AVStream のデバイスを作成します。 このデバイスは、フィルター ファクトリが含まれていないし、決してミニドライバーにディスパッチします。 ミニドライバーをインスタンス化も[ **KSFILTERFACTORY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilterfactory)呼び出すことによって、デバイス上の構造[ **KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatefilterfactory)します。

独自にインストールする*AddDevice*ハンドラー。

```cpp
DriverObject->DriverExtension->AddDevice=MyAddDevice();
```
AVStream ミニドライバーが提供する機能を使用することをお勧めします[ **KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)ではなく、既定値よりも*AddDevice*によって提供されるルーチン。クラスのドライバーです。

詳細については、次を参照してください。、 [DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)コールバック関数。

## <a name="driverentry-routine-for-stream-class-minidrivers"></a>Stream クラス ミニドライバーの DriverEntry ルーチン

**DriverEntry**ストリーム クラスのミニドライバーの初期のエントリ ポイントです。 このルーチンが必要です。

[ **StreamClassRegisterMinidriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisteradapter) 、必要なドライバーの初期化のストリーム クラス ミニドライバーの主要なタスクのほとんどを実行**DriverEntry**ルーチン割り当てし、入力には、 [ **HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)ドライバー固有の定数とエントリ ポイントを含む構造体。 **DriverEntry**呼び出す必要がありますし、 **StreamClassRegisterMinidriver**します。

詳細については、次を参照してください。、 [DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)コールバック関数。

## <a name="driverentry-function-of-avstream-minidriver-function"></a>AVStream ミニドライバー関数の DriverEntry 関数

*DriverEntry*関数は、AVStream ミニドライバーへの初期のエントリ ポイント。

各 AVStream ミニドライバーは、明示的にという名前の関数をいる必要があります*DriverEntry*読み込まれるためです。 *DriverEntry* I/O システムで直接呼び出されます。 通常、 *DriverEntry*呼び出し[ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)によって返される値を返します**KsInitializeDriver**します。

詳細については、次を参照してください。、 [DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)コールバック関数。

## <a name="kscancelroutine-function"></a>KsCancelRoutine 関数

**KsCancelRoutine**関数は、標準的な IRP のキャンセル機能を実行します。 エントリを削除およびをキャンセルし、要求を完了します。 関数が、PDRIVER として定義されている\_キャンセル ルーチン。 使用される既定の関数は**KsAddIrpToCancelableQueue**がない場合。

この関数は、通常キャンセル IRP の I/O サブシステムによって呼び出されますが、KSMETHOD への応答で直接呼び出すことができます\_ストリーム\_要求のプレゼンテーションを設定します。 任意の一般的なキャンセル ルーチンとは、この関数は、関数の入力時に取得された I/O キャンセル スピン ロックを要求します。

このルーチンが、KSQUEUE を期待しているメモ\_スピンロック\_IRP\_で指定されたリストへのアクセスのスピン ロックを指す STORAGE(Irp) **KsAddIrpToCancelableQueue**します。

**KsCancelRoutine** IRP を実際に完了しなくても、処理、暫定版 ボックスの一覧の削除を行うために使用できます。 場合 Irp -&gt;IoStatus.Status が状態に設定されている\_取り消された場合に、この関数を入力して、IRP は完了しません。 ステータス、状態を設定する場合は、\_キャンセルおよび IRP が完了します。 これは、 **KsCancelRoutine**を最初のリストの操作を行います、スピン ロック操作と固有の処理と最終的な IRP の完了を行うドライバーの完了ルーチンに戻りますキャンセル ルーチン内で使用できます。

詳細については、次を参照してください。、 [DRIVER_CANCEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチン。

## <a name="ksdefaultdispatchpnp-function"></a>KsDefaultDispatchPnp 関数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_PNP) DRIVER_DISPATCH KsDefaultDispatchPnp;
```

**KsDefaultDispatchPnp**関数は、既定では、メインの PnP ディスパッチ ハンドラーは、このハンドラーに機能するデバイスのオブジェクトに関する通知を送信できます。 この関数は、以前の PnP デバイス オブジェクトにすべての通知を渡します**KsSetDevicePnpAndBaseObject**デバイス ヘッダーの使用を前提としています。 関数が IRP を渡された場合\_MN\_削除\_デバイス、デバイス オブジェクトを削除します。

**KsDefaultDispatchPnp**関数は、基になる物理デバイス オブジェクト IRP の処理の状態を返します。

**KsDefaultDispatchPnp**関数は、デバイスのヘッダーを解放して、実際のデバイス オブジェクトを削除する以外にデバイスを削除するときに必要な追加のクリーンアップがない場合に便利です。

詳細については、次を参照してください。、 [DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。


## <a name="ksdefaultdispatchpower-function"></a>KsDefaultDispatchPower 関数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_POWER) DRIVER_DISPATCH KsDefaultDispatchPower;
```

**KsDefaultDispatchPower**関数は、既定のメインの電源ディスパッチ ハンドラー。 機能のデバイス オブジェクトに関する通知は、ここに移動できます。 この関数は、以前 PnP デバイス オブジェクトにすべての通知を渡します**KsSetDevicePnpAndBaseObject**デバイスのヘッダーの使用を前提としています。

**KsDefaultDispatchPower**関数は、電源の Irp または電力 IRP の完了方法と同様に必要な追加のクリーンアップがない場合に便利です。 また既定クロック imlementation などの特定のファイル オブジェクト自体を使用して電源 Irp をアタッチする、 **KsSetPowerDispatch**、しては、このルーチンが完了する前に対処します。 この関数は、IRP を完了する前に、各 power ディスパッチ ルーチンを呼び出します。

詳細については、次を参照してください。、 [DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

## <a name="ksdefaultforwardirp-routine"></a>KsDefaultForwardIrp ルーチン

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_SYSTEM_CONTROL)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH KsDefaultForwardIrp;
```

この既定のハンドラーは、対応する物理デバイスのオブジェクトへの I/O 要求を転送するルーチンをディスパッチできます。

この既定のハンドラーは、ドライバーが IRP ある要件を満たすためにディスパッチ ルーチンの手段を提供します。\_MJ\_ \*特定の主要な関数の関数のハンドラー。

詳細については、次を参照してください。、 [DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

<a name="see-also"></a>関連項目
--------

[KsAddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksadddevice)

[KsCreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatedevice)

[KSDEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice)

[KsDispatchIrp](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdispatchirp)

[KsInitializeDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedevice)

[KsInitializeDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)

[KsAddIrpToCancelableQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksaddirptocancelablequeue)

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)

[ドライバー\_オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object)

[デバイス\_オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)

[StreamClassRegisterMinidriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisteradapter)

[HW\_初期化\_データ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)

[DriverEntry ルーチンを記述します。](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-driverentry-routine)








