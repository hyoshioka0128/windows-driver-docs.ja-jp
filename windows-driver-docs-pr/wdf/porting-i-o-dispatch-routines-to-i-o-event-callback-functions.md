---
title: I/O ディスパッチ ルーチンの I/O イベント コールバック関数への移植
description: I/O ディスパッチ ルーチンの I/O イベント コールバック関数への移植
ms.assetid: 0BD65185-C358-4E28-8E31-255AF8D77F93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab11ee720dae3b4eaef1b74a99848092dc871d7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379640"
---
# <a name="porting-io-dispatch-routines-to-io-event-callback-functions"></a>I/O ディスパッチ ルーチンの I/O イベント コールバック関数への移植


WDM ドライバーの I/O のディスパッチ ルーチンの中核は、WDF ドライバーの I/O イベント コールバック関数にマップされます。 ただし、I/O イベントのコールバック関数は、WDM ドライバーの I/O のディスパッチ ルーチンからいくつかの重要な点で異なります。

-   フレームワークが WDF ドライバーの I/O イベント コールバックを呼び出すと、コールバックは、オブジェクトの状態で要求を受け取ります。 ドライバーに明示的にマークを付けますとしてキャンセル可能な限り、要求をキャンセルできません。
-   ドライバーでは、キューごとまたはデバイスのオブジェクトごとに、このような 1 つだけのコールバックが同時に実行されるように、フレームワークが I/O イベントのコールバックの呼び出しを同期するかどうか、またはかどうか、フレームワークが適用されない同期ですべてを指定します。 同期オプションを選択する方法についての詳細については、次を参照してください。[を使用して自動同期](using-automatic-synchronization.md)します。

これらの違いにより、ほとんどの I/O イベント コールバック関数がアクセスを同期して、対応する WDM よりも、競合状態を防ぐためには、大幅に少ないコードを含む**DispatchXxx**ルーチン。

別に、同期は、WDM ドライバーの I/O の主な違いは、ルーチン、WDF ドライバーの I/O のイベント コールバック関数には、ドライバーがパラメーターを取得する方法と、I/O バッファーにアクセスする方法をディスパッチします。

## <a name="parameters-for-io-requests"></a>I/O 要求のパラメーター


WDF のドライバーを処理し、I/O キューを構成する方法、ドライバーは必要ないかもしれません WDM ドライバーとして、I/O 要求のパラメーターを解析することを要求の種類によっては。 フレームワークが I/O イベントのコールバックを呼び出すときに要求を読み取り、書き込み、およびデバイスの I/O コントロール ([*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)、 [ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)、[ *EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)、 [ *EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control))、最もよく使用されるパラメーターを抽出しますIRP のコールバックにパラメーターとして渡します。 たとえば、フレームワークがドライバーの*EvtIoRead* WDFREQUEST オブジェクトと、読み取るバイト数へのハンドルをコールバックします。 ドライバーにデバイスのオフセットまたは並べ替えキーが不要な場合だけを取得できる、バッファー WDFREQUEST オブジェクトからの 1 つを呼び出すことによって、 **WdfRequestRetrieveOutputXxx**メソッドです。 追加のパラメーターを取得する必要はありません。

**EvtIoDefault**コールバック、ただし、フレームワークに渡しますハンドルのみに、キューおよび要求オブジェクトを識別するハンドル。 その結果、ドライバーを呼び出す必要があります**WdfRequestGetParameters**要求の種類を含む、パラメーターを取得する (**WdfRequestTypeXxx**)。 [**WdfRequestGetParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)を返します、 [ **WDF\_要求\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_parameters)で渡されたパラメーターを格納する構造体、作成、読み取り、書き込み、デバイスの I/O 制御、または内部デバイス I/O 制御要求。

## <a name="access-to-buffers-for-buffered-and-direct-io"></a>バッファーとダイレクト I/O バッファーへのアクセス


フレームワークは、i/o 要求を受信したときに、基になる WDM IRP をカプセル化する WDFREQUEST オブジェクトを作成します。 WDFREQUEST オブジェクトをキューにし、最終的に、ドライバーのに従ってディスパッチ[仕様をディスパッチ](dispatching-methods-for-i-o-requests.md)キュー。 ドライバーでは、WDF メソッドを使用して、パラメーターと、I/O 要求のバッファーを取得します。 ドライバーは、いつでも基になる WDM IRP を呼び出すことで取得できます[ **WdfRequestWdmGetIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)します。

WDM ドライバーと同様に WDF のドライバーがサポートできる[バッファー、直接、またはどちらも I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)します。 ドライバーを呼び出すことで各デバイス オブジェクトはサポートされている I/O の種類を設定する[ **WdfDeviceInitSetIoType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)で、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)デバイス オブジェクトを作成する前にコールバックします。 WDM ドライバーとは異なり、KMDF ドライバーにアクセス バッファーと同じ方法でバッファリングまたはダイレクト I/O を実行してごとに、同じメソッドを使用しているかどうか。

