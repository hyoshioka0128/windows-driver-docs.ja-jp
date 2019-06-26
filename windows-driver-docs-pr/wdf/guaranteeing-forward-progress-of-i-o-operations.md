---
title: I/O 操作の前方進行の保証
description: I/O 操作の前方進行の保証
ms.assetid: e230eb3b-54ac-43b1-ac2b-8fa137cee43e
keywords:
- 保証された進行 WDK KMDF
- WDK KMDF の保証の進行状況を転送します。
- メモリ不足状況 WDK KMDF
- I/O キュー WDK KMDF、進行の保証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a14ea003fbd2bc4235983bd7d9a445667204eb4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382853"
---
# <a name="guaranteeing-forward-progress-of-io-operations"></a>I/O 操作の前方進行の保証


システムのページングのデバイスの記憶装置ドライバーなど、一部のドライバーを実行する必要があります、少なくとも一部の重要なシステムのデータの損失を回避するために、問題なくサポートされている I/O 操作。 ドライバーの障害の潜在的な原因の 1 つは、メモリ不足状況です。 フレームワークまたはドライバーには、I/O 要求を処理するために十分なメモリを割り当てることができません場合、いずれか 1 つは、によって I/O 要求が失敗する必要があります[完了](completing-i-o-requests.md)エラー状態の値を使用します。

バージョン 1.9 より前のバージョン KMDF のフレームワークでは、I/O マネージャーがドライバーに送信 I/O 要求パケット (IRP) のフレームワークの要求オブジェクトを割り当てることができない場合、I/O 要求が常に失敗します。 バージョン 1.9 以降のフレームワークを提供するドライバーのメモリ不足の状況での I/O 要求を処理する機能を提供するには*進行を保証*の I/O キューの機能です。

この機能により、フレームワークはし、事前のメモリを割り当て、ドライバーがそれぞれの要求オブジェクトと、ドライバーの要求に関連するコンテキスト バッファーを設定します。 フレームワークとドライバーは、システム メモリの量が少ないときにのみ、メモリを事前に割り当てられたこれを使用します。

### <a name="features-of-guaranteed-forward-progress"></a>保証された処理を進行の機能

フレームワークの進行の保証の I/O キューを使用して、ドライバーでは次のことができます。

-   メモリ不足の状況の中に特定の I/O キューを使用する要求オブジェクトのセットを事前に割り当てるために、フレームワークに問い合わせてください。

-   メモリ不足の状況の中に、framework から事前に割り当てられた要求オブジェクトを受信すると、ドライバーが使用できる要求に固有のリソースを事前に コールバック関数を提供します。

-   ドライバー固有のリソースを割り当てる、I/O 要求のメモリ不足の状況がもう 1 つのコールバック関数を用意*いない*されてが検出されました。 このコールバック関数の割り当ては、メモリ不足状態のため失敗した場合、フレームワークがその要求を事前に割り当てられたオブジェクトのいずれかを使用する必要があるかどうかを示している可能性があります。

-   事前に割り当てられた要求オブジェクトを使用する必要する I/O 要求を指定します。 事前に割り当てられたオブジェクトを使用して、ページング I/O 操作が進行中、または事前に割り当てられたオブジェクトを使用するかどうかを判断するには、各 IRP を調べて、コールバック関数が追加のドライバーを持つ場合にのみ、それらを使用して、すべての Irp のオプションが含まれます。

ドライバーの実装が保証される場合進行の I/O キューの 1 つ以上のドライバーは改善されますことができない正常[I/O 要求を処理](processing-i-o-requests.md)メモリ不足の状況の中にします。 デバイスの既定の I/O キューの保証された処理を進行を実装して、ドライバーを呼び出すことによって構成のすべての I/O キューを[ **WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)します。

フレームワークは、ドライバーとドライバーの両方に、進行の機能が、ドライバーの機能を保証の[I/O ターゲット](using-i-o-targets.md)実装は、進行を保証します。 つまり、ドライバーは、デバイスの保証された処理を進行を実装する場合でも、デバイスのドライバー スタックのすべての下位レベルのドライバー保証された処理を進行する必要がありますも実装します。

