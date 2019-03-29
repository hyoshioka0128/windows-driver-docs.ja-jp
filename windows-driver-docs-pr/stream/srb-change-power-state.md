---
title: SRB\_変更\_POWER\_状態
description: SRB\_変更\_POWER\_状態
ms.assetid: 61a3e390-1ba2-44e0-b364-e86b10937cd6
keywords:
- SRB_CHANGE_POWER_STATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_CHANGE_POWER_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d975d8569d98eb5bd8a00a0603627a8903446a3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573322"
---
# <a name="srbchangepowerstate"></a>SRB\_変更\_POWER\_状態


## <span id="ddk_srb_change_power_state_ks"></span><span id="DDK_SRB_CHANGE_POWER_STATE_KS"></span>


クラス ドライバーでは、この要求の電源状態をリセットする必要がありますが、ミニドライバーに通知を送信します。 *pSrb*-&gt;**DeviceState**新しい電源の状態を指定します。 参照してください[ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
低電力を呼び出すことができません、ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

ミニドライバーは、保存またはデバイスに固有のデータを復元する必要がある場合に行ってください、SRB を処理するときに\_変更\_POWER\_状態要求。

電源状態の詳細については、次を参照してください。[個々 のデバイスを管理する Power](https://msdn.microsoft.com/library/windows/hardware/ff554397)します。

 

 