WDF ドライバーは、同じ方法でバッファーをバッファーとダイレクトの両方の I/O のアクセス、ですが、I/O 要求の種類に応じて、バッファーを取得するのにさまざまな方法を使用します。 次のセクションでは、ドライバーが I/O 要求の種類ごとに処理する方法について説明します。

-   [要求を作成します。](#create-requests)
-   [読み取り要求](#read-requests)
-   [書き込み要求](#write-requests)
-   [デバイス I/O 制御要求](#device-io-control-requests)
-   [内部デバイス I/O 制御要求](#internal-device-io-control-requests)

## <a name="create-requests"></a>要求を作成します。


WDF のドライバーが処理できる要求の作成 ([**IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)) 2 つの方法のいずれかで。

-   キューをバイパスし、代わりに指定する[ *EvtDeviceFileCreate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック。
-   フレームワークのキューの要求を作成し、実装がある、 [ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)キューからこのような要求を処理するためにコールバックします。

ファイルの作成要求の処理の詳細については、次を参照してください。 [Framework ファイル オブジェクト](framework-file-objects.md#creating-or-opening-a-file)します。

## <a name="read-requests"></a>読み取り要求


読み取り要求のためのバッファーを取得する ([**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read))、WDF ドライバーでは、1 つを呼び出す、 **WdfRequestRetrieveOutputXxx**メソッド。 ドライバーが実行するかどうかに依存しているは、これらのメソッドを返します。 各バッファー[バッファー、直接、またはどちらも I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。

バッファー ポインターの WDM 対応については、次を参照してください。 [KMDF バッファー ポインターの対応する WDM](wdm-equivalents-for-kmdf-buffer-pointers.md#read)します。

## <a name="write-requests"></a>書き込み要求


書き込み要求のためのバッファーを取得する ([**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write))、WDF ドライバーでは、1 つを呼び出す、 **WdfRequestRetrieveInputXxx**メソッド。 ドライバーが実行するかどうかに依存しているは、これらのメソッドを返します。 各バッファー[バッファー、直接、またはどちらも I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。

バッファー ポインターの WDM 対応については、次を参照してください。 [KMDF バッファー ポインターの対応する WDM](wdm-equivalents-for-kmdf-buffer-pointers.md#write)します。

## <a name="device-io-control-requests"></a>デバイス I/O 制御要求


デバイス I/O 制御要求を処理する ([**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control))、WDF ドライバーでは、いずれかを呼び出す**WdfRequestRetrieveInputXxx**メソッドまたは**WdfRequestRetrieveOutputXxx**バッファーのバッファーを取得し、ダイレクト I/O メソッド。 対応する入力と出力のメソッドは、ドライバーは、いずれかを使用できるように、同じバッファーを返します。 ドライバーが実行するかどうかに依存しているは、これらのメソッドを返します。 各バッファー[バッファー、直接、またはどちらも I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)、だけでは、読み取りおよび書き込み要求。

ドライバーが別のデバイス スタックかを使用して送信されるデバイス I/O 制御要求を処理する場合、 **Parameters.Other**フィールド、ドライバーが呼び出す必要があります[ **WdfRequestGetParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)呼び出す代わりにバッファーへのポインターを取得する[ **WdfRequestRetrieveInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)と[ **WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer). これらの要求のソースは、カーネル モード コンポーネントである保証は、ため、ドライバーは、返されたバッファー ポインターを信頼できます。 ただし、バッファー長、およびその他のパラメーターを検証にする必要がありますも。

バッファー ポインターの WDM 対応については、次を参照してください。 [KMDF バッファー ポインターの対応する WDM](wdm-equivalents-for-kmdf-buffer-pointers.md#device-control)します。

## <a name="internal-device-io-control-requests"></a>内部デバイス I/O 制御要求


内部デバイス I/O 制御要求 ([**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)) カーネル モード コンポーネントによってのみを発行し、要求のブロックを渡すためにいくつかのオペレーティング システム コンポーネントによって内部的に使用 (SCSI など xRB プロトコル要求ブロック\[される Srb\]またはユニバーサル要求ブロック\[翻訳\])。 さまざまな種類のバッファーには、このような要求を伴うことができます。

取得して、内部デバイス I/O 制御要求のパラメーターの解釈は、問題が発生することができます。 このような一部の要求の長さを渡すために、問題が発生、 **InputBufferLength**と**OutputBufferLength**のフィールド、 **Parameters.DeviceIoControl**WDM IRP がいくつかの構造は必要ありません。 それにもかかわらず、フレームワークをどのような値は、抽出、 **InputBufferLength**と**OutputBufferLength**フィールドし、パラメーターとして渡し、 [ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)コールバック。 これらの値でも、内部の検証も行われません。

バッファーを取得するには、ドライバーを呼び出す次のいずれかの。

-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)、返された、 **Parameters.DeviceIoControl.Type3InputBuffer** IRP のフィールド。
-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)、返された、 **UserBuffer** IRP のフィールド。

 

 





