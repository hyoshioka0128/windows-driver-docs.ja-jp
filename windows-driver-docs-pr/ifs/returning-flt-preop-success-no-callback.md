---
title: FLT_PREOP_SUCCESS_NO_CALLBACK が返される場合
description: FLT_PREOP_SUCCESS_NO_CALLBACK が返される場合
ms.assetid: cde708b0-b572-4444-ba4b-158b6906884e
keywords:
- FLT_PREOP_SUCCESS_NO_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e42dd37a7b69b7b39721ebf4ec711d4a2a422bce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379490"
---
# <a name="returning-fltpreopsuccessnocallback"></a>返す FLT\_PREOP\_成功\_いいえ\_コールバック


## <span id="ddk_returning_flt_preop_success_no_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_NO_CALLBACK_IF"></span>


ミニフィルター ドライバーの場合[ **preoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)返します FLT\_PREOP\_成功\_いいえ\_コールバック、フィルター マネージャーがありませんミニフィルター ドライバーの呼び出す[ **postoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)I/O の完了時に存在する場合は、します。

ミニフィルター ドライバーの preoperation 場合、コールバック ルーチンは FLT を返します\_PREOP\_成功\_いいえ\_返す必要があります、コールバック**NULL**でその*CompletionContext*出力パラメーター。

FLT\_PREOP\_成功\_いいえ\_すべての種類の I/O 操作のコールバック状態値を返すことができます。

 

 




