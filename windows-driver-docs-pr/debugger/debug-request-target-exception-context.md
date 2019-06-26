---
title: デバッグ\_要求\_ターゲット\_例外\_コンテキスト
description: デバッグ\_要求\_ターゲット\_例外\_コンテキスト
ms.assetid: e599a3f7-110b-46fc-8266-3a00ea1efe03
keywords:
- デバッグ DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a48ec1f66ebb7997ac545bbe88d3688fadfaf7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366969"
---
# <a name="debugrequesttargetexceptioncontext"></a>デバッグ\_要求\_ターゲット\_例外\_コンテキスト


デバッグ\_要求\_ターゲット\_例外\_コンテキスト[**要求**](request.md)操作は戻り、[スレッド コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context)ユーザー モードのミニダンプ ファイル ストアド イベント。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されていません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
ストアドのイベントのスレッド コンテキスト。 スレッド コンテキストの種類は、イベントの時点で、ターゲットの有効なプロセッサのコンテキスト構造です。 *OutBuffer*この構造体を保持するために十分な大きさである必要があります。

<a name="remarks"></a>注釈
-------

この情報にも返されます、*コンテキスト*パラメーターによって、 [ **GetStoredEventInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)メソッド。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**GetStoredEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)

 

 






