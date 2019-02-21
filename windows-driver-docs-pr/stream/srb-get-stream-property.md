---
title: SRB\_取得\_ストリーム\_プロパティ
description: SRB\_取得\_ストリーム\_プロパティ
ms.assetid: 579ae9b1-06f0-4f7b-afbf-c5a7df399745
keywords:
- SRB_GET_STREAM_PROPERTY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_GET_STREAM_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a92d556c5fc34ddc63ca2aa15343f1661ebe9c48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528989"
---
# <a name="srbgetstreamproperty"></a>SRB\_取得\_ストリーム\_プロパティ


## <span id="ddk_srb_get_stream_property_ks"></span><span id="DDK_SRB_GET_STREAM_PROPERTY_KS"></span>


クラス ドライバーは、このストリームのミニドライバー定義プロパティのプロパティを完了するために必要なデータの取得要求をミニドライバーを照会するには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラス ドライバーは、操作のパラメーターを渡す、 *pSrb*-&gt;**CommandData**.**PropertyInfo**バッファー、フォームの構造[**ストリーム\_プロパティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff568442)します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)構造体。

**プロパティ**ストリームのメンバー\_プロパティ\_記述子構造体が、問題の中にプロパティを記述、 **PropertyInfo**メンバーのコピー先バッファーを指定します、プロパティにデータをします。 バッファーが小さすぎる場合、ミニドライバーを設定する必要があります、**状態**によって示されるメンバー *pSrb*ステータス\_バッファー\_オーバーフローが発生します。

## <a name="see-also"></a>関連項目


[**SRB\_設定\_ストリーム\_プロパティ**](srb-set-stream-property.md)

[**ストリーム\_プロパティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff568442)

 

 






