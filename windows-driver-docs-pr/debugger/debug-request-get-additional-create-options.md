---
title: デバッグ\_要求\_取得\_追加\_作成\_オプションは、コードを制御します。
description: デバッグ\_要求\_取得\_追加\_作成\_オプションの要求操作は、既定のプロセスの作成オプションを返します。
ms.assetid: ad4c98d9-ca4e-4ee3-a177-2fe04a8f22e2
keywords:
- Windows デバッグ DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS 制御コード
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdaa08e09d698a35eb80bbaedba641447191d6ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366976"
---
# <a name="debugrequestgetadditionalcreateoptions-control-code"></a>デバッグ\_要求\_取得\_追加\_作成\_オプションは、コードを制御します。


デバッグ\_要求\_取得\_追加\_作成\_オプション[**要求**](request.md)操作は、既定のプロセスを返します作成オプション。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されていません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
既定のプロセス作成のオプション。 プロセスの作成オプションの種類は[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)します。

<a name="remarks"></a>注釈
-------

既定のプロセス作成のオプションがメソッドで使用される[ **CreateProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess)と[ **CreateProcessAndAttach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach) とは異なり、この[**CreateProcess2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess2)と[ **CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)、プロセス作成オプションの完全な範囲を指定しません。

**CreateFlags**のフィールド、 [**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)ために、構造体は、既定値として使用されませんすべてプロセス作成操作では、この情報を提供します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**デバッグ\_要求\_設定\_追加\_作成\_オプション**](debug-request-set-additional-create-options.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

 






