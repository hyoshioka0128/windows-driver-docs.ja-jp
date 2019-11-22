---
title: I/O ディスパッチ ルーチンの I/O イベント コールバック関数への移植
description: I/O ディスパッチ ルーチンの I/O イベント コールバック関数への移植
ms.assetid: 0BD65185-C358-4E28-8E31-255AF8D77F93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e338a030a167b9dcc89cb41806fb909392bf9774
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845209"
---
# <a name="porting-io-dispatch-routines-to-io-event-callback-functions"></a>I/O ディスパッチ ルーチンの I/O イベント コールバック関数への移植


WDM ドライバーの i/o ディスパッチルーチンのコアは、WDF ドライバーの i/o イベントコールバック関数に対応しています。 ただし、i/o イベントのコールバック関数は、WDM ドライバーの i/o ディスパッチルーチンのいくつかの重要な点で異なります。

-   フレームワークが WDF ドライバーの i/o イベントコールバックを呼び出すと、コールバックはキャンセル不可能な状態で要求を受信します。 ドライバーが明示的に取り消し可能としてマークしない限り、要求を取り消すことはできません。
-   ドライバーは、このようなコールバックが1つのキューまたは各デバイスオブジェクトに対して同時に実行されるように、または、フレームワークがまったく同期を適用しないように、i/o イベントコールバックへの呼び出しを同期するかどうかを指定します。 同期オプションの選択の詳細については、「[自動同期の使用](using-automatic-synchronization.md)」を参照してください。

これらの違いは、ほとんどの i/o イベントコールバック関数は、アクセスを同期し、対応する WDM **DispatchXxx**ルーチンと競合状態を防ぐために、はるかに少ないコードを含むことを意味します。

同期とは別に、WDM ドライバーの i/o ディスパッチルーチンと WDF ドライバーの i/o イベントコールバック関数の主な違いは、ドライバーがパラメーターを取得する方法と、それが i/o バッファーにアクセスする方法にあります。

## <a name="parameters-for-io-requests"></a>I/o 要求のパラメーター


WDF ドライバーによって処理される要求の種類や、i/o キューの構成方法によっては、WDM ドライバーと同様に i/o 要求に対してパラメーターを解析する必要がない場合があります。 フレームワークが読み取り、書き込み、デバイス i/o 制御要求 ([*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)、 [*evtiowrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)、 [*evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)、 [*evtiointernaldevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)) の i/o イベントコールバックを呼び出すと、最も一般的に使用されるIRP からパラメーターを渡し、コールバックにパラメーターとして渡します。 たとえば、フレームワークは、WDFREQUEST オブジェクトをハンドルし、読み取るバイト数を指定して、ドライバーの*EvtIoRead*コールバックを呼び出します。 ドライバーがデバイスオフセットまたは並べ替えキーを必要としない場合は、 **WdfRequestRetrieveOutputXxx**メソッドのいずれかを呼び出すことによって、単に WDFREQUEST オブジェクトからバッファーを取得できます。追加のパラメーターを取得する必要はありません。

ただし、 **Evtiodefault**コールバックでは、フレームワークはキューへのハンドルと要求オブジェクトへのハンドルのみを渡します。 そのため、ドライバーは、要求の種類 (**Wdfrequesttypexxx**) を含むパラメーターを取得するために、 **Wdfrequestgetparameters**を呼び出す必要があります。 [**Wdfrequestgetparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)は、作成、読み取り、書き込み、デバイス i/o 制御、または内部デバイス i/o 制御要求で渡されたパラメーターを含む[**WDF\_要求\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_parameters)構造体を返します。

## <a name="access-to-buffers-for-buffered-and-direct-io"></a>バッファーへのアクセスと直接 i/o


フレームワークは、i/o の要求を受信すると、基になる WDM IRP をカプセル化する WDFREQUEST オブジェクトを作成します。 次に、WDFREQUEST オブジェクトをキューに置いて、最終的にキューのドライバーの[ディスパッチ仕様](dispatching-methods-for-i-o-requests.md)に従ってディスパッチします。 ドライバーは、WDF メソッドを使用して、i/o 要求のパラメーターとバッファーを取得します。 ドライバーは、 [**Wdfrequestwdmgetirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)を呼び出すことにより、基になる WDM IRP をいつでも取得できます。

WDM ドライバーと同様に、WDF ドライバーで[は、バッファー、直接、またはその両方](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)の i/o をサポートできます。 ドライバーは、デバイスオブジェクトを作成する前に、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックで[**Wdfdeviceinitsetiotype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)を呼び出して、各デバイスオブジェクトでサポートされている i/o の種類を設定します。 ただし、WDM ドライバーとは異なり、KMDF ドライバーはバッファーにアクセスするのと同じ方法でバッファーまたは直接 i/o を実行し、それぞれに同じメソッドを使用します。

