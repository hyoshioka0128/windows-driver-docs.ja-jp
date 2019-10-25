---
title: コンテキスト内での状態の維持
description: コンテキスト内での状態の維持
ms.assetid: dabf6aa7-f127-419c-9245-5270768fef5b
keywords:
- コンテキスト WDK Direct3D、状態の保持
- WDK Direct3D の状態
- 内部状態 WDK Direct3D
- パブリック状態 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0699f6248b2936acdfa7ba9547d5d56260bf02ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840587"
---
# <a name="maintaining-state-within-a-context"></a>コンテキスト内での状態の維持


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


ドライバーは、その[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックが呼び出されたときに、コンテキストに関連付けられた内部状態を更新します。 このコールバックは、更新されたコンテキストのパブリック状態も Direct3D に返す必要があります。

 

 





