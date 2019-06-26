---
title: debugbaseeventcallbackswide
description: DebugBaseEventCallbacksWide クラスでは、IDebugEventCallbacksWide インターフェイスの基本実装を提供します。
ms.assetid: 38AD8472-1BA3-42EA-99CE-E91098A5B334
keywords:
- DebugBaseEventCallbacksWide
ms.date: 01/10/2018
topic_type:
- apiref
api_name:
- debugbaseeventcallbackswide
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fcddd75b4a243630c7b7c43f949d96580f1ed456
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366964"
---
# <a name="debugbaseeventcallbackswide-class"></a>DebugBaseEventCallbacksWide class 

DebugBaseEventCallbacksWide クラスの基本実装を提供する、 [IDebugEventCallbacksWide](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbackswide)インターフェイス。 

プログラムでは、DebugBaseEventCallbacksWide からイベントのコールバック クラスを派生でき、必要なメソッドのみを実装することができます。 

GetInterestMask を適切に実装するように注意します。
 
### <a name="requirements"></a>要件

Header

Dbgeng.h (Dbgeng.h を含む)  


### <a name="see-also"></a>関連項目
[DebugBaseEventCallbacks](debugbaseeventcallbacks.md)

 

 





