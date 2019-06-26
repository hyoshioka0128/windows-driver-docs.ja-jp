---
title: SRB\_提案\_データ\_形式
description: SRB\_提案\_データ\_形式
ms.assetid: a15ec7cc-7351-4a63-ad35-e59610205913
keywords:
- SRB_PROPOSE_DATA_FORMAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_PROPOSE_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8206351223b7e4e455f66a371698727496a250f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377884"
---
# <a name="srbproposedataformat"></a>SRB\_提案\_データ\_形式


## <span id="ddk_srb_propose_data_format_ks"></span><span id="DDK_SRB_PROPOSE_DATA_FORMAT_KS"></span>


クラスのドライバーでは、ストリームが指定されたデータ形式をサポートするかどうかを判断するには、この要求を発行します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>ステータス\_いない\_サポートされています。  
提案された形式が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラス ドライバーが受信すると、 [ **KSPROPERTY\_接続\_PROPOSEDATAFORMAT** ](ksproperty-connection-proposedataformat.md)要求、提案された形式がサポートされているかどうかを判断するこの SRB コードを使用します。 クラスのドライバーで提案されたデータ形式を通過する、 **CommandData**.**OpenFormat**によって示されるメンバー *pSrb*します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。

ミニドライバーは、データ形式をサポートしていない場合は設定*pSrb*-&gt;**状態**ステータス\_いない\_サポートされています。 このフィールドは、状態を設定が、ミニドライバーは、ストリームを指定した形式に切り替えることが場合、\_成功します。

ミニドライバーは、新しい形式を受け入れることは場合、クラス ドライバーが後で送信できます、ミニドライバーで示される形式の変更、 **OptionsFlags**内のメンバー、 [ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造体。

## <a name="see-also"></a>関連項目


[**SRB\_設定\_データ\_形式**](srb-set-data-format.md)

[SRB\_取得\_データ\_形式](srb-get-data-format.md)

 

 






