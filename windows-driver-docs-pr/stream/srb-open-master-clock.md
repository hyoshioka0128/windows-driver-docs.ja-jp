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
ms.openlocfilehash: 3b30d765138e8c2cfd56236f84e34492a1b1d2c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377895"
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

クラスのドライバー セット、 **CommandData**.**MasterClockHandle**によって示されるメンバー *pSrb*クロック オブジェクトのハンドルには、マスターのクロックを表すが作成されます。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。

ミニドライバーを保持する必要があります、 **CommandData.MasterClockHandle**フィールドのマスターのクロックのハンドルを指す SRB の値。

 

 





