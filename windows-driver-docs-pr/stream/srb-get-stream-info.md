---
title: SRB\_取得\_ストリーム\_情報
description: SRB\_取得\_ストリーム\_情報
ms.assetid: ff5412ee-6e4f-43f4-a90d-4a2bdfa5d4ae
keywords:
- SRB_GET_STREAM_INFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_GET_STREAM_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55703bfffb363c27088f9f236053ac4f279d32de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358373"
---
# <a name="srbgetstreaminfo"></a>SRB\_取得\_ストリーム\_情報


## <span id="ddk_srb_get_stream_info_ks"></span><span id="DDK_SRB_GET_STREAM_INFO_KS"></span>


クラス ドライバーは、デバイスと、ストリームのサポートの説明を取得するには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスのドライバーにバッファーを渡します*pSrb*-&gt;**CommandData.StreamBuffer**クラス ドライバーへの応答でミニドライバーで指定したサイズの[**SRB\_初期化\_デバイス**](srb-initialize-device.md)要求。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。 参照してください[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_port_configuration_information)します。

ミニドライバー塗りつぶし**CommandData.StreamBuffer**で、 [ **HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)デバイスと、ストリームを記述することサポートされています。 このバッファーのサイズでミニドライバーで示されている、 **StreamDescriptorSize**フィールドに、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_port_configuration_information)構造体。

クラス ドライバーは通常、この要求を 1 回だけ発行します。 クラス ドライバーを呼び出すことによって、サポートされているストリームの説明を更新する、この要求を再発行することがあります強制的に、ミニドライバー [StreamClassReenumerateStreams](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassreenumeratestreams)します。

**ときに、SRB\_取得\_ストリーム\_ミニドライバーが INFO コマンドを受信した、ようにミニドライバーにする必要があります。**

1.  ストリーム ヘッダーとストリーム情報のデータ構造のポインターを取得します。 次に、例を示します。

    ```cpp
     PHW_STREAM_HEADER pstrhdr =
      (PHW_STREAM_HEADER)&(pSrb->CommandData.StreamBuffer->StreamHeader);
     PHW_STREAM_INFORMATION pstrinfo =
      (PHW_STREAM_INFORMATION)&(pSrb->CommandData.StreamBuffer->StreamInfo);
     
    ```

2.  バッファーが返されたデータを保持するのに十分な大きさであることを確認します。

3.  情報をバッファーに書き込みます。
