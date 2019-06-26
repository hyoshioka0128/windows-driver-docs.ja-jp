---
title: debugbaseeventcallbacks
description: DebugBaseEventCallbacks クラスでは、IDebugEventCallbacks インターフェイスの基本実装を提供します。
ms.assetid: B0422248-2F5F-4AE6-93C9-D96B5E4A1B5A
keywords:
- DebugBaseEventCallbacks
ms.date: 01/10/2018
topic_type:
- apiref
api_name:
- debugbaseeventcallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b03e86ab589997584c3900a4c236c30004a6bcf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361414"
---
# <a name="debugbaseeventcallbacks-class"></a>DebugBaseEventCallbacks class 

DebugBaseEventCallbacks クラスの基本実装を提供する、 [IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイス。 

プログラムでは、DebugBaseEventCallbacks からイベントのコールバック クラスを派生でき、必要なメソッドのみを実装することができます。 

GetInterestMask を適切に実装するように注意します。
 
### <a name="requirements"></a>必要条件

Header

Dbgeng.h (Dbgeng.h を含む)  


### <a name="see-also"></a>関連項目
[DebugBaseEventCallbacksWide](debugbaseeventcallbackswide.md)

 

 





