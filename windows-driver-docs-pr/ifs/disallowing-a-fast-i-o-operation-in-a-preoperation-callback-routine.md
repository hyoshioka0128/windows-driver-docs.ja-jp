---
title: Preoperation コールバックルーチンで高速 i/o 操作を許可しない
description: Preoperation コールバックルーチンで高速 i/o 操作を許可しない
ms.assetid: 20797d8c-ffcf-46df-b870-839d5c02d2d4
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター (高速 i/o を禁止)
- 高速 i/o 操作を許可しない WDK ファイルシステムミニフィルター
- 高速 i/o が禁止されている WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038301b102db1a7b6111f25340169a8800e152a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841434"
---
# <a name="disallow-a-fast-io-operation-in-a-preoperation-callback-routine"></a>Preoperation コールバックルーチンで高速 i/o 操作を許可しない


## <span id="ddk_disallowing_a_fast_io_operation_in_a_preoperation_callback_routine"></span><span id="DDK_DISALLOWING_A_FAST_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE"></span>


場合によっては、ミニフィルタードライバーでは、実行するのではなく、高速の i/o 操作を許可しないことがあります。 高速 i/o 操作を禁止すると、高速な i/o パスを操作に使用できなくなります。

I/o 操作の完了と同様に、高速な i/o 操作を禁止するということは、処理を停止し、フィルターマネージャーに返すことを意味します。 ただし、高速の i/o 操作を許可しないことは、その処理を完了することとは異なります。 ミニフィルタードライバーで i/o マネージャーによって発行された高速 i/o 操作が禁止されている場合、i/o マネージャーは、同等の IRP ベースの操作と同じ操作を再実行することがあります。

ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)で高速 i/o 操作が禁止されている場合、フィルターマネージャーは次の処理を実行します。

-   は、現在のミニフィルタードライバー、レガシフィルター、またはファイルシステムの下にあるミニフィルタードライバーに操作を送信しません。

-   ミニフィルタードライバーインスタンススタック内の現在のミニフィルタードライバーの前にあるミニ[**操作コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を呼び出します。

-   は、現在のミニフィルタードライバーの postoperation コールバックルーチンが存在する場合、その操作を呼び出しません。

ミニフィルタードライバーでは、FLT\_PREOP\_を返すことによって、操作の preop コールバックルーチンからの\_FAO を許可しないようにすることで、高速な i/o 操作を行うことができません。

Preoperation コールバックルーチンは、コールバックデータ構造の FLT フィールドを設定しないでください **。** フィルターマネージャーによって、このフィールドが自動的に status\_\_設定され、高速\_IO\_は許可されません。

FLT\_PREOP\_\_許可されていない高速 i/o 操作の場合にのみ返すことができます。 操作が高速 i/o 操作であるかどうかを確認するには、「 [**FLT\_is\_faan o\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

ミニフィルタードライバーは、FLT\_PREOP\_を返すことができません。 IRP\_MJ\_SHUTDOWN、IRP\_MJ\_VOLUME\_MOUNT、または IRP\_MJ\_VOLUME\_のマウント解除操作で、\_FAを許可しません。

 

 




