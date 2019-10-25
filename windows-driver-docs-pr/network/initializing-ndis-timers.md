---
title: NDIS タイマーの初期化
description: NDIS タイマーの初期化
ms.assetid: 2f304f5c-fa70-441e-853e-a48ad70d61a0
keywords:
- タイマーサービス WDK NDIS
- NDIS タイマーサービス WDK
- NDIS タイマーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a67f91fa6d548879d4dfc508f7d381151c6f50e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824438"
---
# <a name="initializing-ndis-timers"></a>NDIS タイマーの初期化





[**NDIS\_timer\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_timer_characteristics)構造は、ワンショットまたは周期的なタイマーの特性を定義します。 NDIS ドライバーは複数のタイマーを持つことができます。 各タイマーオブジェクトは、 **timerfunction**メンバーで指定されている別の[**nettimercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_timer_function)関数に関連付けられています。 NDIS は、タイマーの有効期限が切れると、関連付けられている*Nettimercallback*関数を呼び出します。

タイマーを割り当てて初期化するには、ドライバーが[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)関数を呼び出し、ドライバーによって割り当てられた NDIS\_TIMER\_特性の構造を提供する必要があります。 ドライバーが[**NdisSetTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)関数を呼び出すまで、タイマーは開始されません。

タイマーオブジェクトを解放するには、ドライバーが[**NdisFreeTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreetimerobject)関数を呼び出す必要があります。

 

 





