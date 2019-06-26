---
title: I/O 操作の処理
description: I/O 操作の処理
ms.assetid: 750fa89b-dbdf-45ff-bfa5-83c717d2d7bb
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、I/O 操作の処理
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、フィルター マネージャー
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、フィルター マネージャー
- 便宜的ロック WDK ファイル システム ミニフィルター
- ロックの WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32f0f06ba6b20947f252557d2d0c526999755055
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385154"
---
# <a name="processing-io-operations"></a>I/O 操作の処理


フィルター マネージャーは、ミニフィルター ドライバーに対する I/O の処理操作を簡略化します。 レガシ フィルターとは異なりドライバーでは、次の下位ドライバーにすべての I/O 要求を正しく渡すし、レガシ フィルター ドライバーは、作業するかどうか、保留中の要求、同期、および I/O 完了正しく処理する必要があります要求に関連する、ミニフィルター ドライバー処理する必要がありますが、I/O 操作のみを登録します。

フィルター マネージャーが登録されているミニフィルター ドライバーのみを呼び出す特定の I/O 操作の[ **preoperation コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)操作ルーチン。 フィルター マネージャーもパラメーターをスタックの次の場所にコピーし、IRP を伝達するなど、ミニフィルター ドライバーに代わって特定の IRP メンテナンス タスクを処理**PendingReturned**フラグ。

その preoperation コールバック ルーチンでミニフィルター ドライバーはどのような処理が I/O 操作のために必要なし、preoperation コールバック ルーチンから適切な値を返すことによって、IRP を処理することを示します。 ミニフィルター ドライバー返す FLT 完了ルーチンなし次の下位ドライバーは IRP を転送するには、するにはたとえば、\_PREOP\_成功\_いいえ\_(、完了のルーチンで同じ処理を実行するコールバック。ミニフィルター ドライバーの postoperation コールバック ルーチンの I/O 操作)、ミニフィルター ドライバー返します FLT\_PREOP\_成功\_WITH\_コールバック。

その preoperation コールバック ルーチンでミニフィルター ドライバー キューに入れることをワーカー スレッドの操作を呼び出して必要な場合[ **FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)します。 その後、ミニフィルター ドライバーに返す FLT\_PREOP\_を I/O 操作が保留中であり、ミニフィルター ドライバーが完了または再開の処理を担当することを示すために、preoperation コールバック ルーチンからの保留要求。 ミニフィルター ドライバーの呼び出しの処理を再開[ **FltCompletePendedPreOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)ワーカー スレッドから。

ミニフィルター ドライバーが処理される未処理の I/O 操作の独自のインスタンスごとのキャンセルの安全なキューを維持するために必要な場合に呼び出すことによって、このようなキューを設定できます[ *FltCbdqInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinitialize)そので*InstanceSetupCallback*ルーチンと呼び出し元[ *FltCbdqInsertIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinsertio)で I/O 操作をキューに挿入する、必要に応じて、preoperation コールバック ルーチン。

フィルター マネージャー呼び出しミニフィルター ドライバーの[ **postoperation コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)低いフィルター ドライバー (レガシ フィルターおよびミニフィルター ドライバー) が完了したら、I/O 操作ルーチン処理しています。

ミニフィルター ドライバーを呼び出すことができます、postoperation コールバック ルーチンで[ **FltDoCompletionProcessingWhenSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)安全な IRQL で処理を実行すると、その完了を確認します。 ワーカー スレッドを操作の完了処理をキューには、呼び出すことによって必要な場合または[ **FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)します。 その後、ミニフィルター ドライバーに返す FLT\_POSTOP\_詳細\_処理\_postoperation コールバック ルーチンからフィルター マネージャーの完了の I/O 操作の処理を停止するために必要な。 ミニフィルター ドライバーの呼び出しの完了処理を再開する[ **FltCompletePendedPostOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation)ワーカー スレッドから。

