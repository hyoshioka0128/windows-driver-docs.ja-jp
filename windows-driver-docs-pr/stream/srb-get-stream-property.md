---
title: SRB\_GET\_STREAM\_プロパティ
description: SRB\_GET\_STREAM\_プロパティ
ms.assetid: 579ae9b1-06f0-4f7b-afbf-c5a7df399745
keywords:
- SRB_GET_STREAM_PROPERTY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_GET_STREAM_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1441f76b29dba92604d4991fdbae62178951410b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843303"
---
# <a name="srb_get_stream_property"></a>SRB\_GET\_STREAM\_プロパティ


## <span id="ddk_srb_get_stream_property_ks"></span><span id="DDK_SRB_GET_STREAM_PROPERTY_KS"></span>


クラスドライバーは、この要求を送信して、このストリームのミニドライバーで定義されたプロパティに対してプロパティ get 要求を完了するために必要なデータをミニドライバーに照会します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスドライバーは、操作のパラメーターを*pSrb*-&gt;**commanddata**に渡します。**PropertyInfo** buffer は、フォームストリームの構造[ **\_プロパティ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_property_descriptor)です。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。

ストリーム\_プロパティ\_記述子構造体の**プロパティ**メンバーは、問題のプロパティを記述します。 **PropertyInfo**メンバーは、プロパティデータをコピーするバッファーを指定します。 バッファーが小さすぎる場合、ミニドライバーは*pSrb*によってポイントされた**状態**メンバーを STATUS\_buffer\_OVERFLOW に設定する必要があります。

## <a name="see-also"></a>関連項目


[**SRB\_SET\_STREAM\_プロパティ**](srb-set-stream-property.md)

[**ストリーム\_プロパティ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_property_descriptor)

 

 






