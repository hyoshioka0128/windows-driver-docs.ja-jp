---
title: SRB\_非\_デバイス
description: SRB\_非\_デバイス
ms.assetid: 2cacb65a-8df3-4649-bc44-1bc7a5c598b9
keywords:
- SRB_UNINITIALIZE_DEVICE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_UNINITIALIZE_DEVICE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ea0c1fc7e211d45e89a3eac9569860e1f06a44f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553750"
---
# <a name="srbuninitializedevice"></a>SRB\_非\_デバイス


## <span id="ddk_srb_uninitialize_device_ks"></span><span id="DDK_SRB_UNINITIALIZE_DEVICE_KS"></span>


クラス ドライバーは、無効にするミニドライバーを通知するには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_ADAPTER_HARDWARE_ERROR"></span><span id="status_adapter_hardware_error"></span>ステータス\_アダプター\_ハードウェア\_エラー  
この時点で、ミニドライバーの初期化を解除することはできないことを示します。

### <a name="comments"></a>コメント

ミニドライバーは、それが割り当てられているリソースの割り当てを解除し、デバイスの割り込みを無効にする必要があります。 (クラス ドライバーに自動的に割り当て解除し、ミニドライバーの代わりに割り当てられているリソース。)

 

 





