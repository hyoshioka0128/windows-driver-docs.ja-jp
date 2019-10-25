---
title: SRB\_設定\_ストリーム\_の状態
description: SRB\_設定\_ストリーム\_の状態
ms.assetid: 8dd1237c-3b3e-4207-96b8-22311968c3a0
keywords:
- SRB_SET_STREAM_STATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_SET_STREAM_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffc2e56ad0f13f607728bc35391479cbf309b139
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837704"
---
# <a name="srb_set_stream_state"></a>SRB\_設定\_ストリーム\_の状態


## <span id="ddk_srb_set_stream_state_ks"></span><span id="DDK_SRB_SET_STREAM_STATE_KS"></span>


クラスドライバーは、この要求を送信して、このストリームのストリームの状態を設定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスドライバーは、 *pSrb*-&gt;**commanddata**に新しいストリームの状態を指定します。**Streamstate**。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。 ストリームの状態の説明については、「 [**Ksk プロパティ\_接続\_状態**](ksproperty-connection-state.md)」を参照してください。

ミニドライバーは、ストリームを指定された状態に設定し、正常に終了した場合は\_状態を返すようにする必要があります。 操作が失敗した場合は、適切なエラーコードが返されます。

## <a name="see-also"></a>関連項目


[SRB\_\_ストリーム\_状態の取得](srb-get-stream-state.md)

 

 






