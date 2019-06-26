---
title: レンダー ターゲットの要件
description: レンダー ターゲットの要件
ms.assetid: 4d16819e-f209-44df-b5af-f3ff9cae256b
keywords:
- レンダー ターゲット WDK Direct3D
- WDK Direct3D バッファーの色
- WDK Direct3D バッファー
- 深度バッファーの WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4045f4ecba4016c0e07aeef3fcab0d9db7144e22
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380553"
---
# <a name="render-target-requirements"></a>レンダー ターゲットの要件


## <span id="ddk_render_target_requirements_gg"></span><span id="DDK_RENDER_TARGET_REQUIREMENTS_GG"></span>


色のバッファーと深度バッファーの要件は次のとおりです。

### <a name="span-idcolorbuffersspanspan-idcolorbuffersspancolor-buffers"></a><span id="color_buffers"></span><span id="COLOR_BUFFERS"></span>色のバッファー

ハードウェアはテクスチャとして使用することもあるレンダー ターゲットをサポートしていない場合 (つまり、デバイスことはできません「にレンダリング テクスチャ」)、デバイスへの呼び出しが失敗する必要があります、 **IDirect3DDevice7::SetRenderTarget**と**IDirect3D7::CreateDevice**メソッド。 これらのメソッドは、Direct3D SDK のドキュメントで説明します。 テクスチャが、DDSCAPS の存在によって示されたとして使用する、レンダー ターゲットであるという事実\_サーフェスの説明にテクスチャ フラグ (を参照してください、 **dwCaps**のメンバー、 [ **DDSCAPS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))構造)。

### <a name="span-iddepthbuffersspanspan-iddepthbuffersspandepth-buffers"></a><span id="depth_buffers"></span><span id="DEPTH_BUFFERS"></span>深度バッファー

ハードウェアがレンダー ターゲットと深度バッファー、特定の組み合わせをサポートしていないかどうかは、デバイスなどの呼び出しで、この種の不一致を検出したときに、このシナリオを発生させる API 呼び出しが失敗する必要があります、 **IDirect3D7::CreateDevice**と**IDirectDrawSurface7::AddAttachedSurface**メソッド。 これらのメソッドは、Direct3D、DirectDraw SDK のドキュメント セットで、それぞれについて説明します。 ときに、このような不一致の例があります、レンダー ターゲットと深度バッファーは、異なるビット深度。 レンダー ターゲットまたは適切に機能する、無効な組み合わせが発生する深度バッファーのいずれかの形式は透過的に変更されません。 代わりに、DirectX のランタイムに通知することがなく高い有効桁数の深度バッファーを割り当てます。

 

 





