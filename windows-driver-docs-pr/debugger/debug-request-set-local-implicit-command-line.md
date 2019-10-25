---
title: デバッグ\_要求\_ローカル\_暗黙的\_コマンド\_行\_設定します
description: デバッグ\_要求\_ローカル\_暗黙的\_コマンド\_行\_設定します
ms.assetid: c54fc9f3-2805-4411-8162-18d4f9983795
keywords:
- DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE Windows のデバッグ
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3529e081b8f42125626cf2b48165496cf9cdd497
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837785"
---
# <a name="debug_request_set_local_implicit_command_line"></a>デバッグ\_要求\_ローカル\_暗黙的\_コマンド\_行\_設定します


DEBUG\_要求\_設定\_ローカル\_暗黙の\_コマンド\_ライン[**要求**](request.md)操作[デバッガーエンジン](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)の暗黙的なコマンドラインを設定します。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新しい暗黙的なコマンドライン。 *Inbuffer*の型は、Unicode 文字列 (PWSTR) へのポインターです。 ポインターはコピーされますが、ポインターが指す文字列はコピーされません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
使用しません。

<a name="remarks"></a>注釈
-------

プロセスを作成するときに、コマンドラインとして暗黙的なコマンドラインを使用できます。 プロセス作成オプション ([**デバッグ\_CREATE\_process\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)) には、プロセスの作成時に指定したコマンドラインではなく、暗黙的なコマンドラインを使用するオプションが含まれています。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**申請**](request.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**デバッグ\_要求\_追加\_\_オプションを作成\_** ](debug-request-get-additional-create-options.md)

[**デバッグ\_要求\_設定\_追加\_\_オプションを作成する**](debug-request-set-additional-create-options.md)

[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)

[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)

 

 






