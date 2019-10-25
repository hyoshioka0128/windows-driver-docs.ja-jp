---
title: タイマーの設定とクリア
description: タイマーの設定とクリア
ms.assetid: 75f348f7-173f-4799-88aa-1ca50a6df023
keywords:
- タイマーサービス WDK NDIS
- NDIS タイマーサービス WDK
- NDIS タイマーのクリア
- NDIS タイマーの割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3e04575a38a808e08babfb7230e9bb445d8708e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841948"
---
# <a name="setting-and-clearing-timers"></a>タイマーの設定とクリア





[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)関数を使用してタイマーを割り当てて初期化した後、NDIS 6.0 ドライバーは[**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)関数を呼び出して、指定された間隔または定期的にタイマーオブジェクトが起動するように設定します。

**NdisSetTimerObject**の*DueTime*パラメーターは、タイマーが起動するまでの期間を指定します。 NDIS は、関連付けられている[**nettimercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)関数を呼び出します。 有効期限は、システム時間単位 (100 ナノ秒間隔) で表されます。

**NdisSetTimerObject**の*MillisecondsPeriod*パラメーターが0でない場合は、タイマーが定期的に起動され、周期的なタイマーが実行されるまでの間隔をミリ秒単位*で指定します。* を起動し、次に*Nettimercallback*関数を呼び出します。

ドライバーは、 [**NdisCancelTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)関数を呼び出して、 **NdisSetTimerObject**関数の前回の呼び出しに関連付けられているタイマーを取り消すことができます。 **NdisCancelTimerObject**の呼び出しの前にタイムアウトが既に期限切れになっている場合、NDIS は*nettimercallback*を呼び出す可能性があります。

 

 





