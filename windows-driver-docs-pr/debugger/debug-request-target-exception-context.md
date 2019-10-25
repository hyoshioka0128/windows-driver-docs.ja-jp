---
title: デバッグ\_要求\_ターゲット\_例外\_コンテキスト
description: デバッグ\_要求\_ターゲット\_例外\_コンテキスト
ms.assetid: e599a3f7-110b-46fc-8266-3a00ea1efe03
keywords:
- DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT Windows のデバッグ
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d1047beb623879bf8af9abb9c9b26c57c56a334
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837780"
---
# <a name="debug_request_target_exception_context"></a>デバッグ\_要求\_ターゲット\_例外\_コンテキスト


デバッグ\_要求\_ターゲット\_の例外\_コンテキスト[**要求**](request.md)操作は、ユーザーモードのミニダンプファイルに格納されているイベントの[スレッドコンテキスト](https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context)を返します。

**パラメーター**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
格納されているイベントのスレッドコンテキスト。 スレッドコンテキストの型は、イベント発生時のターゲットの有効なプロセッサのコンテキスト構造です。 *Outbuffer*は、この構造体を保持するのに十分な大きさである必要があります。

<a name="remarks"></a>解説
-------

この情報は、 [**GetStoredEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)メソッドによって*コンテキスト*パラメーターにも返されます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**Request**](request.md)

[**GetStoredEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)

 

 






