---
title: I/O 操作の処理
description: I/O 操作の処理
ms.assetid: 750fa89b-dbdf-45ff-bfa5-83c717d2d7bb
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、i/o 操作の処理
- preoperation コールバックルーチン WDK ファイルシステムミニフィルターマネージャー
- postoperation コールバックルーチン WDK ファイルシステムミニフィルターマネージャー
- 便宜的ロック WDK ファイルシステムミニフィルター
- WDK ファイルシステムミニフィルターのロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27eddc036058e17a182f565ecb90f1495ab9e10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841022"
---
# <a name="processing-io-operations"></a>I/O 操作の処理


フィルターマネージャーを使用すると、ミニフィルタードライバーの i/o 操作の処理が簡単になります。 レガシフィルタードライバーは、すべての i/o 要求を次の下位のドライバーに正しく渡す必要があります。また、レガシフィルタードライバーが要求に関連する処理を行うかどうかに関係なく、保留中の要求、同期、および i/o の完了を正しく処理する必要があります。は、処理する必要がある i/o 操作に対してのみ登録します。

特定の i/o 操作では、フィルターマネージャーは、その操作に対して[**事前操作コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)ルーチンが登録されているミニフィルタードライバーのみを呼び出します。 フィルターマネージャーは、ミニフィルタードライバーに代わって特定の IRP メンテナンスタスクを処理します。たとえば、パラメーターを次のスタック位置にコピーし、IRP **Pendingreturned れ**たフラグを伝達することができます。

事前操作コールバックルーチンでは、ミニ操作コールバックルーチンから適切な値を返すことによって、i/o 操作に必要な処理がすべてミニフィルタードライバーによって行われます。 たとえば、完了ルーチンを使用せずに、IRP を次の下位のドライバーに転送する場合、ミニフィルタードライバーは、FLT\_PREOP\_SUCCESS\_\_コールバックなしで返されます。完了ルーチン (i/o 操作のミニフィルタードライバーの postoperation コールバックルーチン) で同じ操作を実行するには、ミニフィルタードライバーが\_コールバックで FLT\_PREOP\_SUCCESS\_を返します。

事前操作コールバックルーチンでは、 [**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)を呼び出すことによって、必要に応じてミニフィルタードライバーがワーカースレッドに操作をキューできます。 この操作を実行すると、ミニ操作コールバックルーチンから保留中の FLT\_PREOP\_PENDING が返され、i/o 操作が保留中であることが示されます。また、ミニフィルタードライバーは、要求の処理を完了または再開します. 処理を再開するには、ミニフィルタードライバーがワーカースレッドから[**Fltcompletependedpreoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)を呼び出します。

ミニフィルタードライバーが、処理対象の未処理の i/o 操作のインスタンスごとのキャンセルセーフキューを保持する必要がある場合、そのようなキューを設定するには、 *Instancesetupcallback*ルーチンで[*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)を呼び出し、必要に応じて preoperation コールバックルーチンで[*FltCbdqInsertIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinsertio)を呼び出して、i/o 操作をキューに挿入します。

フィルターマネージャーは、低フィルタドライバー (レガシフィルターおよびミニフィルタードライバー) が完了処理を完了したときに、ミニフィルタードライバーの i/o 操作に対してミニ[**操作コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)ルーチンを呼び出します。

Postoperation コールバックルーチンでは、ミニフィルタードライバーは[**Fltdocompletion Processingwhensafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)を呼び出して、完了処理が安全な IRQL で実行されるようにすることができます。 または、 [**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)を呼び出すことによって、必要に応じて、操作の完了処理をワーカースレッドにキューすることができます。 この操作を実行すると、ミニフィルタードライバーは、postoperation コールバックルーチンから必要な\_の処理\_より多くの\_を\_返します。これにより、i/o 操作のフィルターマネージャーの完了処理が中断されます。 完了処理を再開するために、ミニフィルタードライバーはワーカースレッドから[**Fltcompletependedpostoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)を呼び出します。

フィルターマネージャーは、i/o 操作ではなく、ミニフィルタードライバーまたはミニフィルタードライバーインスタンスに関連付けられた作業項目である "汎用" 作業項目のキューのサポートを提供します。 ミニフィルタードライバーは、 [**Fltqueuegenericworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)を呼び出して、作業項目をシステム作業キューに挿入できます。 このルーチンは、 [**Exqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exqueueworkitem)などのルーチンに似ています。たとえば、 [**FltAllocateGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)を呼び出すことによって割り当てられた作業項目は再利用できます。 ただし、フィルターマネージャーでは、未処理の作業項目がまだ処理されている間はミニフィルタードライバーまたはミニフィルタードライバーインスタンスをアンロードできないため、 **Fltqueuegenericworkitem**はミニフィルタードライバーを使用する方が安全です。

フィルターマネージャーでは、便宜的ロック (oplock) 操作もサポートされています。 Oplock 操作の場合、ミニフィルタードライバーは[**Fltinitializeoplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializeoplock)および[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)としてこのようなフィルターマネージャールーチンを使用できます。これは、 **FsRtlInitializeOplock**および**FsRtlOplockFsctrl**ルーチンと同等です。ファイルシステムおよびレガシフィルタードライバーによって使用されます。

### <a name="span-idfilter_manager_routines_for_processing_i_o_operationsspanspan-idfilter_manager_routines_for_processing_i_o_operationsspanspan-idfilter_manager_routines_for_processing_i_o_operationsspanfilter-manager-routines-for-processing-io-operations"></a><span id="Filter_Manager_Routines_for_Processing_I_O_Operations"></span><span id="filter_manager_routines_for_processing_i_o_operations"></span><span id="FILTER_MANAGER_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>I/o 操作を処理するためのフィルターマネージャールーチン

フィルターマネージャーには、 [**preoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)および[**postoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)コールバックルーチンでの保留中の i/o に対する次のサポートルーチンが用意されています。

[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)

[**FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)

[**Fltdo補完 Processingwhensafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)

次のルーチンは、事前操作および postoperation コールバックルーチンで作業項目をキューに置いたときに使用されます。

[**FltAllocateDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)

[**FltAllocateGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)

[**FltFreeDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreedeferredioworkitem)

[**FltFreeGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreegenericworkitem)

[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)

[**FltQueueGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)

次のルーチンは、キャンセルセーフキューのサポートを提供します。

[*FltCbdqDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqdisable)

[*FltCbdqEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqenable)

[*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)

[*FltCbdqInsertIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinsertio)

[*FltCbdqRemoveIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqremoveio)

[*FltCbdqRemoveNextIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqremovenextio)

次のルーチンでは、oplock のサポートが提供されます。

[*FltCheckOplock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcheckoplock)

[**FltCurrentBatchOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcurrentbatchoplock)

[**FltInitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializeoplock)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FltOplockIsFastIoPossible**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockisfastiopossible)

[**FltUninitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializeoplock)

### <a name="span-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanspan-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanspan-idminifilter_driver_callback_routines_for_processing_i_o_operationsspanminifilter-driver-callback-routines-for-processing-io-operations"></a><span id="Minifilter_Driver_Callback_Routines_for_Processing_I_O_Operations"></span><span id="minifilter_driver_callback_routines_for_processing_i_o_operations"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>I/o 操作を処理するためのミニフィルタードライバーのコールバックルーチン

次のコールバックルーチンは、ミニフィルタードライバーが処理する i/o 操作の種類ごとに、 [**FLT\_操作\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration)構造体に格納されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバックルーチン名</th>
<th align="left">コールバックルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>PostOperation</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_POST_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)"><strong>PFLT_POST_OPERATION_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>PreOperation</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




