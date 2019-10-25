---
title: プリ操作コールバックルーチンで i/o 操作を保留しています
description: プリ操作コールバックルーチンで i/o 操作を保留しています
ms.assetid: 39b04911-c0d9-42ec-b93e-b440b12f9e41
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、保留中の操作
- コールバックルーチンにおける保留中の i/o 操作 WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ba29a922377502458583a7227a93103fa5a0331
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841036"
---
# <a name="pending-an-io-operation-in-a-preoperation-callback-routine"></a>プリ操作コールバックルーチンで i/o 操作を保留しています


## <span id="ddk_pending_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)は、操作をシステムの作業キューに送信し、FLT\_preoperation\_PENDING を返すことによって、i/o 操作を保留できます。 この状態値を返すことは、ミニフィルタードライバーが、i/o 操作の処理を再開するために[**Fltcompletependedpreoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)を呼び出すまで i/o 操作の制御を維持していることを示します。

ミニフィルタードライバーの preoperation コールバックルーチンは、次の手順を実行して i/o 操作を pends します。

1.  [**FltQueueDeferredIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)などのルーチンを呼び出して、i/o 操作をシステム作業キューに送信します。

2.  FLT\_PREOP\_PENDING を返しています。

すべて (またはほとんど) の入出力操作を保留する必要があるミニフィルタードライバーでは、 **FltQueueDeferredIoWorkItem**などのルーチンを使用して操作を保留することはできません。このルーチンを呼び出すと、システムの作業キューがあふれてしまう可能性があるからです。 代わりに、このようなミニフィルタードライバーでは、キャンセルセーフキューを使用する必要があります。 キャンセルセーフキューの使用の詳細については、「 [*FltCbdqInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcbdqinitialize)」を参照してください。

次のいずれかの条件に該当する場合、 **FltQueueDeferredIoWorkItem**の呼び出しは失敗することに注意してください。

-   この操作は、IRP ベースの i/o 操作ではありません。

-   操作はページング i/o 操作です。

-   現在のスレッドの**TopLevelIrp**フィールドが**NULL**ではありません。 (このフィールドの値を検索する方法の詳細については、「 [**IoGetTopLevelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogettoplevelirp)」を参照してください)。

-   I/o 操作のターゲットインスタンスが破棄されています。

ミニフィルタードライバーの preoperation コールバックルーチンが、FLT\_PREOPERATION\_PENDING を返した*場合、完了後の出力パラメーター*で**NULL**を返す必要があります。

ミニフィルタードライバーは、IRP ベースの i/o 操作に対してのみ保留中の FLT\_PREOP\_を返すことができます。 操作が IRP ベースの i/o 操作であるかどうかを判断するには、 [**FLT\_is\_irp\_operation**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))マクロを使用します。

I/o 操作をデキューして処理する作業ルーチンでは、操作の処理を再開するために**Fltcompletependedpreoperation**を呼び出す必要があります。

 

 




