---
title: SRB\_設定\_ストリーム\_プロパティ
description: SRB\_設定\_ストリーム\_プロパティ
ms.assetid: 33a44732-a75c-4394-9839-f3c7d71d01e1
keywords:
- SRB_SET_STREAM_PROPERTY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_SET_STREAM_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 148bd6efcd645b60350936ce37ab7cc774e7ae4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377858"
---
# <a name="srbsetstreamproperty"></a>SRB\_設定\_ストリーム\_プロパティ


## <span id="ddk_srb_set_stream_property_ks"></span><span id="DDK_SRB_SET_STREAM_PROPERTY_KS"></span>


クラス ドライバーは、このストリームのミニドライバー定義プロパティのプロパティのセット要求を完了するために必要なデータのミニドライバーを照会するには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラス ドライバーは、操作のパラメーターを渡す、 *pSrb*-&gt;**CommandData**.**PropertyInfo**バッファー、フォームの構造[**ストリーム\_プロパティ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_stream_property_descriptor)します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。

**プロパティ**ストリームのメンバー\_プロパティ\_記述子には、問題の中にプロパティがについて説明します、 **PropertyInfo**メンバーは、コピー元のバッファーを指定しますプロパティのデータ。 バッファーが小さすぎる場合、ミニドライバーを設定する必要があります、**状態**によって示されるメンバー *pSrb*ステータス\_バッファー\_オーバーフローが発生します。

## <a name="see-also"></a>関連項目


[**SRB\_取得\_ストリーム\_プロパティ**](srb-get-stream-property.md)

[**ストリーム\_プロパティ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_stream_property_descriptor)

 

 






