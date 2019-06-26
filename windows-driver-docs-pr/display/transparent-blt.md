---
title: 透過 Blt
description: 透過 Blt
ms.assetid: bc2f4159-cd5d-43db-8bc3-e6fbf1e594fb
keywords:
- サーフェス WDK DirectDraw、中
- 描画 blt WDK DirectDraw、透過的な blt
- DirectDraw 中 WDK Windows 2000 の表示、透過的な blt
- 中 WDK DirectDraw、透過的な blt
- blt WDK DirectDraw、透過的な
- 色は、WDK DirectDraw をキーします。
- 透過的な blt WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a65f764dbf4109c1f0f627c185ee9d2c50a7ce4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353413"
---
# <a name="transparent-blt"></a>透過 Blt


## <span id="ddk_transparent_blt_gg"></span><span id="DDK_TRANSPARENT_BLT_GG"></span>


*透明 blt*、カラー キーが通常は移動されません色を指定します。 ソースのカラー キーは、映画で使用されるブルー スクリーンに似ています。 色は、各ピクセルと比較して、一致した場合、ピクセルはコピーされません。 一致しない場合は、ピクセルがコピーされます。 DirectDraw には、範囲のカラー キーもサポートしています。

場合によっては、透過的な blt を部分的にのみ、ハードウェアでサポートする可能性があります。 これは、ソフトウェア内で行うよりも高速可能性があります。 DDCAPS\_COLORKEYHWASSIST フラグは、このような場合に設定する必要があります。

部分的にサポートされている透過的な blt の例は、色キーを使用するだけではなく、ビットマスクを必要とするディスプレイ カードです。 この場合、各ピクセルをコピーするかどうかを判断する色キーを比較するのではなく、モノクロ マスクが作成されます。 色キーを持つすべてのピクセルが比較され、サーフェス全体は、ビットマスク (通常は 1 バイト、色の解像度に応じて 1 ビット) に変換されます。 DirectDraw を使用して、これは、画面のロックが解除されているときに行います。

アルファのマスクが作成されると、ソース画面と比較されます。 すべてのアルファのマスクが設定されていないことは、転送先のサーフェスにコピーされます。 これは、ソースのカラー キーと同じ効果を実現がマスクを比較して、同時コピーではなく最初に、ビルドする必要があります。 マスクは、いつでもカラー キーを設定を再構築する必要があります。 これもチェックする必要がたびに、blt は、その時点での色キーのオーバーライドを指定することができます。 ときに、アプリケーションの**Blt**関数が呼び出されると、カラー キー (blt に渡される唯一のカラー キー) をオーバーライドすることを確認は、画面で設定されているカラー キーと同じです。 場合は、同じですが、オーバーライドではない実際とマスクが再構築する必要はありません。 異なる場合、マスクをリビルドしてください。 (ドライバーの[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)関数は常にオーバーライドとして色キーを表示します)。

 

 





