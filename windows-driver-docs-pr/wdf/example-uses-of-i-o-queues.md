---
title: I/O キューの使用例
description: I/O キューの使用例
ms.assetid: 13b09254-ce0a-4c7d-bdb1-d28ec094a266
keywords:
- I/o キュー WDK KMDF、例
- 要求ハンドラー WDK KMDF
- 既定の i/o キュー WDK KMDF
- 単一 i/o キュー WDK KMDF
- 複数の i/o キュー (WDK KMDF)
- 並列 i/o キュー WDK KMDF
- 順次 i/o キュー WDK KMDF
- 手動 i/o キュー WDK KMDF
- I/o キュー WDK KMDF、ディスパッチメソッド
- メソッドのディスパッチ (WDK KMDF)
- シーケンシャルディスパッチ WDK KMDF
- WDK KMDF の同期ディスパッチ
- WDK KMDF の並列ディスパッチ
- WDK KMDF の非同期ディスパッチ
- WDK KMDF の手動によるディスパッチ
- WdfIoQueueDispatchParallel
- WdfIoQueueDispatchSequential
- WdfIoQueueDispatchManual
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34c9f4be46d24a8baf6cf218f526ad7cc23e8b7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843187"
---
# <a name="example-uses-of-io-queues"></a>I/O キューの使用例





システムに接続され、特定のドライバーでサポートされているデバイスごとに、ドライバーは次の i/o キューと[要求ハンドラー](request-handlers.md)の組み合わせを使用できます。

-   1つの既定の i/o キューと1つの要求ハンドラー ( [*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default))。 フレームワークは、デバイスのすべての要求を既定のキューに配信し、ドライバーの*Evtiodefault*ハンドラーを呼び出して、ドライバーに各要求を配信します。

-   単一の既定の i/o キューと、 [*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)、 [*evtiowrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)、 [*evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)などの複数の要求ハンドラー。 フレームワークは、すべてのデバイスの要求を既定のキューに配信します。 このメソッドは、ドライバーの*EvtIoRead*ハンドラーを呼び出して、読み取り要求、書き込み要求を配信するための*Evtiowrite*ハンドラー、およびデバイスの i/o 制御要求を配信するための*evtiodevicecontrol*ハンドラーを呼び出します。

-   複数の i/o キュー (読み取り要求用および書き込み要求用に1つなど)。 キューは1種類の要求のみを受信するため、各キューについては、ドライバーが提供する要求ハンドラーは1つだけです。

-   複数の i/o キュー。それぞれに複数の要求ハンドラーがあります。

シナリオの例を次に示します。

