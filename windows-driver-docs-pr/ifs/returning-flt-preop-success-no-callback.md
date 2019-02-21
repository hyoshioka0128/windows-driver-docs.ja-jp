---
title: FLT_PREOP_SUCCESS_NO_CALLBACK を返す
description: FLT_PREOP_SUCCESS_NO_CALLBACK を返す
ms.assetid: cde708b0-b572-4444-ba4b-158b6906884e
keywords:
- FLT_PREOP_SUCCESS_NO_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed11d5ace93beb67fb08c70005538ce306367ebd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528705"
---
# <a name="returning-fltpreopsuccessnocallback"></a>返す FLT\_PREOP\_成功\_いいえ\_コールバック


## <span id="ddk_returning_flt_preop_success_no_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_NO_CALLBACK_IF"></span>


ミニフィルター ドライバーの場合[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)返します FLT\_PREOP\_成功\_いいえ\_コールバック、フィルター マネージャーがありませんミニフィルター ドライバーの呼び出す[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)I/O の完了時に存在する場合は、します。

ミニフィルター ドライバーの preoperation 場合、コールバック ルーチンは FLT を返します\_PREOP\_成功\_いいえ\_返す必要があります、コールバック**NULL**でその*CompletionContext*出力パラメーター。

FLT\_PREOP\_成功\_いいえ\_すべての種類の I/O 操作のコールバック状態値を返すことができます。

 

 




