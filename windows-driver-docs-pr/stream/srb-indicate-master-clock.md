---
title: SRB\_\_マスター\_クロックを示す
description: SRB\_\_マスター\_クロックを示す
ms.assetid: 76ce59d2-d33c-4cec-a90e-563a16dc476b
keywords:
- SRB_INDICATE_MASTER_CLOCK ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_INDICATE_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e377c1e965b353e492539dea5add295351f38715
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843299"
---
# <a name="srb_indicate_master_clock"></a>SRB\_\_マスター\_クロックを示す


## <span id="ddk_srb_indicate_master_clock_ks"></span><span id="DDK_SRB_INDICATE_MASTER_CLOCK_KS"></span>


クラスドライバーは、この要求を発行して、現在マスタークロックとして機能するクロックオブジェクトのハンドル、またはストリームが無料で実行されていることを示すゼロハンドルを指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスドライバーは**Commanddata**を設定します。マスタークロックを表す clock オブジェクトのハンドルに*pSrb*によって指された**masterclockhandle**メンバー。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。

ストリームは、マスタークロックハンドルを[**Streamclassquerymasterclock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassquerymasterclock)または[**Streamclassquerymasterclocksync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassquerymasterclocksync)に渡すことによって、マスタークロックの時刻値を照会することができます。

特定のストリームの\_マスター\_クロックを示すために、ミニドライバーが\_受信するまでは、ストリームが無料で実行されていると想定できます。 下位のピンに対してこの SRB に渡されたハンドルが\_SRB のミニドライバーに渡されたハンドルと同じである場合、 [ **\_マスター\_クロックを開い**](srb-open-master-clock.md)ているとき、ミニドライバーはマスタークロックから時刻を直接読み取ることができます。これは、マスタークロックがマスターを制御し、下位。

ミニドライバーは、マスタークロックのハンドルを指す SRB 内の**Commanddata. MasterClockHandle**フィールドを保持する必要があります。 このハンドルが0の場合は、ミニドライバーに対して、このストリームが解放され、マスタークロックの下位になることができないことを示します。

 

 





