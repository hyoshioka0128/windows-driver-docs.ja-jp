---
title: Preoperation コールバック ルーチンで高速な I/O 操作を許可しません。
description: Preoperation コールバック ルーチンで高速な I/O 操作を許可しません。
ms.assetid: 20797d8c-ffcf-46df-b870-839d5c02d2d4
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、高速な I/O を禁止しています
- 高速な I/O 操作の WDK ファイル システム ミニフィルターを禁止します。
- 高速の I/O には、WDK のファイル システムが許可されていません
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afc61f1f77cee583691f97684d1dce45da0859d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385557"
---
# <a name="disallow-a-fast-io-operation-in-a-preoperation-callback-routine"></a>Preoperation コールバック ルーチンで高速な I/O 操作を許可しません。


## <span id="ddk_disallowing_a_fast_io_operation_in_a_preoperation_callback_routine"></span><span id="DDK_DISALLOWING_A_FAST_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE"></span>


特定の状況でミニフィルター ドライバーを完了するのではなく高速な I/O 操作を許可しないようにできます。 高速な I/O 操作を禁止することにより、高速の I/O パス操作に使用されていることを防ぎます。

など、I/O 操作を完了すると、高速な I/O 操作を禁止することで処理を停止し、フィルター マネージャーに返すことを意味します。 ただし、高速な I/O 操作を禁止することは完了と異なるです。 ミニフィルター ドライバーには、I/O マネージャーによって発行された高速な I/O 操作が許可されていません、I/O マネージャーは同等の IRP ベースの操作と同じ操作を再発行することがあります。

ミニフィルター ドライバーのときに[ **preoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)高速の I/O 操作を許可されていません。 フィルター マネージャーは次の。

-   以下の現在のミニフィルター ドライバー ミニフィルター ドライバー、レガシ フィルター、またはファイル システム操作を送信しません。

-   呼び出し、 [ **postoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)ミニフィルター ドライバーのインスタンスのスタックでは、現在のミニフィルター ドライバー上ミニフィルター ドライバー。

-   存在する場合の操作で、現在のミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出しません。

ミニフィルター ドライバー FLT を返すことによって、高速の I/O 操作を許可しません\_PREOP\_DISALLOW\_FASTIO、操作の preoperation コールバック ルーチンから。

Preoperation コールバック ルーチンは、コールバックのデータ構造体を設定しないでください**IoStatus.Status**フィールド、フィルター マネージャーがステータスを自動的にこのフィールドを設定するため\_FLT\_DISALLOW\_高速\_IO。

FLT\_PREOP\_DISALLOW\_FASTIO は高速な I/O 操作に対してのみ返されます。 操作が高速な I/O 操作であるかどうかを確認するのを参照してください。 [ **FLT\_IS\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

ミニフィルター ドライバー FLT を返すことができません\_PREOP\_DISALLOW\_IRP の FASTIO\_MJ\_シャット ダウン、IRP\_MJ\_ボリューム\_マウント、または IRP\_MJ\_ボリューム\_マウント解除の動作。

 

 




