---
title: 完了処理が安全な IRQL で実行されるようにする
description: 完了処理が安全な IRQL で実行されるようにする
ms.assetid: 54487fba-2ced-4bcd-afa6-d56b351aa7d6
keywords:
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、完了処理
- i/o 要求の完了 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a83d64463151bb74641ad4c0a4fb6d6df832e92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841426"
---
# <a name="ensuring-that-completion-processing-is-performed-at-safe-irql"></a>完了処理が安全な IRQL で実行されるようにする


## <span id="ddk_ensuring_that_completion_processing_is_performed_at_safe_irql_if"></span><span id="DDK_ENSURING_THAT_COMPLETION_PROCESSING_IS_PERFORMED_AT_SAFE_IRQL_IF"></span>


[Postoperation コールバックルーチンの記述](writing-postoperation-callback-routines.md)に関する記事で説明したように、IRP ベースの i/o 操作の[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、フィルター処理されたドライバーの preoperation コールバックルーチンでない限り、IRQL = ディスパッチ\_レベルで呼び出すことができます。FLT\_PREOP\_SYNCHRONIZE を返すことによって操作が同期されました。または、操作が作成操作であり、本質的に同期がとられています。 (この戻り値の詳細については、「return [FLT\_PREOP\_SYNCHRONIZE](returning-flt-preop-synchronize.md)」を参照してください)。

ただし、まだ同期されていない IRP ベースの i/o 操作の場合、ミニフィルタードライバーはを使用して2つの手法を使用して、完了処理が IRQL &lt;= APC\_レベルで実行されるようにすることができます。

最初の方法は、終了処理を IRQL &lt;= APC\_レベルで実行できるようになるまで i/o 操作を保留する postoperation コールバックルーチンです。 この手法については、「 [Postoperation コールバックルーチンで I/o 操作を保留中](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)」を参照してください。

2つ目の手法では、ミニフィルタードライバーの postoperation コールバックルーチンが[**Fltdocompletionprocessingwhensafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)を呼び出します。 **Fltdopends Processingwhensafe**は、現在の IRQL が &gt;= ディスパッチ\_レベルの場合にのみ i/o 操作を実行します。 それ以外の場合、このルーチンはミニフィルタードライバーの**Safepostcallback**ルーチンを直ちに実行します。 この手法については、「 **Fltdoの Processingwhensafe**」を参照してください。

 

 




