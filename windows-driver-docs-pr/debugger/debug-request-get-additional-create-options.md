---
title: デバッグ\_要求\_\_追加\_\_オプションの制御コードを作成する
description: デバッグ\_要求\_\_\_GET\_OPTIONS 要求操作を作成すると、既定のプロセス作成オプションが返されます。
ms.assetid: ad4c98d9-ca4e-4ee3-a177-2fe04a8f22e2
keywords:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS コントロールコードの Windows デバッグ
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8a95b7d04171960dc980a4d83250c52ec6832ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837791"
---
# <a name="debug_request_get_additional_create_options-control-code"></a>デバッグ\_要求\_\_追加\_\_オプションの制御コードを作成する


デバッグ\_要求\_\_\_GET\_OPTIONS[**要求**](request.md)操作を作成すると、既定のプロセス作成オプションが返されます。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用しません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
既定のプロセス作成オプション。 プロセス作成オプションの種類は、[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)です。

<a name="remarks"></a>注釈
-------

既定のプロセス作成オプションは、 [**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)および[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)メソッドによって使用されます。このメソッドは、 [**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)や[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)とは異なり、プロセス作成オプションのすべての範囲を指定するわけではありません。

[**DEBUG\_CREATE\_process\_OPTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)構造体の**createflags**フィールドは、すべてのプロセス作成操作でこの情報が提供されるため、既定値としては使用されません。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**申請**](request.md)

[**デバッグ\_要求\_設定\_追加\_\_オプションを作成する**](debug-request-set-additional-create-options.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

 






