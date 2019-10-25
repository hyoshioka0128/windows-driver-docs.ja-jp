---
title: SRB\_\_データ\_形式の設定
description: SRB\_\_データ\_形式の設定
ms.assetid: a111ab92-a0a0-464e-ac13-f5be33ecd064
keywords:
- SRB_SET_DATA_FORMAT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_SET_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3acabd401f734f1a4e32f5fe3552705ea252b09f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837709"
---
# <a name="srb_set_data_format"></a>SRB\_\_データ\_形式の設定


## <span id="ddk_srb_set_data_format_ks"></span><span id="DDK_SRB_SET_DATA_FORMAT_KS"></span>


クラスドライバーは、この要求を発行してストリームのデータ形式を設定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>ステータス\_\_サポートされていません  
ミニドライバーが要求されたデータ形式をサポートしていないことを示します。

### <a name="comments"></a>コメント

クラスドライバーは、新しいデータ形式を**Commanddata**に渡します。*PSrb*ポインターの**openformat**メンバー。 (このポインターは、[**ハードウェア\_ストリームを指し、\_ブロック構造\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)します)。

データ形式の詳細については、「 [Stream クラスミニドライバー Design Guide](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)」を参照してください。 [AVStream のデータ範囲の共通](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)部分も参照してください。

 

 





