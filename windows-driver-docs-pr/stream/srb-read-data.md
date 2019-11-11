---
title: SRB\_読み取り\_データ
description: SRB\_読み取り\_データ
ms.assetid: b59d705d-5215-42ee-85cf-369a2e69f99b
keywords:
- SRB_READ_DATA ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_READ_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f9daf3bbcbe6df3d124767100e2f7c33a0254e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837711"
---
# <a name="srb_read_data"></a>SRB\_読み取り\_データ


## <span id="ddk_srb_read_data_ks"></span><span id="DDK_SRB_READ_DATA_KS"></span>


クラスドライバーは、ミニドライバーの読み取り要求を受け取りました。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定できます。また、メモリエラーや無効なパラメーターなどのエラー状況を示すために、追加のエラーコードを渡すこともできます。 クラスドライバーは、ステータス\_成功したかどうかのみをチェックします。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

*PSrb*の値-**commanddata**&gt;ます。**DataBufferArray**は、データバッファーについて説明する[**KSK ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体の配列を指します。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。 *pSrb*-**commanddata**&gt;ます。**Numberofbuffers**は配列のサイズを指定します。

**SRB\_READ\_DATA コマンドがミニドライバーによって受信されると、応答するミニドライバールーチンは次のようになります。**

1.  現在のストリームの状態を確認する場合にチェックします。 ミニドライバーは、一時停止または実行状態のときにのみ読み取り要求を受け入れる必要があります。 ストリームが停止している場合は、すぐに完了し、SRB を返します。

2.  SRB をキューに配置します。

 

 





