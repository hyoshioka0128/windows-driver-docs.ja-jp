---
title: SRB\_\_データの書き込み
description: SRB\_\_データの書き込み
ms.assetid: f7867185-3f1b-4c83-b23a-5b2b4ce6e484
keywords:
- SRB_WRITE_DATA ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_WRITE_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633b5e567fb32965eef2f2d01580acfa283fb806
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837697"
---
# <a name="srb_write_data"></a>SRB\_\_データの書き込み


## <span id="ddk_srb_write_data_ks"></span><span id="DDK_SRB_WRITE_DATA_KS"></span>


クラスドライバーは、ミニドライバーの書き込み要求を受け取りました。 *PSrb*の値-**commanddata**&gt;ます。**DataBufferArray**は、データバッファーについて説明する[**KSK ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体の配列を指します。 *PSrb*の値-**commanddata**&gt;ます。**Numberofbuffers**は配列のサイズを指定します。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定できます。また、メモリエラーや無効なパラメーターなどのエラー状況を示すために、追加のエラーコードを渡すこともできます。 クラスドライバーは、STATUS\_SUCCESS のみに関係しています。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

## <a name="see-also"></a>関連項目


[**SRB\_設定\_ストリーム\_の状態**](srb-set-stream-state.md)

 

 






