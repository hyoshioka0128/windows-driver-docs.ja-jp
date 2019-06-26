---
title: 圧縮テクスチャ サーフェスの幅と高さのレポート
description: 圧縮テクスチャ サーフェスの幅と高さのレポート
ms.assetid: 262262b6-9fef-4f28-beec-373f78a10f8f
keywords:
- WDK DirectDraw、圧縮されたテクスチャを表示します。
- 圧縮テクスチャ WDK DirectDraw、
- 描画圧縮テクスチャ WDK DirectDraw、幅
- DirectDraw 圧縮テクスチャ WDK Windows 2000 では、表示幅
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、幅
- 描画圧縮テクスチャ WDK DirectDraw、高さ
- DirectDraw 圧縮テクスチャ WDK Windows 2000 を表示する高さ
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、高さ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1236314e7cf2aab592f7deb7903dc5bd6effb23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375908"
---
# <a name="reporting-width-and-height-of-compressed-texture-surfaces"></a>圧縮テクスチャ サーフェスの幅と高さのレポート


## <span id="ddk_reporting_width_and_height_of_compressed_texture_surfaces_gg"></span><span id="DDK_REPORTING_WIDTH_AND_HEIGHT_OF_COMPRESSED_TEXTURE_SURFACES_GG"></span>


DirectX のランタイムが、ドライバーが、DXT を作成することを要求したとき*n*圧縮テクスチャ画面幅と高さより小さい 4 x 4 ドライバー実際には、4 x 4 のブロックを割り当てますメモリ テクスチャ サーフェス用です。 ただし、ドライバー、幅と高さのテクスチャ サーフェスとして報告、ランタイムが要求された値。 たとえば、2 × 2 DXT1 圧縮テクスチャ サーフェスが要求された場合ドライバー 4 x 4 ブロックを割り当てますが、要求されたテクスチャ サイズを変更しないままにすると、ブロックが 2 x 2 であることを報告します。 特定の DXT を要求する*n*圧縮テクスチャ サイズ、ランタイム、 **dwWidth**と**dwHeight**のメンバー、 [ **DDSURFACEDESC** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550339(v=vs.85))または[ **DDSURFACEDESC2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))テクスチャ サーフェスを表す構造体です。 ドライバーでは、テクスチャ サーフェスの幅と高さが、4 x 4 未満の要求がある場合は、4 x 4 テクスチャ サーフェスを割り当てる場合でも、これらのサイズ設定は変更されません。

 

 





