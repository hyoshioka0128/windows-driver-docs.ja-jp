---
title: ストリーム ドライバーのディスパッチ ルーチンの処理
description: ドライバーのディスパッチルーチンの処理に関するガイダンスを提供します。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 69300a688cebcb5c2a21917f077247b6fb1a3da6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843357"
---
# <a name="handling-dispatch-routines-in-stream-drivers"></a>ストリーム ドライバーのディスパッチ ルーチンの処理

このトピックでは、ドライバーのディスパッチルーチンの処理に関するガイダンスを提供します。

## <a name="adddevice-routine-for-avstream-minidrivers"></a>AVStream ミニドライバーの AddDevice ルーチン

ほとんどの AVStream ミニドライバーは、独自の*AddDevice*ルーチンを提供しません。 代わりに、 [**KsAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksadddevice)を使用します。これは、 [**ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)によってインストールされる既定の*AddDevice*ハンドラーです。 それでも独自の*AddDevice*ハンドラーを提供する必要があるミニドライバーは、次のガイドラインに従う必要があります。

ドライバーが*Driverentry*で[**ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)を呼び出し、後で*AddDevice*ハンドラーを置き換える場合、ミニドライバーはこのルーチン内から[**KsAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksadddevice)を呼び出して、既定の追加処理を実行できます。

ミニドライバーは、このルーチンから[**KsCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedevice)を呼び出して、とオプションの[**KSDEVICE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)で渡すことができます。 [**Ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)が呼び出されていない場合、これは、記述子によって記述された avstream デバイスを作成する最上位レベルの呼び出しです。

ミニドライバーが独自の FDO を作成し、デバイススタックに手動でアタッチする場合は、 [**Ksinitializedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedevice)を呼び出して avstream デバイスを作成する必要があります。

ドライバーが[**Ksk デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)を提供せず、まだデバイスを作成している場合は、avstream によって既定の avstream デバイスが作成されます。 このデバイスにはフィルターファクトリが含まれておらず、ミニドライバーにディスパッチされることはありません。 ミニドライバーは、 [**KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory)を呼び出すことによって、デバイス上で[**ksk filterfactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilterfactory)構造体をインスタンス化することもできます。

独自の*AddDevice* handler をインストールするには:

```cpp
DriverObject->DriverExtension->AddDevice=MyAddDevice();
```
AVStream ミニドライバーは、クラスドライバーによって提供される既定の*AddDevice*ルーチンをオーバーライドするのではなく、 [**ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)によって提供される機能を使用することをお勧めします。

詳細については、「 [DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) callback 関数」を参照してください。

## <a name="driverentry-routine-for-stream-class-minidrivers"></a>ストリームクラスミニドライバーの DriverEntry ルーチン

**Driverentry**は、ストリームクラスミニドライバーの最初のエントリポイントです。 このルーチンは必須です。

[**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)は、必要なドライバーの初期化の大部分を実行するため、ストリームクラスミニドライバーの**driverentry**ルーチンの主要なタスクは、[**ハードウェア\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)を割り当てて入力することです。ドライバー固有の定数とエントリポイントを含む構造体。 **Driverentry**は**StreamClassRegisterMinidriver**を呼び出す必要があります。

詳細については、「 [DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) callback 関数」を参照してください。

## <a name="driverentry-function-of-avstream-minidriver-function"></a>AVStream ミニドライバー関数の DriverEntry 関数

*Driverentry*関数は、avstream ミニドライバーへの最初のエントリポイントです。

各 AVStream ミニドライバーには、読み込まれるために*Driverentry*という名前の関数が明示的に指定されている必要があります。 *Driverentry*は、i/o システムによって直接呼び出されます。 通常、 *Driverentry*は[**ksk initializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)を呼び出し、次に**ksk initializedriver**から返された値を返します。

詳細については、「 [DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) callback 関数」を参照してください。

## <a name="kscancelroutine-function"></a>KsCancelRoutine 関数

**Kscancelroutine**関数は、標準の IRP キャンセル機能を実行します。この関数は、エントリを削除してから、要求をキャンセルして完了します。 関数は、キャンセルルーチン\_PDRIVER として定義されています。 指定されていない場合は、 **Ksk Addiの Tocancelablequeue**に使用される既定の関数です。

