---
title: デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行
description: デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行
ms.assetid: c54fc9f3-2805-4411-8162-18d4f9983795
keywords:
- デバッグ DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 430960b284f37f3d9a63623485adf1d212a8cbd4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361432"
---
# <a name="debugrequestsetlocalimplicitcommandline"></a>デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行


デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行[**要求**](request.md)操作、を設定します。[デバッガー エンジン](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)の暗黙的なコマンドライン。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新しい暗黙的なコマンドライン。 型*InBuffer* Unicode 文字列 (PWSTR) へのポインターです。 ポインターのコピーが指す文字列はコピーされません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
使用されていません。

<a name="remarks"></a>注釈
-------

暗黙的なコマンド ラインは、プロセスを作成するときに、コマンドラインとして使用できます。 プロセス作成のオプション ([**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)) ではなく、指定された暗黙のコマンドラインを使用するためのオプションを含めるコマンド ライン プロセスを作成するときにします。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)

[**デバッグ\_要求\_取得\_追加\_作成\_オプション**](debug-request-get-additional-create-options.md)

[**デバッグ\_要求\_設定\_追加\_作成\_オプション**](debug-request-set-additional-create-options.md)

[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess2)

[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)

 

 






