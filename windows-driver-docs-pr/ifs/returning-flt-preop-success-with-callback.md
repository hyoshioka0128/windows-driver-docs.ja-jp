---
title: FLT_PREOP_SUCCESS_WITH_CALLBACK が返される場合
description: FLT_PREOP_SUCCESS_WITH_CALLBACK が返される場合
ms.assetid: 6247b952-3189-4792-a15b-c3a4b3dc80ae
keywords:
- FLT_PREOP_SUCCESS_WITH_CALLBACK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fc40035213be28d241e590c6b96f6dc065c69d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344562"
---
# <a name="returning-fltpreopsuccesswithcallback"></a>返す FLT\_PREOP\_成功\_WITH\_コールバック


## <span id="ddk_returning_flt_preop_success_with_callback_if"></span><span id="DDK_RETURNING_FLT_PREOP_SUCCESS_WITH_CALLBACK_IF"></span>


ミニフィルター ドライバーの場合[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)返します FLT\_PREOP\_成功\_WITH\_コールバック、フィルター マネージャーの呼び出しミニフィルター ドライバーの[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107) I/O の完了時にします。

**注**  コールバック ルーチンが FLT を返す場合ミニフィルター ドライバーの preoperation\_PREOP\_成功\_WITH\_コールバックがミニフィルター ドライバーが登録されていない、操作の postoperation コールバック ルーチン、システムは、チェック ビルドにアサートします。

 

ミニフィルター ドライバーの preoperation 場合、コールバック ルーチンは FLT を返します\_PREOP\_成功\_WITH\_コールバックに NULL 以外の値を返すことの*CompletionContext*出力パラメーター。 このパラメーターは、対応する postoperation コールバック ルーチンに渡される省略可能なコンテキスト ポインターです。 Postoperation コールバック ルーチンでは、このポインターを受け取るその*CompletionContext*入力パラメーター。

FLT\_PREOP\_成功\_WITH\_すべての種類の I/O 操作のコールバック状態値を返すことができます。

 

 




