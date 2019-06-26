---
title: SRB\_閉じる\_ストリーム
description: SRB\_閉じる\_ストリーム
ms.assetid: e118ddd7-fe0e-4834-9ae6-19eef0348b2c
keywords:
- SRB_CLOSE_STREAM ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_CLOSE_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 993d6d26d733b49dc31e116d0653232b25d069fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358381"
---
# <a name="srbclosestream"></a>SRB\_閉じる\_ストリーム


## <span id="ddk_srb_close_stream_ks"></span><span id="DDK_SRB_CLOSE_STREAM_KS"></span>


クラスのドライバーでは、ストリームを閉じるには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラス ドライバーを提供する[ **HW\_ストリーム\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_object)内でバッファー *pSrb* - &gt; **StreamObject**で*pSrb*-&gt;**StreamObject**-&gt;**StreamNumber**閉じるストリームの数に設定します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。 **StreamNumber**内のストリームのオフセットに対応する、 [ **HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)構造体への応答で、ミニドライバーを提供する、[ **SRB\_取得\_ストリーム\_情報**](srb-get-stream-info.md)要求。

ミニドライバーに状態が返されます場合、ミニドライバーは、正常にストリームを閉じ、\_成功します。 それ以外の場合、適切なエラー状態を返します。

**ときに、SRB\_閉じる\_ストリーム コマンドが、ミニドライバーによって受信されると、応答のミニドライバー ルーチンにする必要があります。**

1.  ストリームを開いたときに、ミニドライバーによって割り当てられているリソースを解放します。

2.  ストリームのクロックを使用した場合、クロックの参照を停止します。

3.  停止する、ストリームの状態をリセットします。

関連付けられているユーザー モード アプリケーションがクラッシュした場合のストリーミング中にストリームを任意に閉じだったことに注意してください。 そのため、ストリームのすべての優れたリソースを解放、ストリームのすべての保留される Srb の完了、およびストリームを休止状態に戻す必要があります。

 

 





