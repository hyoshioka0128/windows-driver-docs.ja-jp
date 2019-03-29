---
title: 動的テクスチャ
description: 動的テクスチャ
ms.assetid: 5e96b33c-a07c-4f58-a016-14d8d925285e
keywords:
- WDK DirectX 9.0 のテクスチャ
- 動的テクスチャ WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d6d55b2c82adb147ed1e6d9a03f449615874565
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581810"
---
# <a name="dynamic-textures"></a>動的テクスチャ


## <span id="ddk_dynamic_textures_gg"></span><span id="DDK_DYNAMIC_TEXTURES_GG"></span>


動的テクスチャはほぼ同じ[動的バッファー](dynamic-vertex-and-index-buffers.md)します。 アプリケーションは、頻繁にもロックし、動的テクスチャを変更、ため、ドライバーが必要です。

-   テクスチャのアップロードやタイルの速度を最適化します。

-   場合は、ハードウェア アーキテクチャにより、ドライバーの使用 nontiled テクスチャ nontiled 方法で動的テクスチャを作成します。 動的テクスチャを untile テクスチャがロックされているときにドライバーを必要としないから受信したパフォーマンス向上はタイルのフィル レートの利点がありますよりも大きいためにです。

-   説明のようを設定すると、複数のバッファリング[動的頂点バッファーとインデックス バッファー](dynamic-vertex-and-index-buffers.md)します。 つまり、DDLOCK を設定\_OKTOSWAP ビット動的テクスチャをロックします。 同様に、ローカルのビデオ メモリに動的テクスチャを格納する可能性もシステムのパフォーマンスが低下する場合は、連番でない方法で、アプリケーションがこのようなテクスチャを書き込みます。 ドライバーがで動的テクスチャを格納するため、 [AGP](agp-support.md)メモリ。

 

 





