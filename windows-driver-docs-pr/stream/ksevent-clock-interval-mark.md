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
ms.openlocfilehash: d68113c0a816febb25949c9c4ad91fe10e424122
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556850"
---
# <a name="kseventclockintervalmark"></a>KSEVENT\_クロック\_間隔\_マーク


クライアントが、KSEVENT を有効にする\_クロック\_間隔\_その後、初期の時刻値に達すると、しを一定の時間単位で通知するイベントをマークします。

## <span id="ddk_ksevent_clock_interval_mark_ks"></span><span id="DDK_KSEVENT_CLOCK_INTERVAL_MARK_KS"></span>


### <a name="span-ideventdataspanspan-ideventdataspanevent-data"></a><span id="event_data"></span><span id="EVENT_DATA"></span>イベント データ

型の構造体を使用して、 [ **KSEVENT\_時間\_間隔**](https://msdn.microsoft.com/library/windows/hardware/ff561887)として、 *OutBuffer*パラメーターを呼び出すときに[ **KsSynchronousDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff567142)このイベントに登録します。

<a name="remarks"></a>注釈
-------

イベントを登録する方法については、[KS イベント](https://msdn.microsoft.com/library/windows/hardware/ff567643)を参照してください。

 

 





