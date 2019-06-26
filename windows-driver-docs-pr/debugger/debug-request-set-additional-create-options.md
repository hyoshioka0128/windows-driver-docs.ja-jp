---
title: デバッグ\_要求\_設定\_追加\_作成\_オプション
description: デバッグ\_要求\_設定\_追加\_作成\_オプション
ms.assetid: e80f8575-b7f9-466a-8087-b3cb103503f7
keywords:
- デバッグ DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27f98567ed627f5b64647a5d54d2ff499b516f89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366986"
---
# <a name="debugrequestsetadditionalcreateoptions"></a>デバッグ\_要求\_設定\_追加\_作成\_オプション


デバッグ\_要求\_設定\_追加\_作成\_オプション[**要求**](request.md)操作は、既定のプロセスの作成を設定します。オプション。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新しい既定のプロセスの作成オプション。 プロセスの作成オプションの種類は[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)します。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
使用されていません。

<a name="remarks"></a>注釈
-------

既定のプロセス作成のオプションがメソッドで使用される[ **CreateProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess)と[ **CreateProcessAndAttach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach) とは異なり、この[**CreateProcess2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess2)と[ **CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)、プロセス作成オプションの完全な範囲を指定しません。

**CreateFlags**のフィールド、 [**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)ために、構造体は、既定値として使用されませんすべてプロセス作成操作では、この情報を提供します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**デバッグ\_要求\_取得\_追加\_作成\_オプション**](debug-request-get-additional-create-options.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

 






