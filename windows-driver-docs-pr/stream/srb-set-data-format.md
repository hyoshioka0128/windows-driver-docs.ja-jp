---
title: SRB\_設定\_データ\_形式
description: SRB\_設定\_データ\_形式
ms.assetid: a111ab92-a0a0-464e-ac13-f5be33ecd064
keywords:
- SRB_SET_DATA_FORMAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_SET_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b97893b39d8e81e11696a6da8ceb00767eba4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377874"
---
# <a name="srbsetdataformat"></a>SRB\_設定\_データ\_形式


## <span id="ddk_srb_set_data_format_ks"></span><span id="DDK_SRB_SET_DATA_FORMAT_KS"></span>


クラスのドライバーでは、ストリームのデータ形式を設定するには、この要求を発行します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>ステータス\_いない\_サポートされています。  
ようにミニドライバーに要求されたデータの形式がサポートされていないことを示します。

### <a name="comments"></a>コメント

クラスのドライバーで新しいデータ形式を渡す、 **CommandData**.**OpenFormat**のメンバー、 *pSrb*ポインター。 (このポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造です)。

データ形式の詳細については、次を参照してください。、 [Stream クラス ミニドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)します。 参照してください[AVStream のデータ範囲の交差部分](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)します。

 

 





