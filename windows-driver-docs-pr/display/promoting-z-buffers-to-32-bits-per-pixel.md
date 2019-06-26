---
title: Z バッファーを 32 ビット/ピクセルに昇格
description: Z バッファーを 32 ビット/ピクセルに昇格
ms.assetid: 6b7dddab-e154-44e8-a4e3-45bd706ed638
keywords:
- z バッファー WDK DirectX 9.0
- カラー バッファー WDK DirectX 9.0
- D3DFORMAT_OP_ZSTENCIL_WITH_ARBITRARY_COLOR_DEPTH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f986a686c60a7754cb36691b87f6b6fac0e228ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383903"
---
# <a name="promoting-z-buffers-to-32-bits-per-pixel"></a>Z バッファーを 32 ビット/ピクセルに昇格


## <span id="ddk_promoting_z_buffers_to_32_bits_per_pixel_gg"></span><span id="DDK_PROMOTING_Z_BUFFERS_TO_32_BITS_PER_PIXEL_GG"></span>


**このトピックには、DirectX 8.0 以降が適用されます。**

ディスプレイ ドライバーが持つ表示デバイスが異なるピクセルの深度で z 値およびカラーのバッファーにレンダリングをサポートしていない z バッファーと 32 ビット/ピクセルの色のバッファーの両方を同時に表示するために z バッファーのピクセル (bpp) 32 ビット/ピクセルあたり 16 ビットに昇格透過的にする必要があります。 ただし、z バッファーがステンシル ビットもはできないことに注意してください。 そのため、アプリケーションでは、バッファーのピクセルの深度では、この不一致を修正する必要はありません。

ドライバー、ドライバーのディスプレイ デバイスは、異なるピクセルの深度の z 値およびカラーのバッファーにレンダリングできますが、設定、D3DFORMAT\_OP\_ZSTENCIL\_WITH\_任意\_色\_深さフラグ**dwOperations**のメンバー、 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat) z バッファー形式の構造体。 Direct3D の実行時に、アプリケーションのレンダリングに z と色ピクセルの深度の不一致がしことができます。

ドライバーは D3DFORMAT を設定していない場合\_OP\_ZSTENCIL\_WITH\_任意\_色\_z バッファー形式の深さ、ランタイムはのみ 32 bpp の不一致をレンダリングするアプリケーションを導入の段落で説明されているバッファーとありませんステンシル ビットの 16 bpp z バッファーを色します。 この場合、ドライバーは、要求された 16 bpp z バッファーの代わりに 32 bpp z バッファーを割り当てます。

場合 D3DFORMAT\_OP\_ZSTENCIL\_WITH\_任意\_色\_深さが設定されていない、ランタイムには、次のシナリオの不一致にレンダリング アプリケーションことはできません。

-   16 ビット/ピクセルの色のバッファーと同時に 32 ビット/ピクセル z バッファー。 このシナリオで正常にレンダリング ドライバーは、z の精度が低下すると大きな成果物が発生する 32 bpp z バッファーを 16 bpp z バッファーを置換する必要があります。

-   Z の形式の深度ステンシルを占有しません (つまり、一致していない z とステンシル サーフェス) のカラー バッファーと同じピクセルあたりのビット数。 このシナリオで正常にレンダリングでは、ドライバーは、顕著な成果物を原因となる、ステンシルのビット数を変更する必要があります。

 

 





