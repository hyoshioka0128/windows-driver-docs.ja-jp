---
title: I/O 操作の前方進行の保証
description: I/O 操作の前方進行の保証
ms.assetid: e230eb3b-54ac-43b1-ac2b-8fa137cee43e
keywords:
- 保証された前進の進行状況 WDK KMDF
- 前進の進行、保証された WDK KMDF
- 低メモリの状況 (WDK KMDF)
- I/o キュー WDK KMDF、事前進行の保証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55986d5528de4cfcbb385e8c0c98aba0e35d3fa1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844434"
---
# <a name="guaranteeing-forward-progress-of-io-operations"></a>I/O 操作の前方進行の保証


システムのページングデバイス用の記憶域ドライバーなど、一部のドライバーでは、重要なシステムデータが失われないように、サポートされている i/o 操作の一部を障害なしで実行する必要があります。 ドライバーエラーの考えられる原因の1つは、メモリ不足の状況です。 フレームワークまたはドライバーが i/o 要求を処理するのに十分なメモリを割り当てることができない場合は、エラー状態の値を入力すること[で i/o](completing-i-o-requests.md)要求が失敗することがあります。

バージョン1.9 より前の KMDF バージョンでは、i/o マネージャーがドライバーに送信した i/o 要求パケット (IRP) のフレームワーク要求オブジェクトを割り当てることができない場合、フレームワークは常に i/o 要求に失敗します。 メモリ不足が発生したときにドライバーに i/o 要求を処理する機能を提供するために、バージョン1.9 以降のフレームワークでは、i/o キューに対して保証された*前進処理*機能が提供されます。

この機能により、フレームワークとドライバーは、要求オブジェクトと要求関連のドライバーコンテキストバッファーのセットにそれぞれメモリを事前に割り当てることができます。 フレームワークとドライバーは、システムメモリの量が少ない場合にのみ、事前に割り当てられたメモリを使用します。

### <a name="features-of-guaranteed-forward-progress"></a>事前進行の保証の機能

I/o キューに対するフレームワークの保証された進行状況を使用することにより、ドライバーは次のことができます。

-   メモリ不足の状況で特定の i/o キューで使用する一連の要求オブジェクトを事前に割り当てるように、フレームワークに依頼します。

-   メモリ不足が発生した場合に、ドライバーが事前に割り当てられた要求オブジェクトをフレームワークから受信するときに使用できる、要求固有のリソースを事前に割り当てるコールバック関数を提供します。

-   メモリ不足の状況が検出され*ない*場合に、i/o 要求に対してドライバー固有のリソースを割り当てる別のコールバック関数を指定します。 メモリ不足の状況によってこのコールバック関数の割り当てが失敗した場合は、フレームワークが事前に割り当てられた要求オブジェクトのいずれかを使用する必要があるかどうかを示すことができます。

-   事前に割り当てられた要求オブジェクトを使用する必要がある i/o 要求を指定します。 オプションには、すべての Irp に事前に割り当てられたオブジェクトの使用、ページング i/o 操作が進行中の場合にのみ使用されます。または、追加のドライバーコールバック関数によって各 IRP を調べ、事前に割り当てられたオブジェクトを使用するかどうかを判断します。

