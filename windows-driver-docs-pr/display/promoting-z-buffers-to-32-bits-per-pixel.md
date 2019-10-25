---
title: Z バッファーを 32 ビット/ピクセルに昇格
description: Z バッファーを 32 ビット/ピクセルに昇格
ms.assetid: 6b7dddab-e154-44e8-a4e3-45bd706ed638
keywords:
- z バッファー、WDK DirectX 9.0
- カラーバッファー WDK DirectX 9.0
- D3DFORMAT_OP_ZSTENCIL_WITH_ARBITRARY_COLOR_DEPTH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 858a99bea97c0168a7ca104112cc93ab99dbcbd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826038"
---
# <a name="promoting-z-buffers-to-32-bits-per-pixel"></a>Z バッファーを 32 ビット/ピクセルに昇格


## <span id="ddk_promoting_z_buffers_to_32_bits_per_pixel_gg"></span><span id="DDK_PROMOTING_Z_BUFFERS_TO_32_BITS_PER_PIXEL_GG"></span>


**このトピックは、DirectX 8.0 以降に適用されます。**

ディスプレイデバイスでは、ピクセル深度が異なる z バッファーとカラーバッファーのレンダリングがサポートされていないディスプレイドライバーでは、z バッファーと 32 bpp カラーバッファーの両方を同時にレンダリングするために、16ビット/ピクセル (bpp) z バッファーを 32 bpp に透過的に昇格させる必要があります。 ただし、z バッファーにはステンシルビットを含めることもできないことに注意してください。 このため、アプリケーションは、バッファーピクセル深度でこの不一致を修正する必要はありません。

ドライバーの表示デバイスで、ピクセル深度が異なる z バッファーおよびカラーバッファーにレンダリングできる場合、ドライバーは D3DFORMAT\_OP\_ZSTENCIL\_を設定します。これは、の**Dwoperations**メンバーの任意の\_色\_深度フラグ\_で設定されます。z バッファー形式の[**Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)構造体。 その後、Direct3D ランタイムによって、アプリケーションは z 色とカラーピクセル深度の不一致を表示できます。

ドライバーで D3DFORMAT\_OP\_ZSTENCIL\_が設定されていない場合は、z バッファー形式の\_深度\_が任意であるため、アプリケーションは 32 bpp カラーバッファーと 16 bpp z バッファーの不一致のみを表示できます。概要の段落で説明されているように、ステンシルのビット。 この場合、ドライバーは、要求された 16 bpp z バッファーの代わりに 32 bpp z バッファーを割り当てます。

D3DFORMAT\_OP\_ZSTENCIL\_\_任意の\_色\_深度が設定されていない場合、アプリケーションは次の不一致シナリオにレンダリングできません。

-   16 bpp カラーバッファーと 32 bpp z バッファー (同時に)。 このシナリオでレンダリングを成功させるには、ドライバーが 32 bpp z バッファーの 16 bpp z バッファーに置き換える必要があります。これにより z 精度が低下し、顕著な成果物が生成されます。

-   深度ステンシルが、カラーバッファーとしてピクセルあたりのビット数 (つまり、z とステンシルが一致しない) を占有していないすべての z 形式。 このシナリオでレンダリングを成功させるには、ドライバーがステンシルビットの数を変更する必要があります。これにより、顕著な成果物も発生します。

 

 





