---
title: コンテキスト内での状態の維持
description: コンテキスト内での状態の維持
ms.assetid: dabf6aa7-f127-419c-9245-5270768fef5b
keywords:
- コンテキスト WDK Direct3D、状態を維持します。
- WDK Direct3D を状態します。
- 内部状態 WDK Direct3D
- パブリック状態 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5cc972ad7a527ba9bfaa847fec6f93535d2b9c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379024"
---
# <a name="maintaining-state-within-a-context"></a>コンテキスト内での状態の維持


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


ドライバーをコンテキストに関連付けられた内部状態を更新するときにその[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックが呼び出されます。 このコールバックは、Direct3D を更新されたコンテキストのパブリックな状態も返す必要があります。

 

 





