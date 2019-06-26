---
title: SRB\_読み取り\_データ
description: SRB\_読み取り\_データ
ms.assetid: b59d705d-5215-42ee-85cf-369a2e69f99b
keywords:
- SRB_READ_DATA ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_READ_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb81167225ba568a003db556f408f1264b095426
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377876"
---
# <a name="srbreaddata"></a>SRB\_読み取り\_データ


## <span id="ddk_srb_read_data_ks"></span><span id="DDK_SRB_READ_DATA_KS"></span>


クラス ドライバーは、ミニドライバーの読み取り要求を受信しました。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、次のいずれかを SRB の状態として設定できますか、メモリ エラーや不適切なパラメーターなどのエラー状況を示す追加のエラー コードを渡すことができます。 クラス ドライバーの状態についてのみチェック\_成功します。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

値*pSrb*-&gt;**CommandData**.**DataBufferArray**の配列を指す[ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造体は、データ バッファーをまとめて説明します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。 *pSrb*-&gt;**CommandData**.**NumberOfBuffers**配列のサイズを指定します。

**ときに、SRB\_読み取り\_データ コマンドが、ミニドライバーによって受信されると、応答のミニドライバー ルーチンにする必要があります。**

1.  現在のストリームの状態を判断することを確認します。 ミニドライバーは、一時停止または実行の状態のときに読み取り要求のみを受け入れる必要があります。 ストリームが停止している場合、すぐに完了して、SRB を返します。

2.  SRB をキューに配置します。

 

 





