---
title: FLT_PREOP_SUCCESS_NO_CALLBACK が返される場合
description: FLT_PREOP_SUCCESS_NO_CALLBACK が返される場合
ms.assetid: cde708b0-b572-4444-ba4b-158b6906884e
keywords:
- FLT_PREOP_SUCCESS_NO_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed11d5ace93beb67fb08c70005538ce306367ebd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344570"
---
# <a name="returning-fltpreopsuccessnocallback"></a>返す FLT\_PREOP\_成功\_いいえ\_コールバック


## <span id="ddk_returning_flt_preop_success_no_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_NO_CALLBACK_IF"></span>


ミニフィルター ドライバーの場合[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)返します FLT\_PREOP\_成功\_いいえ\_コールバック、フィルター マネージャーがありませんミニフィルター ドライバーの呼び出す[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)I/O の完了時に存在する場合は、します。

ミニフィルター ドライバーの preoperation 場合、コールバック ルーチンは FLT を返します\_PREOP\_成功\_いいえ\_返す必要があります、コールバック**NULL**でその*CompletionContext*出力パラメーター。

FLT\_PREOP\_成功\_いいえ\_すべての種類の I/O 操作のコールバック状態値を返すことができます。

 

 




