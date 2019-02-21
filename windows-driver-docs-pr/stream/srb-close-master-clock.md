---
title: SRB\_閉じる\_マスター\_クロック
description: SRB\_閉じる\_マスター\_クロック
ms.assetid: 5d49f64a-22e0-4fec-a9f5-4ce5169fa305
keywords:
- SRB_CLOSE_MASTER_CLOCK ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_CLOSE_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 467ff76acb23c0f4a180249d644166c1e2447fd6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549463"
---
# <a name="srbclosemasterclock"></a>SRB\_閉じる\_マスター\_クロック


## <span id="ddk_srb_close_master_clock_ks"></span><span id="DDK_SRB_CLOSE_MASTER_CLOCK_KS"></span>


クラス ドライバーは、ストリーム、ミニドライバー用の時計はマスターではないことを示すには、この要求を発行します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

 

 





