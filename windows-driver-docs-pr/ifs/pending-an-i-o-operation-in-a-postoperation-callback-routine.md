---
title: 操作後コールバック ルーチン内で I/O 操作を保留にする
description: 操作後コールバック ルーチン内で I/O 操作を保留にする
ms.assetid: 126e13fb-51f6-4dcc-aa13-850921b3c752
keywords:
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、保留中の操作
- コールバックルーチンにおける保留中の i/o 操作 WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adafc1e13455253d82db9382f25c1d070ed7b3f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841038"
---
# <a name="pending-an-io-operation-in-a-postoperation-callback-routine"></a>操作後コールバック ルーチン内で I/O 操作を保留にする


## <span id="ddk_pending_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルタードライバーの[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、次の手順を実行して i/o 操作を保留できます。

1.  I/o 操作のために作業項目を割り当てるために[**FltAllocateDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)を呼び出しています。

2.  [**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)を呼び出して、i/o 操作をシステムの作業キューに送信します。

3.  FLT\_POSTOP を返すことで、\_処理\_必要な\_を増やすことができます。

次のいずれかの条件に該当する場合、 **FltQueueDeferredIoWorkItem**の呼び出しは失敗することに注意してください。

-   この操作は、IRP ベースの i/o 操作ではありません。

-   操作はページング i/o 操作です。

-   現在のスレッドの**TopLevelIrp**フィールドが**NULL**ではありません。 (このフィールドの値を検索する方法の詳細については、「 [**IoGetTopLevelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogettoplevelirp)」を参照してください)。

-   I/o 操作のターゲットインスタンスが破棄されています。 (フィルターマネージャーは、この状況を示しています。これは、FLTFL\_POST\_操作\_、*フラグ*入力パラメーター内のドレインフラグを postoperation コールバックルーチンに設定することによって示されます。

このエラーを処理するには、ミニフィルタードライバーを準備する必要があります。 ミニフィルタードライバーがこのようなエラーを処理できない場合は、「i/o 操作を保留するのではなく、 [FLT\_PREOP\_同期を返す](returning-flt-preop-synchronize.md)」で説明されている手法を使用することを検討してください。

ミニフィルタードライバーの postoperation コールバックルーチンによって FLT\_POSTOP が返された後\_より多くの\_処理\_必要な場合、フィルターマネージャーはミニフィルターを使用するまで i/o 操作の完了処理を実行しません。ドライバーの作業ルーチンは[**Fltcompletependedpostoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)を呼び出して、操作の制御をフィルターマネージャーに返します。 このような状況では、操作のコールバックデータ構造の**iostatus. Status**フィールドに失敗の NTSTATUS 値が設定されている場合でも、フィルターマネージャーはそれ以上の処理を実行しません。

I/o 操作の完了処理をデキューして実行する作業ルーチンは、 **Fltcompletependedpostoperation**を呼び出して、操作の制御をフィルターマネージャーに返す必要があります。

 

 