-   [単一の順次 i/o キュー](#a-single-sequential-io-queue)

-   [複数の順次 i/o キューと手動キュー](#multiple-sequential-io-queues-and-a-manual-queue)

-   [単一の並列 i/o キュー](#a-single-parallel-io-queue)

-   [複数の並列 i/o キュー](#multiple-parallel-io-queues)

## <a name="a-single-sequential-io-queue"></a>単一の順次 i/o キュー

読み取り要求と書き込み要求を同時に処理できるディスクドライブ用の関数ドライバーを一度に1つずつ作成する場合、関数ドライバーはデバイスごとに1つの i/o キューしか必要としません。

ドライバーは、ドライバーが[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出したときに、フレームワークによって作成される既定の i/o キューを使用できます。また、キューの[**WDF\_IO\_queue\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体で**defaultqueue**を**TRUE**に設定します。 WDF\_IO\_QUEUE\_CONFIG 構造体では、ドライバーは次の項目も指定する必要があります。

-   **WdfIoQueueDispatchSequential**はディスパッチ方法として、既定の i/o キューはドライバーに i/o 要求を同期的に配信します。

-   すべての i/o 要求を受信する、1つのイベントコールバック関数[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)。

ドライバーの既定の i/o キューで i/o 要求を使用できるようになるたびに、フレームワークはドライバーの[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)要求ハンドラーを呼び出すことによって、ドライバーに要求を配信します。 キューで別の要求を使用できるようになった場合、以前に配信された要求に対してドライバーが[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出すまで、フレームワークはそれを提供しません。

## <a name="multiple-sequential-io-queues-and-a-manual-queue"></a>複数の順次 i/o キューと手動キュー

次の特性を持つシリアルポートデバイスを考えてみましょう。

-   1回の読み取り操作と1回の書き込み操作を同時に実行できます。

-   複数の読み取りまたは書き込み操作を非同期に実行することはできません。

-   デバイスの i/o 制御要求を受信して、状態情報を取得できます。 デバイスのドライバーは、これらの要求の一部 (状態の変更を待機する要求など) の実行に時間がかかることがあります。

このデバイスの関数ドライバーは、デバイスごとに複数の順次 i/o キューを使用する可能性があります。 このドライバーは、 [**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を3回呼び出します。1回は既定のキューを作成し、2回は2つの追加の i/o キューを作成します。 これらの各キューの[**WDF\_IO\_QUEUE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体で、ドライバーは次を指定する必要があります。

-   **WdfIoQueueDispatchSequential**は、各キューのディスパッチメソッドとして、フレームワークが i/o 要求をドライバーに同期的に配信するようにします。

-   キューごとに異なる[要求ハンドラー](request-handlers.md) ([*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)、 [*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)、および[*evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write))。これは、キューの i/o 要求を受け取ります。

[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出すと、ドライバーは[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を2回呼び出して、すべての読み取り要求を追加キューに転送し、すべての書き込み要求を他のキューに転送できます。

この構成では、デバイスの既定の i/o キュー [*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数は、状態情報に関するデバイス i/o 制御要求のみを受信します。

ドライバーがステータス要求を長時間保持する必要がある場合は、4つ目のキューを作成し、ディスパッチ方法として**WdfIoQueueDispatchManual**を指定できます。 ドライバーは、待機する必要がある情報の要求を受信すると、状態情報が使用可能になるまで、この追加のキューに要求を配置できます。 次に、ドライバーがキューから要求を取得して完了することができます。 それまでの間、既定のキューはドライバーに別の要求を配信できます。

## <a name="a-single-parallel-io-queue"></a>単一の並列 i/o キュー

IDE ディスクコントローラーは、一部の i/o 操作と重複することはできません。 たとえば、コントローラーが1つのディスクで読み取りまたは書き込み操作を処理している間に、別のディスクにシークコマンドを送信できます。 一方、複数の同時読み取りおよび書き込みコマンドはサポートされていません。

このコントローラーの関数ドライバーは、各 i/o 要求を確認する必要があります。 ドライバーが seek コマンドを受け取る場合は、シークコマンドを処理できるかどうかを判断する必要があります。 次の場合、seek コマンドは処理できません。

-   指定されたディスクドライブは既にビジーです。

-   ディスクドライブがフォーマットされているため、他のドライブをアクティブにすることはできません。

コントローラーに接続されているデバイスごとに、ドライバーは[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して既定の i/o キューを作成できます。 これらの各キューの[**WDF\_IO\_QUEUE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体で、ドライバーは次を指定する必要があります。

-   **WdfIoQueueDispatchParallel**は、各キューのディスパッチメソッドとして、フレームワークが i/o 要求をドライバーに非同期的に配信するようにします。

-   各キューの[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)イベントコールバック関数。これにより、キューの i/o 要求が受信されます。

この構成では、1つの並列 i/o キューが各デバイスに割り当てられます。 ドライバーは、各 i/o キューからフレームワークが提供する各 i/o 要求を確認する必要があります。 ドライバーが要求をすぐに処理できる場合は、それが実行されます。 それ以外の場合、ドライバーは[**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)を呼び出します。これにより、ドライバーが[**Wdfioqueuestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)を呼び出すまで、フレームワークは要求の配信を停止します。

## <a name="multiple-parallel-io-queues"></a>複数の並列 i/o キュー

SCSI ホストアダプターは、非同期の重複 i/o 操作をサポートするデバイスの一例です。 最大32のデバイスをアダプターに接続できます。 次の構成のシステムを考えてみましょう。

-   SCSI アダプターに接続されているデバイスの中には、"reselection" をサポートしているものと、そうでないものがあります。 SCSI デバイスが reselection をサポートしている場合、i/o 操作中に、デバイスは、アダプターが別のデバイスにサービスを実行できるように、アダプターを一時的に解放できます。 最初のデバイスは、後でそれ自体を再選択して操作を完了します。

-   SCSI アダプターは、ハードウェアメールボックスを使用して、ドライバーとデバイス間で要求と応答を渡します。 デバイスが要求の準備ができていても、使用可能なメールボックスがない場合、デバイスは待機する必要があります。

最適なパフォーマンスを得るために、この SCSI ホストアダプターの関数ドライバーは、使用可能になるとすぐに、フレームワークから i/o 要求を受信する必要があります。 ドライバーは、各要求を調べて、すぐに開始できるかどうか、またデバイスとリソース (メールボックスメモリなど) が使用可能になるまで延期する必要があるかどうかを判断する必要があります。

ドライバーでは、複数の並列 i/o キューを使用することをお勧めします。 アダプターに接続されているデバイスごとに、ドライバーは[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して既定の i/o キューを作成します。 これらの各キューの[**WDF\_IO\_QUEUE\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体で、ドライバーは次を指定する必要があります。

-   **WdfIoQueueDispatchParallel**は、各キューのディスパッチメソッドとして、フレームワークが i/o 要求をドライバーに非同期的に配信するようにします。

-   各キューの[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)イベントコールバック関数。これにより、キューの i/o 要求が受信されます。

各 i/o キューの[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数は、キューの i/o 要求を配信されているかどうかを調べ、それぞれをすぐに処理できるかどうかを判断する必要があります。 デバイスとシステムリソースが使用可能な場合、ドライバーは i/o 操作を開始します。 デバイスまたはリソースを使用できない場合、ドライバーは[**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)を呼び出して、現在の要求を処理できるようになるまで追加の要求の配信を停止する必要があります。

必要に応じて、ドライバーは[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して、デバイスごとに追加のキューを作成できます。 次に、ドライバーは[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)を呼び出して、追加のキューに対していくつかの種類の要求をキューへできます。 フレームワークが追加のキューから要求を配信する場合、ドライバーは、必要に応じて、既定のキューではなく、そのキューで[**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)を呼び出すことができます。これにより、配信が延期される要求の数や種類を最小限に抑えることができます。

 

 





