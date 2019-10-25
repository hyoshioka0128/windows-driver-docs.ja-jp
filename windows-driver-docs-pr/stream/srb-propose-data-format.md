---
title: SRB\_\_データ\_形式の提案
description: SRB\_\_データ\_形式の提案
ms.assetid: a15ec7cc-7351-4a63-ad35-e59610205913
keywords:
- SRB_PROPOSE_DATA_FORMAT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_PROPOSE_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74ee1eeb67971bef4d14be795f607b4b39dfcad6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837713"
---
# <a name="srb_propose_data_format"></a>SRB\_\_データ\_形式の提案


## <span id="ddk_srb_propose_data_format_ks"></span><span id="DDK_SRB_PROPOSE_DATA_FORMAT_KS"></span>


クラスドライバーは、ストリームが特定のデータ形式をサポートしているかどうかを判断するために、この要求を発行します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>ステータス\_\_サポートされていません  
提案された形式がミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>説明

クラスドライバーが[**Ksk プロパティ\_接続\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md) request を受け取ると、この SRB コードを使用して、提案された形式がサポートされているかどうかを判断します。 クラスドライバーは、指定されたデータ形式を**commanddata**に渡します。*PSrb*が指す**openformat**メンバー。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。

ミニドライバーがデータ形式をサポートしていない場合は、 *pSrb*-&gt;の**状態**が\_\_サポートされていない状態に設定されます。 ミニドライバーがストリームを指定した形式に切り替えることができる場合、このフィールドは STATUS\_SUCCESS に設定されます。

ミニドライバーが新しい形式を受け入れることができる場合、後でクラスドライバーがミニドライバー a 形式の変更を送信することがあります。これは、 [**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体の**optionsflags**メンバーによって示されます。

## <a name="see-also"></a>関連項目


[**SRB\_\_データ\_形式の設定**](srb-set-data-format.md)

[SRB\_\_のデータ\_形式を取得する](srb-get-data-format.md)

 

 






