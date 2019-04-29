---
title: レンダー ターゲットの有効性の確認
description: レンダー ターゲットの有効性の確認
ms.assetid: 316ecd58-996a-4277-b2dc-4424c96d8a56
keywords:
- レンダー ターゲット WDK DirectX 9.0、有効性を確認しています
- WDK DirectX 9.0 のレンダー ターゲットを検証しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af45a846922aa41edd4bfa375f5ca74359c37cb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390782"
---
# <a name="verifying-validity-of-render-target"></a>レンダー ターゲットの有効性の確認


## <span id="ddk_verifying_validity_of_render_target_gg"></span><span id="DDK_VERIFYING_VALIDITY_OF_RENDER_TARGET_GG"></span>


ドライバーのバージョンでは、DirectX 9.0 ランタイムにより、アプリケーションを設定するために、レンダー ターゲットを使用する前に、その内部のレンダー ターゲットが有効かどうかを確認する必要があります DirectX 9.0 のレンダリングにターゲット**NULL**します。 これに対し、DirectX 8.1 およびそれ以前のランタイム保証レンダー ターゲットでは常に Direct3D のコンテキストで有効です。

 

 





