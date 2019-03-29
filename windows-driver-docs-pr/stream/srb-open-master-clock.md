---
title: SRB\_オープン\_マスター\_クロック
description: SRB\_オープン\_マスター\_クロック
ms.assetid: 1ccad1bc-27e7-4038-b341-389240051fb8
keywords:
- SRB_OPEN_MASTER_CLOCK ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_OPEN_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa3b353712b3d3c2ac6537df22866bab13c8738b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572719"
---
# <a name="srbopenmasterclock"></a>SRB\_オープン\_マスター\_クロック


## <span id="ddk_srb_open_master_clock_ks"></span><span id="DDK_SRB_OPEN_MASTER_CLOCK_KS"></span>


クラス ドライバーは、ストリームを示す、ミニドライバーには、今すぐマスター クロックとして機能するには、この要求を発行します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスのドライバー セット、 **CommandData**.**MasterClockHandle**によって示されるメンバー *pSrb*クロック オブジェクトのハンドルには、マスターのクロックを表すが作成されます。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)構造体。

ミニドライバーを保持する必要があります、 **CommandData.MasterClockHandle**フィールドのマスターのクロックのハンドルを指す SRB の値。

 

 





