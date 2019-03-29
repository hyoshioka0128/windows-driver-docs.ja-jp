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
ms.openlocfilehash: a5109db1e49ffc0de0342fc5ef178780a8373815
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571788"
---
# <a name="initializing-ndis-timers"></a>NDIS タイマーの初期化





[ **NDIS\_タイマー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff567886)構造体が 1 回限りまたは定期的なタイマーの特性を定義します。 NDIS ドライバーでは、1 つ以上のタイマーを持つことができます。 各タイマー オブジェクトは、別の関連付け[ **NetTimerCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff568351)関数で指定されている、 **TimerFunction**メンバー。 NDIS 呼び出し、関連付けられている*NetTimerCallback*タイマーが切れたときに機能します。

割り当てをタイマーの初期化は、ドライバーを呼び出す必要があります、 [ **NdisAllocateTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561618)機能し、ドライバーによって割り当てられた NDIS\_タイマー\_特性構造体。 ドライバーの呼び出しまで、タイマーが開始されない、 [ **NdisSetTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff564563)関数。

タイマー オブジェクトを解放するには、ドライバーを呼び出す必要があります、 [ **NdisFreeTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff562605)関数。

 

 





