---
title: I/o 操作をミニフィルタードライバーインスタンススタックに渡す
description: 下のミニフィルター ドライバー インスタンス スタックへ I/O 操作を渡す
ms.assetid: b2661e1e-2190-4def-be6c-27057c631304
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニパス、ドライバーインスタンススタックの引き渡し
- i/o 操作をミニフィルタドライバースタック WDK ファイルシステムに渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b76b17d9f2663a04777f799b524043460cbe7f47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841044"
---
# <a name="passing-io-operations-down-the-minifilter-driver-instance-stack"></a>I/o 操作をミニフィルタードライバーインスタンススタックに渡す


## <span id="ddk_passing_an_io_operation_down_the_minifilter_instance_stack_if"></span><span id="DDK_PASSING_AN_IO_OPERATION_DOWN_THE_MINIFILTER_INSTANCE_STACK_IF"></span>


ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)または作業ルーチンがフィルターマネージャーに i/o 操作を返すと、フィルターマネージャーは、ミニフィルタードライバーインスタンススタック内の現在のミニフィルタードライバーの下にあるミニフィルタードライバーに操作を送信します。

ミニフィルタードライバーの preoperation コールバックルーチンは、次のいずれかの状態値を返すことによって、後続の処理のために i/o 操作をフィルターマネージャーに返します。

-   FLT\_PREOP\_SUCCESS\_\_コールバックなし (すべての操作の種類)

-   FLT\_PREOP\_成功\_と\_コールバック (すべての操作の種類)

-   FLT\_PREOP\_SYNCHRONIZE (IRP ベースの i/o 操作のみ)

**注**  \_preop\_SYNCHRONIZE は、IRP ベースの i/o 操作に対してのみ返される必要がありますが、他の操作の種類については、この状態の値を返すことができます。 IRP ベースの i/o 操作ではない i/o 操作に対して返された場合、フィルターマネージャーは、この戻り値を\_コールバックと共に\_PREOP\_成功\_として扱います。

 

別の方法として、preoperation コールバックルーチンで保留されていた操作の作業ルーチンが、 [**Fltcompletependedpreoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)を呼び出して、保留中の i/o 操作の処理を再開するときに、その前の状態値の1つをコールバック*ステータス*パラメーターに渡すことによって、フィルターマネージャーに i/o 操作を返します。

このセクションの内容:

[\_コールバックで FLT\_PREOP\_SUCCESS\_を返す](returning-flt-preop-success-with-callback.md)

[FLT\_PREOP\_SUCCESS\_\_コールバックなしで返す](returning-flt-preop-success-no-callback.md)

[FLT\_PREOP\_SYNCHRONIZE を返す](returning-flt-preop-synchronize.md)

 

 




