---
title: 操作後コールバック ルーチン内で I/O 操作を保留にする
description: 操作後コールバック ルーチン内で I/O 操作を保留にする
ms.assetid: 126e13fb-51f6-4dcc-aa13-850921b3c752
keywords:
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、保留中の操作
- 保留中のコールバック ルーチン WDK で I/O 操作は、ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e050d4bbdebbbe7e357b7418114583eff5d6a62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386056"
---
# <a name="pending-an-io-operation-in-a-postoperation-callback-routine"></a>操作後コールバック ルーチン内で I/O 操作を保留にする


## <span id="ddk_pending_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_PENDING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルター ドライバーの[ **postoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)次の手順を実行することによって、I/O の保留操作ができます。

1.  呼び出す[ **FltAllocateDeferredIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem) I/O 操作を作業項目を割り当てられません。

2.  呼び出す[ **FltQueueDeferredIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)システム ワーク キューに I/O 操作を投稿します。

3.  返す FLT\_POSTOP\_詳細\_処理\_必要な作業です。

なおへの呼び出し**FltQueueDeferredIoWorkItem**次の条件のいずれかに該当する場合は失敗します。

-   操作は IRP ベースの I/O 操作ではありません。

-   ページング I/O 操作にします。

-   **TopLevelIrp** 、現在のスレッドのフィールドがない**NULL**します。 (このフィールドの値を検索する方法の詳細については、次を参照してください[ **IoGetTopLevelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogettoplevelirp)。)。

-   I/O 操作のターゲット インスタンスが破棄されています。 (フィルター マネージャーでは、このような状況を示す、FLTFL を設定して\_POST\_操作\_でドレイン中のフラグ、*フラグ*postoperation コールバック ルーチンへの入力パラメーターです)。

ミニフィルター ドライバーは、このエラーを処理するために準備する必要があります。 ミニフィルター ドライバーは、このようなエラーを処理できない場合に記載されている手法を使用してを考慮する必要があります[返す FLT\_PREOP\_同期](returning-flt-preop-synchronize.md)の代わりに保留中の I/O 操作。

ミニフィルター ドライバーの postoperation コールバック ルーチン返します FLT\_POSTOP\_詳細\_処理\_必要に応じて、フィルター マネージャーがない補完を実行、さらに、I/O の処理ミニフィルター ドライバーのルーチンの呼び出しを操作するまで、操作を[ **FltCompletePendedPostOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation)操作の制御フィルター マネージャーを返します。 フィルター マネージャーが処理は実行、さらにこのような状況での作業工程の障害 NTSTATUS 値を設定する場合でも、 **IoStatus.Status**操作のコールバックのデータ構造のフィールド。

デキューし、I/O 操作を呼び出す必要がありますの完了処理を実行する作業ルーチン**FltCompletePendedPostOperation**操作の制御フィルター マネージャーを返します。

 

 




