---
title: KSEVENT\_クロック\_間隔\_マーク
description: クライアントが、KSEVENT を有効にする\_クロック\_間隔\_その後、初期の時刻値に達すると、しを一定の時間単位で通知するイベントをマークします。
ms.assetid: 5292606e-d0b3-4e64-a236-c1cecf3fd53a
keywords:
- KSEVENT_CLOCK_INTERVAL_MARK ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSEVENT_CLOCK_INTERVAL_MARK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1593765b0264780eadb5e18d76ec2ba506e6a6fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382433"
---
# <a name="kseventclockintervalmark"></a>KSEVENT\_クロック\_間隔\_マーク


クライアントが、KSEVENT を有効にする\_クロック\_間隔\_その後、初期の時刻値に達すると、しを一定の時間単位で通知するイベントをマークします。

## <span id="ddk_ksevent_clock_interval_mark_ks"></span><span id="DDK_KSEVENT_CLOCK_INTERVAL_MARK_KS"></span>


### <a name="span-ideventdataspanspan-ideventdataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>イベント データ

型の構造体を使用して、 [ **KSEVENT\_時間\_間隔**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_time_interval)として、 *OutBuffer*パラメーターを呼び出すときに[ **KsSynchronousDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)このイベントに登録します。

<a name="remarks"></a>注釈
-------

イベントを登録する方法については、次を参照してください。 [KS イベント](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)します。

 

 