フィルター マネージャーは、「汎用」作業項目の I/O 操作ではなく、ミニフィルター ドライバーまたはミニフィルター ドライバーのインスタンスに関連付けられている作業項目のキューのサポートを提供します。 ミニフィルター ドライバーは呼び出すことによってシステム ワーク キューに作業項目を挿入することができます[ **FltQueueGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuegenericworkitem)します。 このルーチンはなどのルーチンに似ています[ **ExQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exqueueworkitem)例: 作業項目 (呼び出しによって割り当てられた[ **FltAllocateGenericWorkItem** 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocategenericworkitem)) を再利用できます。 ただし、 **FltQueueGenericWorkItem**ミニフィルター ドライバーまたはミニフィルター ドライバーのインスタンスをアンロード未完了の作業項目がまだされている間にフィルター マネージャーが許可されないために、ミニフィルター ドライバーを使用するより安全には処理されます。

フィルター マネージャーもサポートの便宜的ロック (oplock) 操作を提供します。 ミニフィルター ドライバーの oplock の操作としてこのようなフィルター マネージャー ルーチンを使用できます[ **FltInitializeOplock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializeoplock)と[ **FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)と同等である、 **FsRtlInitializeOplock**と**FsRtlOplockFsctrl**ファイル システムとレガシ フィルター ドライバーで使用されるルーチン。

### <a name="span-idfiltermanagerroutinesforprocessingiooperationsspanspan-idfiltermanagerroutinesforprocessingiooperationsspanspan-idfiltermanagerroutinesforprocessingiooperationsspanfilter-manager-routines-for-processing-io-operations"></a><span id="Filter_Manager_Routines_for_Processing_I_O_Operations"></span><span id="filter_manager_routines_for_processing_i_o_operations"></span><span id="FILTER_MANAGER_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>I/O 操作を処理するマネージャー ルーチンをフィルター処理します。

フィルター マネージャーでの I/O の保留中の次のサポート ルーチンを提供する[ **preoperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)と[ **postoperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)コールバックルーチン:

[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation)

[**FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)

[**FltDoCompletionProcessingWhenSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)

Preoperation と postoperation コールバック ルーチンのキュー作業項目では、次のルーチンが使用されます。

[**FltAllocateDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)

[**FltAllocateGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocategenericworkitem)

[**FltFreeDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreedeferredioworkitem)

[**FltFreeGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreegenericworkitem)

[**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)

[**FltQueueGenericWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuegenericworkitem)

次のルーチンでは、キャンセルの安全なキューのサポートを提供します。

[*FltCbdqDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqdisable)

[*FltCbdqEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqenable)

[*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinitialize)

[*FltCbdqInsertIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqinsertio)

[*FltCbdqRemoveIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqremoveio)

[*FltCbdqRemoveNextIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcbdqremovenextio)

次のルーチンでは、oplock のサポートを提供します。

[*FltCheckOplock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcheckoplock)

[**FltCurrentBatchOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcurrentbatchoplock)

[**FltInitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializeoplock)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FltOplockIsFastIoPossible**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockisfastiopossible)

[**FltUninitializeOplock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuninitializeoplock)

### <a name="span-idminifilterdrivercallbackroutinesforprocessingiooperationsspanspan-idminifilterdrivercallbackroutinesforprocessingiooperationsspanspan-idminifilterdrivercallbackroutinesforprocessingiooperationsspanminifilter-driver-callback-routines-for-processing-io-operations"></a><span id="Minifilter_Driver_Callback_Routines_for_Processing_I_O_Operations"></span><span id="minifilter_driver_callback_routines_for_processing_i_o_operations"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_PROCESSING_I_O_OPERATIONS"></span>I/O 操作を処理するためのミニフィルター ドライバー コールバック ルーチン

次のコールバック ルーチンが格納されている、 [ **FLT\_操作\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_operation_registration)ミニフィルター ドライバーを処理する I/O 操作の種類ごとに構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバック ルーチンの名前</th>
<th align="left">コールバック ルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>PostOperation</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_POST_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)"><strong>PFLT_POST_OPERATION_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>PreOperation</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




