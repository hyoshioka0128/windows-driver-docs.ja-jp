---
title: SRB\_を示す\_マスター\_クロック
description: SRB\_を示す\_マスター\_クロック
ms.assetid: 76ce59d2-d33c-4cec-a90e-563a16dc476b
keywords:
- SRB_INDICATE_MASTER_CLOCK ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_INDICATE_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65db7727a7a4ae1b2be815e15c5f7f47e2afb310
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377908"
---
# <a name="srbindicatemasterclock"></a>SRB\_を示す\_マスター\_クロック


## <span id="ddk_srb_indicate_master_clock_ks"></span><span id="DDK_SRB_INDICATE_MASTER_CLOCK_KS"></span>


クラス ドライバーがストリームに、そのマスターのクロックとなるようになりましたクロック オブジェクト ハンドルを示すためには、この要求を発行するか、0 個のハンドルをストリームを示すためには実行されている無料。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスのドライバー セット、 **CommandData**.**MasterClockHandle**によって示されるメンバー *pSrb*マスターのクロックを表すクロック オブジェクトのハンドルにします。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。

ストリームはマスターのクロックを識別するハンドルを渡すことによって、マスターのクロックの時刻の値を照会することが[ **StreamClassQueryMasterClock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassquerymasterclock)または[ **StreamClassQueryMasterClockSync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassquerymasterclocksync).

ミニドライバーは、SRB を受け取るまで\_を示す\_マスター\_クロックの特定のストリームをそのことができますがあると想定ストリームを実行している無料。 この SRB 下位暗証番号 (pin) は、ハンドルと同じです渡されたハンドルのミニドライバーに渡す場合[ **SRB\_オープン\_マスター\_クロック**](srb-open-master-clock.md)、、ミニドライバー。マスターとは従属要素を制御しているために、マスター クロックから直接時間を読み取ることができます。

ミニドライバーを保持する必要があります、 **CommandData.MasterClockHandle**マスターのクロックのハンドルを指す SRB フィールド。 このハンドルが 0 の場合は、あることを示しますミニドライバーにこのストリーム無料実行し、マスターのクロックに従属することはできません。

 

 





