---
title: debugbaseeventcallbacks バック
description: DebugBaseEventCallbacks バッククラスは、IDebugEventCallbacks インターフェイスの基本実装を提供します。
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
ms.openlocfilehash: 6ed59e435e2d9f040e80e1c89dd83e66de4957ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837781"
---
# <a name="debugbaseeventcallbacks-class"></a>DebugBaseEventCallbacks バッククラス 

DebugBaseEventCallbacks バッククラスは、 [IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイスの基本実装を提供します。 

プログラムは、DebugBaseEventCallbacks バックからイベントコールバッククラスを派生させ、必要なメソッドのみを実装できます。 

GetInterestMask を適切に実装するように注意してください。
 
### <a name="requirements"></a>要件

Header

Dbgeng .h (Dbgeng .h を含む)  


### <a name="see-also"></a>参照
[Debugbaseeventゲートウェイ Swide](debugbaseeventcallbackswide.md)

 

 





