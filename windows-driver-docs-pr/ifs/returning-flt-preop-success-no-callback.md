---
title: FLT_PREOP_SUCCESS_NO_CALLBACK が返される場合
description: FLT_PREOP_SUCCESS_NO_CALLBACK が返される場合
ms.assetid: cde708b0-b572-4444-ba4b-158b6906884e
keywords:
- FLT_PREOP_SUCCESS_NO_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f178fb5676bad3424b757b98442ef086171dc492
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840999"
---
# <a name="returning-flt_preop_success_no_callback"></a>FLT\_PREOP\_SUCCESS\_\_コールバックなしで返す


## <span id="ddk_returning_flt_preop_success_no_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_NO_CALLBACK_IF"></span>


ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)が、FLT\_preoperation\_SUCCESS\_\_コールバックを返さない場合、フィルタマネージャはミニフィルタドライバの[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を呼び出しません (存在する場合)。i/o の完了時。

ミニフィルタードライバーの preoperation コールバックルーチンが、FLT\_PREOPERATION\_SUCCESS\_\_コールバックを返さない場合は、*その実行元の*出力パラメーターで**NULL**を返す必要があります。

FLT\_PREOP\_SUCCESS\_\_コールバック状態値は、すべての種類の i/o 操作に対して返すことができます。

 

 




