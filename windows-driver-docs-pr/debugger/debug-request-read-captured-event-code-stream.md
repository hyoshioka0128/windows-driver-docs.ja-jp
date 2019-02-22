---
title: デバッグ\_要求\_読み取り\_CAPTURED\_イベント\_コード\_ストリーム
description: デバッグ\_要求\_読み取り\_CAPTURED\_イベント\_コード\_ストリーム
ms.assetid: 867c6b3e-13d5-46ae-b73c-f90936cb35c5
keywords:
- デバッグ DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5d08c61fe7014d5b3fc04c200f882e795693a78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558607"
---
# <a name="debugrequestreadcapturedeventcodestream"></a>デバッグ\_要求\_読み取り\_CAPTURED\_イベント\_コード\_ストリーム


デバッグ\_要求\_読み取り\_CAPTURED\_イベント\_コード\_ストリーム[**要求**](request.md)まで操作を返します現在のイベントの命令ポインターのメモリの 64 バイトです。

**パラメーター**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
現在のイベントの命令ポインターのメモリ。 最大で 64 バイトのメモリは、返される可能性があります。

<a name="remarks"></a>注釈
-------

メモリのスナップショットをイベントが発生したときに、メモリが返されます。 変更が行われたターゲットのメモリにイベント以降は反映されません。

現在のイベントの命令ポインターがによって返される、 [**要求**](request.md)操作[**デバッグ\_要求\_取得\_キャプチャ\_イベント\_コード\_オフセット**](debug-request-get-captured-event-code-offset.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット**](debug-request-get-captured-event-code-offset.md)

 

 






