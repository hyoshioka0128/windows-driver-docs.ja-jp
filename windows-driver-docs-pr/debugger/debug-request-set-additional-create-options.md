---
title: デバッグ\_要求\_設定\_追加\_\_オプションを作成する
description: デバッグ\_要求\_設定\_追加\_\_オプションを作成する
ms.assetid: e80f8575-b7f9-466a-8087-b3cb103503f7
keywords:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS Windows のデバッグ
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8818fecff5db9e900d14984477637afb2b778ca9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837789"
---
# <a name="debug_request_set_additional_create_options"></a>デバッグ\_要求\_設定\_追加\_\_オプションを作成する


[デバッグ\_要求\_設定]\_追加\_CREATE\_OPTIONS[**要求**](request.md)操作は、既定のプロセス作成オプションを設定します。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新しい既定のプロセス作成オプション。 プロセス作成オプションの種類は、[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)です。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
使用しません。

<a name="remarks"></a>注釈
-------

既定のプロセス作成オプションは、 [**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)および[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)メソッドによって使用されます。このメソッドは、 [**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)や[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)とは異なり、プロセス作成オプションのすべての範囲を指定するわけではありません。

[**DEBUG\_CREATE\_process\_OPTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)構造体の**createflags**フィールドは、すべてのプロセス作成操作でこの情報が提供されるため、既定値としては使用されません。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**申請**](request.md)

[**デバッグ\_要求\_追加\_\_オプションを作成\_** ](debug-request-get-additional-create-options.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

 