### <a name="enabling-guaranteed-forward-progress-for-an-io-queue"></a>転送の進行状況を I/O キューの保証を有効にします。

I/O キューの保証された処理を進行を有効にするには、ドライバーを初期化します、 [ **WDF\_IO\_キュー\_フォワード\_進行状況\_ポリシー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)構造体に呼び出し、 [ **WdfIoQueueAssignForwardProgressPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)メソッド。 ドライバーを呼び出す場合[ **WdfDeviceConfigureRequestDispatching** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)で、I/O キューを構成するが行う必要がありますを呼び出す前に**WdfIoQueueAssignForwardProgressPolicy**します。

ドライバーを呼び出すと[ **WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)、省略可能なすべての次の 3 つのイベント コールバック関数を指定できます。

<a href="" id="evtioallocateresourcesforreservedrequest"></a>[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)  
ドライバーの[ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数の割り当てし、メモリ不足のために、フレームワークを予約する要求オブジェクトの要求に固有のリソースを格納場合。

フレームワークでは、予約済みの要求オブジェクトを作成するたびにこのコールバック関数を呼び出します。 ドライバー割り当てる必要があります要求に固有のリソース、1 つの I/O 要求の通常の予約済みの要求オブジェクトを使用して[コンテキスト領域](framework-object-context-space.md)します。

<a href="" id="evtioallocaterequestresources"></a>[*EvtIoAllocateRequestResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)  
ドライバーの[ *EvtIoAllocateRequestResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数はすぐに使用を要求に固有のリソースを割り当てます。 フレームワークが IRP を受信し、IRP の要求オブジェクトを作成した直後に呼び出されます。

コールバック関数のリソースを割り当てようとして失敗した場合、コールバック関数は、エラー状態の値を返します。 フレームワークは、新しく作成された要求オブジェクトを削除し、その予約済みの要求オブジェクトの 1 つを使用します。 さらに、ドライバーの[要求ハンドラー](request-handlers.md)要求に固有のリソースを使用するその[ *EvtIoAllocateRequestResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)以前割り当てられ、コールバック関数。

<a href="" id="evtiowdmirpforforwardprogress"></a>[*EvtIoWdmIrpForForwardProgress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)  
ドライバーの[ *EvtIoWdmIrpForForwardProgress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)コールバック関数が IRP を検査し、フレームワークでを実行して、I/O 要求は失敗するか IRP の予約済みの要求オブジェクトを使用するかどうかを指示します。エラー状態の値。

フレームワークは、新しい要求オブジェクトを作成することがあり、指定した場合にのみ、フレームワークはこのコールバック関数を呼び出します (ドライバーのフラグを設定して[ **WDF\_IO\_キュー\_フォワード\_進行状況\_ポリシー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)構造)、メモリ不足の状況の中に Irp を調査するドライバーをします。 つまり、ドライバーは各 IRP を評価し、いずれかのメモリ不足の状況が発生しても処理する必要があるかを決定できます。

ドライバーを呼び出すと[ **WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)、メモリ不足の状況を事前割り当てするためにフレームワークをするオブジェクトの予約済みの要求の数も指定します。 デバイスとドライバーの適切な要求オブジェクトの数を選択することができます。 パフォーマンスの低下を防ぐためには、ドライバーは通常、ドライバーとデバイスが並列で処理できる I/O 要求の数を概算する番号を指定する必要があります。

ただし場合、に、ドライバーの呼び出し[ **WdfIoQueueAssignForwardProgressPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)とその[ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数は、事前要求の予約済みのオブジェクトが多すぎるまたは要求固有のリソースのメモリが多すぎるに割り当ててには、ドライバーは処理しようとしているメモリ不足の状況に実際に投稿できます。 ドライバーとデバイスのパフォーマンスをテストしを選択する最適な数を決定する、メモリ不足のシミュレーションを含める必要があります。

前に[ **WdfIoQueueAssignForwardProgressPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)フレームワークを作成し、予約、ドライバーが指定された要求オブジェクトの数を返します。 その it 要求オブジェクトを予約するたびに、ドライバーのすぐにフレームワーク[ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数のドライバーを割り当てるして保存できるように要求に固有のリソース、フレームワークの場合も実際にオブジェクトを使用して、予約済みの要求。

ときに、ドライバーのいずれかの[要求ハンドラー](request-handlers.md) I/O 要求の受信 I/O キューから呼び出すことができます、 [ **WdfRequestIsReserved** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestisreserved)判断するメソッドかどうか、要求オブジェクトは、いずれかのフレームワークに割り当て済みメモリ不足の状況です。 このメソッドが戻る場合**TRUE**、ドライバーは、リソースを使用する必要がありますをその[ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数が予約されています。

フレームワークは、その予約済みの要求オブジェクトのいずれかを使用している場合オブジェクトを返します、予約済みのオブジェクトのセットをドライバーが要求を完了後します。 フレームワークは、要求オブジェクトと、ドライバーを呼び出すことによって作成されるコンテキストの領域を保存します[ **WdfDeviceInitSetRequestAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)または[  **。WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectallocatecontext)、別のメモリ不足の状況が発生した場合に再利用できるようにします。

### <a name="how-the-framework-and-driver-support-guaranteed-forward-progress"></a>フレームワークとドライバーが保証された処理を進行をサポートする方法

I/O キューの保証された処理を進行をサポートするために、ドライバーとフレームワークを実行する手順を次に示します。

1.  ドライバー呼び出し[ **WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)します。

    応答では、フレームワークは割り当てし、ドライバーを指定する要求オブジェクトの数を格納します。 ドライバーと呼ばれていた場合[ **WdfDeviceInitSetRequestAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)、各割り当てには、コンテキストの領域が含まれますが**WdfDeviceInitSetRequestAttributes**指定します。

    さらに、ドライバーが指定されている場合、 [ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数では、フレームワークは、毎回その it を割り当てます、および要求を格納は、コールバック関数を呼び出しますオブジェクト。

2.  フレームワークは、I/O マネージャーがドライバーに送信する I/O 要求パケット (IRP) を受け取ります。

    フレームワークは、IRP の要求オブジェクトを割り当てようとします。 要求の種類用に作成されたドライバーがサポートする I/O キューに転送の進行状況が保証される場合、次の手順は、割り当てが成功または失敗したかどうかによって異なります。

    -   要求オブジェクトの割り当てが成功します。

        ドライバーが指定されている場合、 [ *EvtIoAllocateRequestResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数では、フレームワークが呼び出します。 コールバック関数は、状態を返す場合\_I/O キューに成功すると、フレームワークの追加要求。 コールバック関数が、エラー状態の値を返す場合、フレームワークはことだけ作成され、その要求を事前に割り当てられたオブジェクトのいずれかを使用して、要求オブジェクトを削除します。 ドライバーの要求ハンドラーは、要求オブジェクトを受信すると、要求オブジェクトが事前に割り当てられたと、そのため、ドライバーのどちらかどうかを使用する事前に割り当てられるリソースかどうかを決定します。

        場合は、ドライバー*いない*提供、 [ *EvtIoAllocateRequestResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数では、フレームワークで、I/O キュー、ドライバーがあるない場合と同様に、要求が追加されます保証された処理を進行を有効になります。

    -   要求オブジェクトの割り当ては失敗します。

        どのようなフレームワークは次のドライバーが提供される値によって異なります、 **ForwardProgressReservedPolicy**のメンバー、 [ **WDF\_IO\_キュー\_フォワード\_進行状況\_ポリシー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)構造体。 このメンバーにより、フレームワークは予約済みの要求を使用する場合: 常に、I/O 要求が、ページング I/O 操作である場合にのみ、または場合にのみ、 [ *EvtIoWdmIrpForForwardProgress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)コールバック関数を示します予約済みの要求を使用する必要があります。

    すべてのケースで、ドライバーの要求ハンドラーを呼び出すことができます[ **WdfRequestIsReserved** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestisreserved)をフレームワークが予約済みの要求オブジェクトを使用するかどうかを判断します。 そのため、ドライバーが要求のリソースを使用する場合をその[ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)割り当てられているコールバック関数。

### <a name="guaranteed-forward-progress-scenario"></a>進行状況を保証

システムのページング ファイルを含む可能性がある記憶装置のドライバーを作成しています。 操作を読み取ることが重要し、ページング ファイルに操作が成功を記述します。

読み取りに対して別の I/O キューを作成および書き込み操作を対象として、有効にするには、これらの I/O キューの両方の進行を保証します。 保証された処理を進行を有効にしなくても他のすべての要求の種類の 3 つ目の I/O キューを作成すること。

ドライバー スタックとデバイスを設定するために、並列で 4 つの書き込み操作を処理できる、 **TotalForwardProgressRequests**のメンバー、 [ **WDF\_IO\_キュー\_フォワード\_進行状況\_ポリシー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)構造体を呼び出す前に 4 [ **WdfIoQueueAssignForwardProgressPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy).

進行を保証する重要であることのみ設定、ドライバーのデバイスがページング デバイスの場合は、そのため、ドライバーを決定する、 **ForwardProgressReservedPolicy** 、WDF のメンバー\_IO\_キュー\_フォワード\_進行状況\_ポリシー構造体[ **WdfIoForwardProgressReservedPolicyPagingIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ne-wdfio-_wdf_io_forward_progress_reserved_policy)します。

ドライバーへの呼び出しに使用するには、いくつかメモリ オブジェクトを割り当てる必要があります事前を決定するには、ドライバーでは、それぞれの読み取り要求および書き込み要求ごとに、framework メモリ オブジェクトが必要であるため[ **WdfIoTargetFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread)と[ **WdfIoTargetFormatRequestForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite)メモリ不足の状況でします。

そのため、ドライバーを提供します、 [ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)キューを読み取り、書き込みキューのもう 1 つのコールバック関数。 これらのコールバック関数のいずれかのフレームワークから呼び出されるたびに、コールバック関数を呼び出す[ **WdfMemoryCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate)メモリ不足の状況の返されたオブジェクトのハンドルを保存します。 コールバック関数が事前に割り当てられた要求オブジェクトへのハンドルを受け取るため、要求オブジェクトへのメモリ オブジェクトの親ことができます。 (DMA デバイス用のドライバーが事前に割り当てても[framework DMA オブジェクト](framework-dma-objects.md))。

[要求ハンドラー](request-handlers.md)の読み取りと書き込みのキューが受信した要求の各オブジェクトは 1 つのメモリ不足の状況、framework が予約されているかどうかを決定する必要があります。 要求ハンドラーを呼び出すことができます[ **WdfRequestIsReserved**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestisreserved)、または、使用して、要求オブジェクト ハンドルを比較できますが、 [ *EvtIoAllocateResourcesForReservedRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)以前に受信するコールバック関数。

用意されており、 [ *EvtIoAllocateRequestResources* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)キューを読み取り、書き込みキューのもう 1 つのコールバック関数。 I/O マネージャーから読み取りまたは書き込み要求を受信し、要求オブジェクトを正常に作成するときにこれらのコールバック関数のいずれかのフレームワークを呼び出します。 これらの各コールバック関数を呼び出す[ **WdfMemoryCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate)メモリ オブジェクトを要求を割り当てられません。 割り当てに失敗した場合、コールバック関数はメモリ不足の状況が発生したフレームワークに通知するエラー状態値を返します。 エラーの戻り値の検出、フレームワークでは、要求オブジェクトを先ほど作成し、事前に割り当てられたオブジェクトのいずれかを使用して削除します。

このドライバーが提供されない、 [ *EvtIoWdmIrpForForwardProgress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)コールバック関数は、個々 の読み取りを確認またはフレームワークを I/O キューに追加する前に、Irp を記述する必要はないためです。

ドライバーは、デバイスの保証された処理を進行を実装すると、デバイスのドライバー スタックのすべての下位レベルのドライバーする必要がありますで実装することが保証された処理を進行を覚えておいてください。

 

 