ドライバーが1つ以上の i/o キューに対して保証された進行状況を実装している場合、ドライバーはメモリ不足の状態で i/o 要求を適切に[処理](processing-i-o-requests.md)できるようになります。 デバイスの既定の i/o キューと、 [**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出すことによってドライバーによって構成されるすべての i/o キューについて、事前に保証された進行状況を実装できます。

使用しているドライバーとドライバーの[i/o ターゲット](using-i-o-targets.md)の両方が事前に保証された進行状況を実装している場合にのみ、このフレームワークの保証された前進処理機能はドライバーに対して機能します。 つまり、ドライバーがデバイスの事前の進行を実装している場合、デバイスのドライバースタック内の下位レベルのドライバーはすべて、事前に保証された進行状況を実装する必要があります。

### <a name="enabling-guaranteed-forward-progress-for-an-io-queue"></a>I/o キューの転送の保証を有効にする

I/o キューの転送の保証を有効にするために、ドライバーは、 [**WDF\_IO\_キューを初期化し\_\_進行状況\_ポリシー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)構造を転送してから、 [**WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)を呼び出します。b. ドライバーが[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出して i/o キューを構成する場合は、 **WdfIoQueueAssignForwardProgressPolicy**を呼び出す前にドライバーを呼び出す必要があります。

ドライバーが[**WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)を呼び出すと、次の3つのイベントコールバック関数を指定できます。これらはいずれも省略可能です。

<a href="" id="evtioallocateresourcesforreservedrequest"></a>[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)  
ドライバーの[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数は、メモリ不足の状況に対してフレームワークが予約している要求オブジェクトに対して、要求固有のリソースを割り当て、格納します。

フレームワークは、予約された要求オブジェクトを作成するたびに、このコールバック関数を呼び出します。 ドライバーは、通常、予約済みの要求オブジェクトの[コンテキスト空間](framework-object-context-space.md)を使用して、1つの i/o 要求に対して要求固有のリソースを割り当てます。

<a href="" id="evtioallocaterequestresources"></a>[*EvtIoAllocateRequestResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)  
ドライバーの[*EvtIoAllocateRequestResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数は、直ちに使用するために要求固有のリソースを割り当てます。 これは、フレームワークが IRP を受信し、IRP の要求オブジェクトを作成した直後に呼び出されます。

コールバック関数がリソースを割り当てようとして失敗した場合、コールバック関数はエラー状態の値を返します。 フレームワークは、新しく作成された要求オブジェクトを削除し、その予約済みの要求オブジェクトの1つを使用します。 さらに、ドライバーの[要求ハンドラー](request-handlers.md)は、 [*EvtIoAllocateRequestResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数によって以前に割り当てられた要求固有のリソースを使用します。

<a href="" id="evtiowdmirpforforwardprogress"></a>[*Evtiowdmirpq Forforwardprogress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)  
ドライバーの[*Evtiowdmiシャードの進行状況*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)のコールバック関数は、irp を調べ、予約済みの要求オブジェクトを irp に使用するか、エラー状態の値を入力して i/o 要求を失敗させるかをフレームワークに通知します。

フレームワークは、フレームワークが新しい要求オブジェクトを作成できない場合にのみ、このコールバック関数を呼び出します。これは、(ドライバーの WDF\_IO\_キューのフラグを設定することによって[ **\_進行状況\_ポリシー\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)する場合にのみ呼び出されます。[構造]) を使用すると、ドライバーがメモリ不足の状態で Irp を調べることができます。 つまり、ドライバーは各 IRP を評価し、メモリ不足が発生した場合でも処理する必要があるかどうかを判断できます。

ドライバーが[**WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)を呼び出すと、メモリ不足の状況に対してフレームワークが事前に割り当てる必要がある予約済みの要求オブジェクトの数も指定します。 デバイスとドライバーに適した要求オブジェクトの数を選択できます。 パフォーマンスを低下させないようにするには、通常、ドライバーとデバイスが並列で処理できる i/o 要求の数を概算する数値を指定する必要があります。

ただし、ドライバーの[**WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)とその[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback 関数の呼び出しによって、予約済みの要求オブジェクトが過剰に割り当てられたり、要求固有のリソースメモリが多すぎたりする場合は、ドライバーは、処理しようとしているメモリ不足の状況に実際に寄与する可能性があります。 最適な数を判断するには、ドライバーとデバイスのパフォーマンスをテストし、メモリ不足のシミュレーションを含める必要があります。

[**WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)が戻る前に、フレームワークによって、ドライバーが指定した要求オブジェクトの数が作成され、予約されます。 フレームワークは、要求オブジェクトを予約するたびに、ドライバーの[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback 関数を呼び出します。これにより、フレームワークによっては、ドライバーが要求固有のリソースを割り当てて保存できるようになります。予約済みの要求オブジェクトを実際に使用します。

ドライバーの[要求ハンドラー](request-handlers.md)の1つが i/o キューから i/o 要求を受信すると、 [**Wdfrequestisreserved**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved)メソッドを呼び出して、要求オブジェクトが、メモリ不足の状況に対してフレームワークに事前に割り当てられているものかどうかを判断できます。 このメソッドが**TRUE**を返す場合、ドライバーは、 [*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback 関数が予約されているリソースを使用する必要があります。

フレームワークが予約されている要求オブジェクトの1つを使用している場合は、ドライバーが要求を完了した後、オブジェクトがその予約済みオブジェクトのセットに返されます。 フレームワークは、別のメモリ不足が発生した場合に再利用するために、要求オブジェクトと、 [**Wdfdeviceinitsetrequestattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)または[**WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext)を呼び出すことによってドライバーが作成したすべてのコンテキスト領域を保存します。

### <a name="how-the-framework-and-driver-support-guaranteed-forward-progress"></a>フレームワークとドライバーのサポートが事前進行を保証する方法

次に、i/o キューの保証された進行状況をサポートするためにドライバーとフレームワークが実行する手順を示します。

1.  ドライバーは[**WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)を呼び出します。

    応答として、フレームワークは、ドライバーが指定する要求オブジェクトの数を割り当てて格納します。 ドライバーが[**Wdfdeviceinitsetrequestattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)を以前に呼び出した場合、各割り当てには、 **wdfdeviceinitsetrequestattributes**が指定されたコンテキスト空間が含まれます。

    また、ドライバーが[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数を提供した場合、フレームワークは、要求オブジェクトを割り当てて格納するたびにコールバック関数を呼び出します。

2.  このフレームワークは、i/o マネージャーがドライバーに送信している i/o 要求パケット (IRP) を受信します。

    フレームワークは、IRP の要求オブジェクトを割り当てようとします。 要求の種類に対して作成されたドライバーが送信の保証をサポートしている i/o キューがある場合、次の手順は、割り当てが成功したか失敗したかによって異なります。

    -   要求オブジェクトの割り当ては成功します。

        ドライバーが[*EvtIoAllocateRequestResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数を提供した場合、フレームワークはそれを呼び出します。 コールバック関数が STATUS\_SUCCESS を返した場合、フレームワークは i/o キューに要求を追加します。 コールバック関数がエラー状態の値を返す場合、フレームワークは、作成した要求オブジェクトを削除し、事前に割り当てられた要求オブジェクトの1つを使用します。 ドライバーの要求ハンドラーは、要求オブジェクトを受け取ると、要求オブジェクトが事前に割り当てられているかどうかを判断します。したがって、ドライバーの事前割り当て済みリソースを使用する必要があるかどうかを判断します。

        ドライバーが[*EvtIoAllocateRequestResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数*を提供しなかった*場合は、ドライバーが有効になっていないとしても、要求が i/o キューに追加されます。

    -   要求オブジェクトの割り当てに失敗します。

        フレームワークの動作は次のようになります。これは、WDF\_IO\_キューの**ForwardProgressReservedPolicy**メンバーに対して指定されたドライバーが[ **\_進行状況\_ポリシー構造\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)する値によって決まります。 このメンバーは、予約された要求を使用するタイミングをフレームワークに通知します。常に、i/o 要求がページング i/o 操作である場合にのみ、または[*Evtiowdmirpq Forforwardprogress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)コールバック関数が予約された要求を使用することを示している場合にのみ使用します。

    どのような場合でも、ドライバーの要求ハンドラーは、 [**Wdfrequestisreserved**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved)を呼び出して、フレームワークが予約済みの要求オブジェクトを使用しているかどうかを判断できます。 その場合、ドライバーは、 [*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback 関数が割り当てた要求リソースを使用する必要があります。

### <a name="guaranteed-forward-progress-scenario"></a>保証された進行状況のシナリオ

システムのページングファイルが含まれている可能性のある記憶装置用のドライバーを作成しています。 ページングファイルに対する読み取り操作と書き込み操作が成功することが重要です。

読み取り操作と書き込み操作用に個別の i/o キューを作成し、これらの i/o キューの両方に対して事前処理を有効にすることを決定しました。 その他のすべての要求の種類に対して、前処理が保証されないように、3つ目の i/o キューを作成することにしました。

ドライバースタックとデバイスは、4つの書き込み操作を並行して処理できるため、WDF\_IO\_キューの**Totalforwardprogress 要求**メンバーを[ **\_転送\_進行状況\_ポリシー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy)に設定します。[**WdfIoQueueAssignForwardProgressPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy)を呼び出す前の構造体が4になります。

ドライバーのデバイスがページングデバイスである場合にのみ、進行状況を保証することが重要であると判断した場合は、ドライバーが WDF\_IO\_キューの**ForwardProgressReservedPolicy**メンバーを設定して\_進行状況を転送\_@no[**WdfIoForwardProgressReservedPolicyPagingIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ne-wdfio-_wdf_io_forward_progress_reserved_policy)にポリシー構造を適用します。

ドライバーでは、各読み取り要求と書き込み要求に対してフレームワークメモリオブジェクトが必要であるため、 [**Wdfiotargetformatrequestforread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread) [**の呼び出しに使用するメモリオブジェクトをドライバーが事前に割り当てておく必要があります。メモリ不足の状況での WdfIoTargetFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite) 。

このため、ドライバーは、読み取りキュー用の[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)コールバック関数と、書き込みキュー用の別のコールバック関数を提供します。 フレームワークがこれらのコールバック関数のいずれかを呼び出すたびに、コールバック関数は[**Wdfmemorycreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)を呼び出し、メモリ不足の状況に対して返されたオブジェクトハンドルを保存します。 コールバック関数は、事前に割り当てられた要求オブジェクトへのハンドルを受け取るため、メモリオブジェクトを要求オブジェクトに親できます。 (DMA デバイスのドライバーでは、[フレームワークの dma オブジェクト](framework-dma-objects.md)も事前に割り当てられる場合があります)。

読み取りキューと書き込みキューの[要求ハンドラー](request-handlers.md)は、受信した各要求オブジェクトが、メモリ不足状態のためにフレームワークによって予約されているものであるかどうかを判断する必要があります。 要求ハンドラーは、 [**Wdfrequestisreserved**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved)を呼び出すことができます。また、要求オブジェクトハンドルと[*EvtIoAllocateResourcesForReservedRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback 関数が以前に受信したものとを比較することもできます。

また、このドライバーは、読み取りキュー用の[*EvtIoAllocateRequestResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)コールバック関数と、書き込みキュー用の別のコールバック関数も提供します。 フレームワークは、i/o マネージャーから読み取り要求または書き込み要求を受信し、要求オブジェクトを正常に作成するときに、これらのコールバック関数のいずれかを呼び出します。 これらの各コールバック関数は、 [**Wdfmemorycreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)を呼び出して、要求にメモリオブジェクトを割り当てます。 割り当てが失敗した場合、コールバック関数は、メモリ不足の状況が発生したことをフレームワークに通知するために、エラー状態の値を返します。 エラーの戻り値を検出するフレームワークは、作成した要求オブジェクトを削除し、事前に割り当てられたオブジェクトのいずれかを使用します。

このドライバーは、フレームワークによって i/o キューに追加される前に個々の読み取りまたは書き込みの Irp を調べる必要がないため、 [*Evtiowdmiシャードの進行状況*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)のコールバック関数を提供しません。

ドライバーがデバイスの転送前の進行状況を実装する場合、デバイスのドライバースタック内のすべての下位レベルのドライバーも、事前に保証された進行状況を実装する必要があることに注意してください。

 

 





