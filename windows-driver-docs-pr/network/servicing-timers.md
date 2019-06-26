---
title: タイマーのサービス提供
description: タイマーのサービス提供
ms.assetid: 6a80a55b-4c7e-4a48-8903-0a1fb28af153
keywords:
- タイマー サービスの WDK NDIS
- NDIS タイマー サービス WDK
- NDIS タイマーをキャンセル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6547f79211c33a3cf1e6381ca4e59ce46c307dbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386831"
---
# <a name="servicing-timers"></a>タイマーのサービス提供





NDIS 呼び出し、 [ **NetTimerCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_timer_function) NDIS 6.0 のタイマーが発生したときに機能します。 *FunctionContext*この関数のパラメーターには、ドライバーによって提供されるコンテキストの領域へのポインターが含まれています。 既定値*FunctionContext*で指定された、 [ **NDIS\_タイマー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_timer_characteristics)構造体。 ドライバーに渡された構造体を[ **NdisAllocateTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatetimerobject)関数を割り当てたり、関連付けられているタイマー オブジェクトを初期化します。

ドライバーで NULL 以外の値が指定したかどうか、 *FunctionContext*パラメーターに渡される、 [ **NdisSetTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)関数、NDIS その値渡し、 *FunctionContext*のパラメーター、 *NetTimerCallback*関数。 それ以外の場合、NDIS は、NDIS で指定されている既定値を渡します\_タイマー\_特性構造体。

NDIS ドライバーには、1 つ以上を指定できる*NetTimerCallback*関数。 これらの各*NetTimerCallback*関数は、別のドライバーに割り当てられた、初期化のタイマー オブジェクトに関連付けである必要があります。

呼び出し、 [ **NdisSetTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)関数のエラーの原因、 *NetTimerCallback*指定した時間後に実行するタイマー オブジェクトに関連付けられている関数または定期的にします。

呼び出しを停止する、 *NetTimerCallback*関数を呼び出しを[ **NdisCancelTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)関数。 NDIS は呼び出すことができますも*NetTimerCallback* 、タイムアウトが既に呼び出しの前に期限切れ**NdisCancelTimerObject**します。

場合、 *NetTimerCallback*関数は、その他のドライバーの機能とリソースを共有、ドライバーは、スピン ロックとそれらのリソースへのアクセスを同期する必要があります。

 

 