通常、この関数は、IRP をキャンセルするときに i/o サブシステムによって呼び出されますが、\_プレゼンテーションセット要求をストリーム\_ストリームメソッドに応答して直接呼び出すことができます。 一般的なキャンセルルーチンと同様に、この関数は、関数を入力したときに i/o キャンセルスピンロックが取得されていることを想定しています。

このルーチンでは、ksk キュー\_スピンロック\_IRP\_ストレージ (Irp) が、 **Ksaddiに**指定されたリストアクセススピンロックをポイントする必要があることに注意してください。

**Kscancelroutine**を使用して、実際に IRP を完了することなく、暫定的なリスト削除処理を行うことができます。 この関数の入力時に、Irp&gt;IoStatus. Status が STATUS\_に設定されている場合、IRP は完了しません。 それ以外の場合、状態は 状態\_キャンセル に設定され、IRP は完了します。 この**Kscancelroutine**をキャンセルルーチン内で使用すると、最初のリストを実行し、ロック操作をスピンして、特定の処理と最終的な IRP 完了を実行するために、ドライバーの完了ルーチンに戻ることができます。

詳細については、「 [DRIVER_CANCEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチン」を参照してください。

## <a name="ksdefaultdispatchpnp-function"></a>KsDefaultDispatchPnp 関数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_PNP) DRIVER_DISPATCH KsDefaultDispatchPnp;
```

**KsDefaultDispatchPnp**関数は、既定の主 PnP ディスパッチハンドラーです。機能デバイスオブジェクトに関する通知は、このハンドラーに送信できます。 この関数は、すべての通知を、以前に**KsSetDevicePnpAndBaseObject**で設定された PnP デバイスオブジェクトに渡し、デバイスヘッダーの使用を前提としています。 関数に\_デバイス\_削除された IRP\_渡されると、デバイスオブジェクトが削除されます。

**KsDefaultDispatchPnp**関数は、基になる物理デバイスオブジェクトの IRP 処理の状態を返します。

**KsDefaultDispatchPnp**関数は、デバイスヘッダーを解放し、実際のデバイスオブジェクトを削除する以外に、デバイスを削除するときに余分なクリーンアップが不要な場合に便利です。

詳細については、「 [DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン」を参照してください。


## <a name="ksdefaultdispatchpower-function"></a>KsDefaultDispatchPower 関数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_POWER) DRIVER_DISPATCH KsDefaultDispatchPower;
```

**KsDefaultDispatchPower**関数は、既定のメインの電源ディスパッチハンドラーです。 機能デバイスオブジェクトに関する通知は、ここに記載されています。 この関数は、すべての通知を、以前に**KsSetDevicePnpAndBaseObject**で設定された PnP デバイスオブジェクトに渡し、デバイスヘッダーを使用することを前提としています。

**KsDefaultDispatchPower**関数は、電源 irp に余分なクリーンアップが必要ない場合、または電源 irp を完了する手段として使用する場合に便利です。 また、既定のクロック imlementation などの特定のファイルオブジェクトを、 **Ksk Setpowerdispatch**を使用して電源 irp に接続し、このルーチンによって処理が完了する前に操作することもできます。 この関数は、IRP を完了する前に各電源ディスパッチルーチンを呼び出します。

詳細については、「 [DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン」を参照してください。

## <a name="ksdefaultforwardirp-routine"></a>KsDefaultForwardIrp ルーチン

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_SYSTEM_CONTROL)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH KsDefaultForwardIrp;
```

この既定のハンドラーを使用すると、ディスパッチルーチンは、対応する物理デバイスオブジェクトに i/o 要求を転送できます。

この既定のハンドラーを使用すると、ディスパッチルーチンは、ドライバーが特定の主要な関数に対する IRP\_MJ\_\* 関数ハンドラーを持つという要件を満たすことができます。

詳細については、「 [DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン」を参照してください。

<a name="see-also"></a>関連項目
--------

[KsAddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksadddevice)

[KsCreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedevice)

[KSDEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)

[KsDispatchIrp](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdispatchirp)

[KsInitializeDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedevice)

[KsInitializeDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)

[Ksk Addiの Tocancelablequeue](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksaddirptocancelablequeue)

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)

[ドライバー\_オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)

[デバイス\_オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)

[StreamClassRegisterMinidriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)

[ハードウェア\_初期化\_データ](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)

[DriverEntry ルーチンを記述する](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-driverentry-routine)








