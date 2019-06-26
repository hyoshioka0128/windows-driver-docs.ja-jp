---
title: タイマーの設定とクリア
description: タイマーの設定とクリア
ms.assetid: 75f348f7-173f-4799-88aa-1ca50a6df023
keywords:
- タイマー サービスの WDK NDIS
- NDIS タイマー サービス WDK
- NDIS タイマーをクリアします。
- NDIS タイマーの割り当てください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 314383af86e25d56000ebf75e3bd06ee53c75255
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373868"
---
# <a name="setting-and-clearing-timers"></a>タイマーの設定とクリア





割り当てのタイマーを初期化した後、 [ **NdisAllocateTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatetimerobject)関数、NDIS 6.0、ドライバーは、 [ **NdisSetTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)一定の間隔後、または定期的に起動するタイマー オブジェクトを設定します。

*DueTime*パラメーターの**NdisSetTimerObject** 、タイマーが起動されると、NDIS に関連付けられている呼び出しまでの経過するまでの間隔を指定します[ **NetTimerCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_timer_function)関数。 有効期限は、システムの時間単位 (100 ナノ秒間隔) で表されます。

場合、 *MillisecondsPeriod*パラメーターの**NdisSetTimerObject** 0、タイマーが起動を定期的にではないと*MillisecondsPeriod*定期的な時刻を指定します定期的なタイマーの作動時に各と次回の呼び出しの間 (ミリ秒単位) の間隔が経過する、 *NetTimerCallback*関数。

ドライバーを呼び出すことができます、 [ **NdisCancelTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)以前の呼び出しに関連付けられているタイマーをキャンセルする関数、 **NdisSetTimerObject**関数。 NDIS は呼び出すことができますも*NetTimerCallback* 、タイムアウトが既に呼び出しの前に期限切れ**NdisCancelTimerObject**します。

 

 





