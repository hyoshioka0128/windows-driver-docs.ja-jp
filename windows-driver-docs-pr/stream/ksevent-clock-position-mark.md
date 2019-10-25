---
title: KSEVENT\_CLOCK\_POSITION\_マーク
description: 時計の特定の時刻に達したときに、KSEVENT\_CLOCK\_POSITION\_MARK イベントが発生します。
ms.assetid: 489e7441-41e9-40e5-8bf5-0bff2fda9f27
keywords:
- KSEVENT_CLOCK_POSITION_MARK ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_POSITION_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7b231c62b0acfd1bdf3ed4119ca085739a39406
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845521"
---
# <a name="ksevent_clock_position_mark"></a>KSEVENT\_CLOCK\_POSITION\_マーク


時計の特定の時刻に達したときに、KSEVENT\_CLOCK\_POSITION\_MARK イベントが発生します。

### <a name="span-idevent_dataspanspan-idevent_dataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>イベントデータ

[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)を呼び出してこのイベントに登録するときに、 [**KSEVENT\_\_TIME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_time_mark)型の構造体を*OUTBUFFER*パラメーターとしてマークします。

<a name="remarks"></a>注釈
-------

イベントに登録する方法の詳細については、「 [KS イベント](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)」を参照してください。

 

 





