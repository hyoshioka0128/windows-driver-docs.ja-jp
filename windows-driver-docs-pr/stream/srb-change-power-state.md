---
title: 電源\_状態\_SRB\_変更
description: 電源\_状態\_SRB\_変更
ms.assetid: 61a3e390-1ba2-44e0-b364-e86b10937cd6
keywords:
- SRB_CHANGE_POWER_STATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_CHANGE_POWER_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c9106a03bce351956b2bc444cd6fda3ef1913f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843313"
---
# <a name="srb_change_power_state"></a>電源\_状態\_SRB\_変更


## <span id="ddk_srb_change_power_state_ks"></span><span id="DDK_SRB_CHANGE_POWER_STATE_KS"></span>


クラスドライバーは、その電源状態をリセットする必要があることをミニドライバーに通知するために、この要求を送信します。 *pSrb*-&gt;**devicestate**は新しい電源の状態を指定します。 「 [**HW\_STREAM\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)」を参照してください。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生し、省電力を呼び出すことができないことを示します。

### <a name="comments"></a>コメント

ミニドライバーがデバイス固有のデータを保存または復元する必要がある場合は、SRB\_を処理するときに、電源\_状態要求\_変更する必要があります。

電源の状態の詳細については、「[個々のデバイスの電源の管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-power-for-individual-devices)」を参照してください。

 

 





