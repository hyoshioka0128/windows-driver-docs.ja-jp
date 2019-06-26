---
title: NDIS タイマーの初期化
description: NDIS タイマーの初期化
ms.assetid: 2f304f5c-fa70-441e-853e-a48ad70d61a0
keywords:
- タイマー サービスの WDK NDIS
- NDIS タイマー サービス WDK
- NDIS タイマーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9246a24925be737321867b1456437e5aa1b06ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381267"
---
# <a name="initializing-ndis-timers"></a>NDIS タイマーの初期化





[ **NDIS\_タイマー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_timer_characteristics)構造体が 1 回限りまたは定期的なタイマーの特性を定義します。 NDIS ドライバーでは、1 つ以上のタイマーを持つことができます。 各タイマー オブジェクトは、別の関連付け[ **NetTimerCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_timer_function)関数で指定されている、 **TimerFunction**メンバー。 NDIS 呼び出し、関連付けられている*NetTimerCallback*タイマーが切れたときに機能します。

割り当てをタイマーの初期化は、ドライバーを呼び出す必要があります、 [ **NdisAllocateTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatetimerobject)機能し、ドライバーによって割り当てられた NDIS\_タイマー\_特性構造体。 ドライバーの呼び出しまで、タイマーが開始されない、 [ **NdisSetTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)関数。

タイマー オブジェクトを解放するには、ドライバーを呼び出す必要があります、 [ **NdisFreeTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreetimerobject)関数。

 

 





