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
ms.openlocfilehash: 0c6f2750b6c9713d27d4d7bbdbfe1e4502d52884
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349046"
---
# <a name="debugrequestsetlocalimplicitcommandline"></a>デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行


デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行[**要求**](request.md)操作、を設定します。[デバッガー エンジン](https://msdn.microsoft.com/library/windows/hardware/ff551059#debugger-engine)の暗黙的なコマンドライン。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新しい暗黙的なコマンドライン。 型*InBuffer* Unicode 文字列 (PWSTR) へのポインターです。 ポインターのコピーが指す文字列はコピーされません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
使用されていません。

<a name="remarks"></a>注釈
-------

暗黙的なコマンド ラインは、プロセスを作成するときに、コマンドラインとして使用できます。 プロセス作成のオプション ([**デバッグ\_作成\_プロセス\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff541464)) ではなく、指定された暗黙のコマンドラインを使用するためのオプションを含めるコマンド ライン プロセスを作成するときにします。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff541464)

[**デバッグ\_要求\_取得\_追加\_作成\_オプション**](debug-request-get-additional-create-options.md)

[**デバッグ\_要求\_設定\_追加\_作成\_オプション**](debug-request-set-additional-create-options.md)

[**CreateProcess2**](https://msdn.microsoft.com/library/windows/hardware/ff539323)

[**CreateProcessAndAttach2**](https://msdn.microsoft.com/library/windows/hardware/ff540055)

 

 