WDF ドライバーはバッファーにアクセスするのと同じ方法でバッファーにアクセスしますが、i/o 要求の種類に応じて、さまざまな方法でバッファーを取得します。 次のセクションでは、ドライバーが各種類の i/o 要求を処理する方法について説明します。

-   [要求の作成](#create-requests)
-   [読み取り要求](#read-requests)
-   [書き込み要求](#write-requests)
-   [デバイス i/o 制御要求](#device-io-control-requests)
-   [内部デバイス i/o 制御要求](#internal-device-io-control-requests)

## <a name="create-requests"></a>要求の作成


WDF ドライバーでは、次の2つの方法のいずれかで作成要求 ([**IRP\_MJ\_create**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)) を処理できます。

-   キューをバイパスし、代わりに[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバックを指定します。
-   フレームワークキューの作成要求を取得し、そのような要求をキューから処理するための[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバックを実装します。

ファイル作成要求の処理の詳細については、「[フレームワークファイルオブジェクト](framework-file-objects.md#creating-or-opening-a-file)」を参照してください。

## <a name="read-requests"></a>読み取り要求


読み取り要求 ([**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)) 用のバッファーを取得するために、WDF ドライバーはいずれかの**WdfRequestRetrieveOutputXxx**メソッドを呼び出します。 これらの各メソッドが返すバッファーは、ドライバーがバッファリングされているか、[直接の i/o か、またはどちら](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)の i/o も実行していないかによって異なります。

バッファーポインターに相当する WDM の詳細については、「 [KMDF バッファーポインターに対応する wdm](wdm-equivalents-for-kmdf-buffer-pointers.md#read)」を参照してください。

## <a name="write-requests"></a>書き込み要求


書き込み要求 ([**IRP\_MJ\_write**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)) のバッファーを取得するために、WDF ドライバーはいずれかの**WdfRequestRetrieveInputXxx**メソッドを呼び出します。 これらの各メソッドが返すバッファーは、ドライバーがバッファリングされているか、[直接の i/o か、またはどちら](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)の i/o も実行していないかによって異なります。

バッファーポインターに相当する WDM の詳細については、「 [KMDF バッファーポインターに対応する wdm](wdm-equivalents-for-kmdf-buffer-pointers.md#write)」を参照してください。

## <a name="device-io-control-requests"></a>デバイス i/o 制御要求


デバイス i/o 制御要求 ([**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)) を処理するために、WDF ドライバーは、バッファーのバッファーを取得するために**WdfRequestRetrieveInputXxx**メソッドまたは**WdfRequestRetrieveOutputXxx**メソッドのいずれかを呼び出します。ダイレクト i/o。 対応する入力メソッドと出力メソッドは同じバッファーを返すので、ドライバーはいずれかを使用できます。 これらの各メソッドが返すバッファーは、ドライバーが読み取り要求と書き込み要求の場合と同様に、バッファリングされている[、直接の i/o、またはどちらでも](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)ない i/o を実行するかどうかによって異なります。

別のデバイススタックで発生したデバイス i/o 制御要求をドライバーが処理する場合、または**パラメーター**を使用する場合、ドライバーは[**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)と[**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)を呼び出す代わりに、 [**wdfrequestgetparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)を呼び出してバッファーポインターを取得する必要があります。 これらの要求のソースはカーネルモードのコンポーネントであることが保証されるため、ドライバーは返されたバッファーポインターを信頼できます。 ただし、バッファーの長さとその他のパラメーターも検証する必要があります。

バッファーポインターに相当する WDM の詳細については、「 [KMDF バッファーポインターに対応する wdm](wdm-equivalents-for-kmdf-buffer-pointers.md#device-control)」を参照してください。

## <a name="internal-device-io-control-requests"></a>内部デバイス i/o 制御要求


内部デバイス i/o 制御要求 ([**IRP\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)) は、カーネルモードコンポーネントによってのみ発行され、一部のオペレーティングシステムコンポーネントによって内部的に使用され、要求ブロック (xrb プロトコル) を通過します。SCSI 要求ブロック \[SRBs\] またはユニバーサル要求ブロック \[URBs\]) などです。 このような要求には、多くの異なる種類のバッファーが付属しています。

内部デバイス i/o 制御要求のパラメーターを取得および解釈すると、問題が発生する可能性があります。 この問題が発生するのは、このような要求の中に、WDM IRP の**DeviceIoControl**構造体にある**inputbufferlength**フィールドと**outputbufferlength**フィールドの長さが渡されるものがあります。 それにもかかわらず、 **inputbufferlength**フィールドと**outputbufferlength**フィールドにある値を抽出し、それらをパラメーターとして[*Evtiointernaldevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)コールバックに渡します。 これらの値に対して内部検証を実行しません。

バッファー自体を取得するために、ドライバーは次のいずれかのメソッドを呼び出します。

-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)。 IRP の**DeviceIoControl. Type3InputBuffer**フィールドを返します。
-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)。 IRP の**UserBuffer**フィールドを返します。

 

 





