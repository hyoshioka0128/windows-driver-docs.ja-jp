---
title: デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット
description: デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット
ms.assetid: cdf05d4f-8a8c-4b52-b36f-9d00575fdb7b
keywords:
- デバッグ DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc9569206a346f5b1025e77295cb7a3c0a10e073
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361430"
---
# <a name="debugrequestgetcapturedeventcodeoffset"></a>デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット


デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット[**要求**](request.md)操作は戻り、現在のイベントの命令ポインター。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されていません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
現在のイベントの命令ポインター。 命令ポインターの型は、ULONG64 です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

<span id="S_OK"></span><span id="s_ok"></span>S\_OK  
メソッドが正常に完了しました。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E\_NOINTERFACE  
現在のイベントの命令ポインターのメモリが無効です。

このメソッドは、エラー値を返すも可能性があります。 参照してください[**戻り値**](https://docs.microsoft.com/windows-hardware/drivers/debugger/hresult-values)の詳細。

<a name="remarks"></a>注釈
-------

使用して、現在のイベントの命令ポインターのメモリを読み取ることができます、 [**要求**](request.md)操作の[**デバッグ\_要求\_読み取り\_CAPTURED\_イベント\_コード\_ストリーム**](debug-request-read-captured-event-code-stream.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**デバッグ\_要求\_読み取り\_CAPTURED\_イベント\_コード\_ストリーム**](debug-request-read-captured-event-code-stream.md)

 

 






