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
ms.openlocfilehash: 80d688d1dfbbbe09b2b2cc5c20dbb2d185879218
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365929"
---
# <a name="maintaining-state-within-a-context"></a>コンテキスト内での状態の維持


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


ドライバーをコンテキストに関連付けられた内部状態を更新するときにその[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)コールバックが呼び出されます。 このコールバックは、Direct3D を更新されたコンテキストのパブリックな状態も返す必要があります。

 

 





