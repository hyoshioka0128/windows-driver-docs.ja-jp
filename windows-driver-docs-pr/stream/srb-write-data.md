---
title: SRB\_書き込み\_データ
description: SRB\_書き込み\_データ
ms.assetid: f7867185-3f1b-4c83-b23a-5b2b4ce6e484
keywords:
- SRB_WRITE_DATA ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_WRITE_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9c83b23fbd4e1acad95d3f6ac8c8d8a0a036cf6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377847"
---
# <a name="srbwritedata"></a>SRB\_書き込み\_データ


## <span id="ddk_srb_write_data_ks"></span><span id="DDK_SRB_WRITE_DATA_KS"></span>


クラス ドライバーは、ミニドライバーの書き込み要求を受信しました。 値*pSrb*-&gt;**CommandData**.**DataBufferArray**の配列を指す[ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造体は、データ バッファーをまとめて説明します。 値*pSrb*-&gt;**CommandData**.**NumberOfBuffers**配列のサイズを指定します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、次のいずれかを SRB の状態として設定できますか、メモリ エラーや不適切なパラメーターなどのエラー状況を示す追加のエラー コードを渡すことができます。 クラス ドライバーは、状態にのみ関係\_成功します。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

## <a name="see-also"></a>関連項目


[**SRB\_設定\_ストリーム\_状態**](srb-set-stream-state.md)

 

 






