---
title: KSEVENT\_CLOCK\_INTERVAL\_マーク
description: クライアントは、初期時間値に達したときに通知を受け取るように、KSEVENT\_CLOCK\_INTERVAL\_マークイベントを有効にし、その後、固定された時間が経過すると通知を受け取ります。
ms.assetid: 5292606e-d0b3-4e64-a236-c1cecf3fd53a
keywords:
- KSEVENT_CLOCK_INTERVAL_MARK ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_INTERVAL_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb042dca53d7a76037aed9d45160ce466136db4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845523"
---
# <a name="ksevent_clock_interval_mark"></a>KSEVENT\_CLOCK\_INTERVAL\_マーク


クライアントは、初期時間値に達したときに通知を受け取るように、KSEVENT\_CLOCK\_INTERVAL\_マークイベントを有効にし、その後、固定された時間が経過すると通知を受け取ります。

## <span id="ddk_ksevent_clock_interval_mark_ks"></span><span id="DDK_KSEVENT_CLOCK_INTERVAL_MARK_KS"></span>


### <a name="span-idevent_dataspanspan-idevent_dataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>イベントデータ

[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)を呼び出してこのイベントに登録するときに、 *outbuffer*パラメーターとして[**KSEVENT\_TIME\_INTERVAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_time_interval)型の構造体を使用します。

<a name="remarks"></a>注釈
-------

イベントに登録する方法の詳細については、「 [KS イベント](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)」を参照してください。

 

 





