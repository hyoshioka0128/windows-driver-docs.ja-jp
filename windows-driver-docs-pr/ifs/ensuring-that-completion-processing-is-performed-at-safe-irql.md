---
title: 完了処理が安全な IRQL で実行されるようにする
description: 完了処理が安全な IRQL で実行されるようにする
ms.assetid: 54487fba-2ced-4bcd-afa6-d56b351aa7d6
keywords:
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、処理の完了
- WDK のファイル システムを要求する I/O の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd8a46d0a4c5a143c66a6fc10ef42c7581598fdb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386099"
---
# <a name="ensuring-that-completion-processing-is-performed-at-safe-irql"></a>完了処理が安全な IRQL で実行されるようにする


## <span id="ddk_ensuring_that_completion_processing_is_performed_at_safe_irql_if"></span><span id="DDK_ENSURING_THAT_COMPLETION_PROCESSING_IS_PERFORMED_AT_SAFE_IRQL_IF"></span>


説明したとおり[書き込み Postoperation コールバック ルーチン](writing-postoperation-callback-routines.md)、 [ **postoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback) IRP ベースの I/O 操作は、IRQL で呼び出すことができます = ディスパッチ\_レベル、ミニフィルター ドライバーの preoperation しない限り、コールバック ルーチンが同期操作 FLT を返すことによって\_PREOP\_同期または操作は本質的な同期は、作成操作をします。 (この戻り値の詳細については、次を参照してください[返す FLT\_PREOP\_同期](returning-flt-preop-synchronize.md)。)。

ただし、IRP ベースの I/O 操作が既に同期されていない、ミニフィルター ドライバーを使用してできます 2 つの手法 IRQL で完了処理を実行するために&lt;APC を =\_レベル。

最初の手法が保留に postoperation コールバック ルーチンの I/O 操作 IRQL で実行できる処理を完了するまで&lt;APC を =\_レベル。 この手法については、「 [Postoperation コールバック ルーチンで、保留中の I/O 操作](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)します。

ミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出すには、2 番目の手法[ **FltDoCompletionProcessingWhenSafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)します。 **FltDoCompletionProcessingWhenSafe**とれた、I/O 操作の現在の IRQL が場合にのみ&gt;= ディスパッチ\_レベル。 それ以外の場合、このルーチンがミニフィルター ドライバーの**SafePostCallback**ルーチンをすぐにします。 この手法については、「 **FltDoCompletionProcessingWhenSafe**します。

 

 




