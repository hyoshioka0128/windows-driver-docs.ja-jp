---
title: SRB\_\_ストリーム\_情報の取得
description: SRB\_\_ストリーム\_情報の取得
ms.assetid: ff5412ee-6e4f-43f4-a90d-4a2bdfa5d4ae
keywords:
- SRB_GET_STREAM_INFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_GET_STREAM_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1deced6611edcd29ba91870d1abe51082175889
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843302"
---
# <a name="srb_get_stream_info"></a>SRB\_\_ストリーム\_情報の取得


## <span id="ddk_srb_get_stream_info_ks"></span><span id="DDK_SRB_GET_STREAM_INFO_KS"></span>


クラスドライバーは、この要求を送信して、デバイスとそれがサポートするストリームの説明を取得します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスドライバーは、クラスドライバーの[**SRB\_INITIALIZE\_デバイス**](srb-initialize-device.md)要求に応答して、ミニドライバーによって指定されたサイズの*pSrb*&gt;-にバッファーを渡します **。** *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。 「[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_port_configuration_information)」も参照してください。

ミニドライバーは、デバイスとそれがサポートするストリームを記述する[**HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)を使用して**Commanddata. streambuffer**を読み込みます。 このバッファーのサイズは、[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_port_configuration_information)構造体の**streamミニドライバー size**フィールドの値によって示されます。

クラスドライバーは通常、この要求を1回だけ発行します。 ミニドライバーは、 [StreamClassReenumerateStreams](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassreenumeratestreams)を呼び出して、サポートされているストリームの説明を更新するために、クラスドライバーがこの要求を強制的に再発行する場合があります。

**SRB\_GET\_STREAM\_INFO コマンドがミニドライバーによって受信されると、ミニドライバーは次のことを行う必要があります。**

1.  ストリームヘッダーおよびストリーム情報のデータ構造のポインターを取得します。 次に、例を示します。

    ```cpp
     PHW_STREAM_HEADER pstrhdr =
      (PHW_STREAM_HEADER)&(pSrb->CommandData.StreamBuffer->StreamHeader);
     PHW_STREAM_INFORMATION pstrinfo =
      (PHW_STREAM_INFORMATION)&(pSrb->CommandData.StreamBuffer->StreamInfo);
     
    ```

2.  バッファーが、返されたデータを保持するのに十分な大きさであることを確認します。

3.  情報をバッファーに書き込みます。
