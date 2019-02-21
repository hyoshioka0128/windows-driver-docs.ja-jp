---
title: SRB\_設定\_ストリーム\_状態
description: SRB\_設定\_ストリーム\_状態
ms.assetid: 8dd1237c-3b3e-4207-96b8-22311968c3a0
keywords:
- SRB_SET_STREAM_STATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_SET_STREAM_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c48cbb6d2d0d813bc5c85b0a0a6c18401e5bb1e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552909"
---
# <a name="srbsetstreamstate"></a>SRB\_設定\_ストリーム\_状態


## <span id="ddk_srb_set_stream_state_ks"></span><span id="DDK_SRB_SET_STREAM_STATE_KS"></span>


クラスのドライバーでは、このストリームのストリームの状態を設定するには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスのドライバーで、新しいストリームの状態を指定する*pSrb*-&gt;**CommandData**.**StreamState**します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)構造体。 参照してください[ **KSPROPERTY\_接続\_状態**](ksproperty-connection-state.md)ストリームの状態の説明についてはします。

ミニドライバーがストリームを指定した状態に設定する必要があり、状態を返す\_成功した場合は成功します。 操作が失敗した場合、適切なエラー コードが返されます。

## <a name="see-also"></a>関連項目


[SRB\_取得\_ストリーム\_状態](srb-get-stream-state.md)

 

 






