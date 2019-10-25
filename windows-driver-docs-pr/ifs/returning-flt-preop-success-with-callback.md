---
title: FLT_PREOP_SUCCESS_WITH_CALLBACK が返される場合
description: FLT_PREOP_SUCCESS_WITH_CALLBACK が返される場合
ms.assetid: 6247b952-3189-4792-a15b-c3a4b3dc80ae
keywords:
- FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bff93862bf17d9472c5ea2e6ea5eaaf7654f8c27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840994"
---
# <a name="returning-flt_preop_success_with_callback"></a>\_コールバックで FLT\_PREOP\_SUCCESS\_を返す


## <span id="ddk_returning_flt_preop_success_with_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_WITH_CALLBACK_IF"></span>


ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)が\_コールバックで FLT\_preoperation\_SUCCESS\_を返した場合、フィルターマネージャーは、i/o 中にミニフィルタードライバーの[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を呼び出します。完了.

ミニフィルタードライバーの preoperation コールバックルーチンが\_コールバックで FLT\_PREOPERATION\_SUCCESS\_を返したが、ミニフィルタードライバーが操作の postoperation コールバックルーチンを登録していない場合**は  ** システムは、チェックされたビルドをアサートします。

 

ミニフィルタードライバーの preoperation コールバックルーチンが\_コールバックと共に FLT\_PREOPERATION\_SUCCESS\_を返す場合 *、その完了後の出力パラメーター*で NULL 以外の値を返すことができます。 このパラメーターは、対応する postoperation コールバックルーチンに渡される省略可能なコンテキストポインターです。 Postoperation コールバックルーチンは、このポインターを完了後*の入力パラメーター*に受け取ります。

\_コールバック状態値を使用した FLT\_PREOP\_SUCCESS\_は、すべての種類の i/o 操作に対して返すことができます。

 

 




